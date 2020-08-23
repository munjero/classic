---
title: Parallel transaction execution in SputnikVM
subtitle: Executing multiple transactions in a MapReduce-like fashion.
---

<section markdown="1">

In Ethereum, the Ethereum Virtual Machine (EVM) is responsible for the
actual transaction execution and state transition. It is observed
that, given a certain block in the blockchain, most of the
transactions are unrelated. This is due to the fact that there are a
vast number of addresses on the blockchain, and at the same time, a
valid transaction depends on the nonce of the `from` address. This
makes it possible to execute transactions in a transaction sequence in
parallel, and thus speed up the client.

Issues do exist, however. In Ethereum, bank-like account structure is
used instead of UTXO. This makes it so that a given transaction can
modify a large number of unrelated accounts. So what we can do is to
use a MapReduce like process. First, try to execute all transactions
in parallel, and join the results together. Second, do the state
transition based on the execution results one by one, if at any
transaction conflict is detected, re-execute that single transaction
and continue.

SputnikVM and the `sputnikvm-stateful` crate provide an easy way to
do this. You can find the full
example
[here](https://github.com/ethereumproject/sputnikvm/blob/f5d386063d480a4215aa9ea465ac898b904591c6/stateful/examples/parallel.rs). SputnikVM
never directly modifies the state. Instead, it returns the state
changes, and let the executor decides what to do with them. This turns
out to help in reduce the complexity of parallel execution
implementation.

</section>

<section markdown="1">

## The Code in Rust

We first create a `MemoryStateful`. This is a wrapper around the
Merkle trie of account states and SputnikVM, which deals with
SputnikVM's `RequireError` automatically.

```rust
let stateful = MemoryStateful::default();
```

For parallel referencing of the stateful, we wrap it around Rust's
`Arc` struct.

```rust
let stateful = Arc::new(stateful);
```

Then, simply execute all transactions in parallel, and join the
results.

```rust
let mut threads = Vec::new();
for transaction in transactions {
    threads.push(thread::spawn(move || {
        let vm: SeqTransactionVM = stateful.call(
            transaction, header, &EIP160_PATCH, &[]);
        vm.accounts()
    }));
}

let mut thread_accounts = Vec::new();
for thread in threads {
    let accounts = thread.join().unwrap();
    thread_accounts.push(accounts);
}
```

After that, each one of the threads returns a result containing all
account changes for that particular transaction. We check whether a
particular account is fetched or changed in any of the previous
transactions. If not (which should be of most of the times), then
continue, otherwise, simply re-execute the transaction.

```rust
for (index, accounts) in thread_accounts.into_iter().enumerate() {
    let accounts = if is_modified(&modified_addresses, &accounts) {
        // Re-execute the transaction if conflict is detected.
        println!("Transaction index {}: conflict detected, re-execute.", index);
        let vm: SeqTransactionVM = stateful.call(
            transactions[index].clone(), header.clone(), &EIP160_PATCH, &[]);
        let accounts: Vec<vm::Account> = vm.accounts().map(|v| v.clone()).collect();
        accounts
    } else {
        println!("Transaction index {}: parallel execution successful.", index);
        accounts
    };

    stateful.transit(&accounts);

    for account in accounts {
        modified_addresses.push(account.address());
    }
}
```

In the end, you get the account state that is the same as executing
the given transaction sequence in a single thread.

</section>
