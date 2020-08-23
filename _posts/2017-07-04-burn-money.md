---
title: Burn money on an Ethereum blockchain
subtitle: Using the SUICIDE opcode to make Ether magically disappear.
---

<section markdown="1">

There are two ways to burn money on an Ethereum blockchain. The first
way is to accidentially lose a private key or to send money to a
contract that cannot be retrived. In this case, total sum of money of
all accounts in the blockchain remains unchanged. The second way is to
just magically make money disappear. After you do that, the total sum
of money of all accounts in the blockchain will be reduced.

In an Ethereum blockchain, to burn money in the second way is really
easy using the SUICIDE opcode. The SUICIDE opcode accepts one
argument -- the receiver of the money to be transferred. It then sets
the current account balance to zero. So if one accidentally set the
argument as the same account as the current account, the money will
first be transferred to itself -- no problem, but then, the current
account balance -- again this is the account itself -- will be set to
zero. In this way, some money is just burnt to nowhere.

</section>
