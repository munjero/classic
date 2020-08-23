---
title: "Extending the Ethoxy initiative"
subtitle: A new project called multi-geth
---

The [Ethoxy Initiative](https://github.com/ethoxy) was created around
December 2017. It was originally an attempt to facilitate
non-consensus-layer specifications for all Ethereum-like
blockchains. The initiative is really small, but it served its propose
-- a blockchain, called [Ellaism](https://ellaism.org) adopted a
[similar process](https://github.com/ellaism/specs) to
[ethoxy/specs](https://github.com/ethoxy/specs). I'm happy to announce
that another project, called *multi-geth*, will be maintained under
the Ethoxy Initiative.

<section markdown="1">

## A Geth Distribution Supporting Multiple Blockchains

*multi-geth* was originally developed by the [Ellaism
Project](https://github.com/ellaism). It is a fork of
[go-ethereum](https://github.com/ethereum/go-ethereum) that supports
multiple blockchains including Ethereum, Ethereum Classic, and
Ellaism. A [recent hard
fork](https://github.com/ellaism/specs/blob/master/specs/2018-0003-wasm-hardfork.md)
makes Ellaism not feasible to support go-ethereum any more. As a
result, the project is decided to be turned over and maintained under
the Ethoxy Initiative.

Just like how you can access multiple networks in
[Parity](https://github.com/paritytech/parity), *multi-geth*'s end
goal is to gain compatibility. With this nature, our maintenance
process is pretty simple: with every new release of *go-ethereum*, we
apply a small patch, whose only propose is just to add additional
blockchain supports. And we tag it and make a release. That's it.

With this, besides using this for your favourite Ethereum-like
blockchain, it also benefits you in that:

* It can acts, as the README describes, a **drop-in replacement** for
  go-ethereum. We promise nearly nothing will break, because our patch
  is really small.
* You can apply the **newest non-consensus-layer improvements** on
  Ethereum to your favourite Ethereum-like blockchain. For example,
  light clients and EIP-706 (snappy compression) work out of the box
  for Ethereum Classic, given you have a neighbor multi-geth node near
  you.
  
And that's all. Hope you enjoy the project! Credits should go to
the Ellaism Project which started it and maintained it up to this
point.

* Project Page and Issue Tracker:
  [source.that.world/source/multi-geth](https://source.that.world/source/multi-geth/)
* Release Download:
  [github.com/ethoxy/multi-geth/releases](https://github.com/ethoxy/multi-geth/releases)
  
</section>
