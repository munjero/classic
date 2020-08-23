---
title: "SputnikVM integration and chainsplit monitoring"
subtitle: Parity, go-ethereum and SputnikVM
---

<section markdown="1">

With [SputnikVM
integration](https://github.com/ethereumproject/go-ethereum/pull/413)
merged to go-ethereum, we now have four client configurations that
support the Ethereum Classic blockchain: Parity, Mantis, go-ethereum
with ClassicVM, and go-ethereum with SputnikVM. Below is a simple
service that integrates with That World's monitoring
infrastructure. It does a simple check on whether go-ethereum with
SputnikVM and Parity can agree on the same block, and alert me if
there's any potential chainsplit caused by software bugs.

If you are interested in helping out to test go-ethereum with
SputnikVM integration, you can download [go-ethereum
nightly](http://builds.etcdevteam.com) and run geth with `./geth
--sputnikvm`.

</section>

<iframe src="https://grafana.that.world/dashboard-solo/db/ethereum-classic?orgId=2&panelId=1" width="100%" height="400" frameborder="0"></iframe>
