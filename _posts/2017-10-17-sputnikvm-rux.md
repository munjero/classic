---
title: SputnikVM, the Rux microkernel, and embedded devices
subtitle: Running SputnikVM on the Rux microkernel using Rust's no_std feature.
---

<section markdown="1">

If one wants to get cryptocurrency integrated with embeded devices and
actually do something more useful than relaying transactions (like
Blockstream's satellite), at least a light client is needed. In one
part, the light client uses Merkle proofs for querying to avoid
storing the full "world state" locally. In another part, the light
client also needs to be able to execute transactions and get the
result locally. This posts talk about the later.

Usually in embedded devices, resources and computations are
limited. There might only be a really lightweight microkernel, or even
no kernel running. That means, many features you would expect to be
immediately available once a program is started will not be
there. This may even include memory management. And a program that
wants to run on an embedded device will need to deal with them.

The above restrictions make
[Rux](https://source.that.world/source/rux/) a good test ground. Rux
is a microkernel that I started to develop around last year. With a
lot of ideas borrowed from seL4, it features a capability-based
system. One particular thing about Rux is that it only deals with the
bare-minimal amount of resource management, and delegate the actual
memory management to userspace. *(In the mean time, Rux handles task
scheduling, which is currently a Robin-round scheduler, because in the
general microkernel research field, there [has not been a good
solution](http://sigops.org/sosp/sosp13/papers/p133-elphinstone.pdf)
for an userspace scheduler.)*

SputnikVM itself can be considered a pure function -- it recieves all
the inputs it needs in the beginning, does some computations, and then
generates all the outputs in the end. In the middle, no interaction is
required. This makes it so that the VM can be ported to require only a
minimal set of functionalities from the kernel:

* Basic task scheduling, or in the case of running bare metal, no task
  scheduling is needed.
* Memory resources management, to tell the program which physical
  memory areas are available for use.
  
After that, SputnikVM can use a [self
allocator](https://source.that.world/source/rux/browse/master/selfalloc/)
and do its own memory management, paging and heap allocation in
userspace.

Right now, given a VM context, and the block header parameters, the
[ported VM](https://github.com/ethereumproject/sputnikvm-on-rux)
running on Rux is able to execute simple transactions, calculate the
used gas, and get the result. Below I'll talk about the details of how
to try the program (called `sputnikvm-on-rux`) yourself and what
actually happens under the hood.

</section>

<section markdown="1">

## Running SputnikVM on Rux

Running SputnikVM on Rux, means SputnikVM would act as the kernel init
program -- the first userspace program that the kernel starts.

First we need to build the kernel:

```bash
git clone https://github.com/ethereumproject/sputnikvm-on-rux
cd sputnikvm-on-rux
git submodule init --recursive --update
```

This, besides `sputnikvm-on-rux`, will also checkout a revision of the
[Rux microkernel](https://source.that.world/source/rux/). After that,
please install [Nix](https://nixos.org/nix) and run

```bash
nix-shell
make sinit-sputnikvm
```

The last command will build the kernel and the init program, load them
via QEMU virtual machine, and obtain the result. A test transaction
will be executed by SputnikVM, after that, you should see something
like this:

```
Exit code: 99, test succeed.
```

</section>

<section markdown="1">

## Under the Hood

For Rux, when it bootstraps, it does several things:

* Load the init program into the memory.
* Set up paging for the init program, and map it to the correct
  virtual address location.
* Create a memory area for stack for the init program, and map it in
  paging.
  
After that, Rux switches to the init program, and only handles task
scheduling from that point on.

A Rust program requires [stack and
heap](https://doc.rust-lang.org/book/first-edition/the-stack-and-the-heap.html)
to run. A simple one only requires stack, but SputnikVM requires
both. So next, after Rux switching to the init program, the init
program will need to handle heap allocation. This is done using a
[self
allocator](https://source.that.world/source/rux/browse/master/selfalloc/src/lib.rs).

The allocator will first check whether it already has enough
memory. If not so, then it requires additional memory areas from the
kernel:

```rust
system::retype_raw_page_free(self.untyped_cap);
```

After that, the allocator maps the new page:

```rust
system::map_raw_page_free(self.page_start_addr,
                          self.untyped_cap,
                          self.toplevel_table_cap,
                          self.page_cap.clone());
```

Rust has a nice allocator interface that allows developers to declare
custom allocations:

```rust
#[global_allocator]
static WATER_ALLOCATOR: WaterAlloc = WaterAlloc;

unsafe impl<'a> Alloc for &'a WaterAlloc {
    ...
}
```

At this stage, everything SputnikVM needed is there, we can start to
[execute a
transaction](https://github.com/ethereumproject/sputnikvm-on-rux/blob/master/sinits/examples/sputnikvm.rs).

```rust
let mut vm = SeqContextVM::<MainnetEmbeddedPatch>::new(
    context, header);
vm.fire().unwrap();
```

Then we check whether we get the correct result, and use a special
kernel system call to inform QEMU:

```rust
if vm.available_gas() == Gas::from_str("0x013874").unwrap() {
    system::debug_test_succeed();
} else {
    system::debug_test_fail();
}
```

</section>
