---
title: Deprecate support of Ethereum Classic
subtitle: Principle of maximum consensus and user choices, why Ethereum Classic now fails the test, and some practical reasons.
---

*([Discuss on
Mastodon](https://social.that.world/@wei/104325275984083255))*

I have been supporting the development of Ethereum Classic since the
early days. However, as of today, I have planned to deprecate my
support of this particular blockchain.

In this final post of this blog, I want to explain the reasoning. I'll
first explain a core developer guideline which I call **principle of
maximum consensus and user choices**. I'll then explain why Ethereum
Classic now **fails the test** of that principle due to loss of
immutability. In the end, I'll also discuss some **practical reasons**
that I withdraw my support.

## Principle of maximum consensus and user choices

Blockchains, in essence, are about reaching consensus. In a
decentralized way, users reach consensus of the current "world state"
of a blockchain, in particular, how much money an account has, and
what then end result of a smart contract execution is. Without
consensus, blockchains do not exist.

The reality is that there are many blockchains. On one hand, varities
should be encouraged for competition, and for healthy development of
the ecosystem. On the other hand, unnecessary splits should be
minimized, because otherwise, there will be no consensus in existence.

Core developers participate, and arguably play an important role in
maintaining the ecosystem. Private influcences and even bribery are
inevitable. However, it does not mean that core developers have to
become puppets. **As with many other engineering fields, blockchain
developers can also define their own ethics and guidelines to follow,
in order to maximize social benefits -- make consensus more likely,
user choices more respected, and the ecosystem more healthy.** Ethics
and guidelines allow us to contribute to the broader blockchain
community, and not just our own pockets. By keeping the ecosystem's
health and growth, we make blockchains as a whole more valuable, and
thus our own work more valuable.

We discussed above that we want to maintain two things --
**consensus** and **user choices**. On one hand, maintain consensus,
to minimize disruptions and splits, because they bring confusion and
loss of money to investors. That means, unless there are good reasons,
core developers should **follow the consensus of the majority**. On
the other hand, respect user choices. That means, **when conflicts
happen, it is not ethical for core developers to censor a voice.**
Rather, we should encourage discussions, provide signaling solutions
and support both sides, in order to give time and space for all sides
involved to resolve the conflict.

* **Consensus**: disruptions and splits should be minimized, because
  otherwise consensus does not exist.
* **User choices**: blockchains are used by users. Varities and
  healthy competitions should be encouraged.

This issue of consensus and user choices is particularly apparent
during a hard fork process, because hard fork is when the majority of
disruptions and splits happen. Here we argue about two different point
of time during a hard fork, **pre-hard-fork** and **post-hard-fork**.

* **Pre-hard-fork**: this is the time when the hard fork has not yet
  happened. Splits and disruptions do not happen at this time. As a
  result, if conflicts happen, we should prioritize discussions --
  provide implementations for all sides, and conduct signaling and
  voting solutions when possible, in hope of the conflict can be
  resolved during this process.
* **Post-hard-fork**: this is the time when the hard fork has
  happened. Splits and disruptions, if they happen, start to damage
  the blockchain. As a result, consensus should be prioritized *unless
  there are good reasons*. That means, core developers should follow
  the majority of consensus, unless there are **current principle,
  philosophical, or technical** reasons to support other sides.
  
During pre-hard-fork, if discussions are not encouraged or if any side
is censored, it harms healthy competitions and can cause better
solutions to be ignored. During post-hard fork, if majority of
consensus is not followed unless with good reasons, a blockchain can
easily split into many different ones of the same thing, with the
essential functionality of the blockchain being lost.

Another important thing to discuss is about **good reasons** to
artifically cause a split. A fundamental difference in principle,
philosophy and technical implementation is a good reason. The reason
must also be **current**, meaning that this must be the **last
possible point when the difference has to appear on-chain**. If two
parties claim to hold different goals and roadmaps of a blockchain *in
the future* but without any current divergence, then that is not a
good reason to cause a split *right now*. They can continue to stay as
one blockchain and split in the future when it indeed becomes
necessary.

The principle of maximum consensus and user choices can be summerized
as follows:

> Core developers should, prior to a hard fork, maximize choices for
> users, and post a hard fork, minimize possibility of splits.

## Failing the test for Ethereum Classic

Ethereum Classic (ETC) is unique among all Etheruem-based blockchains,
in that it is one of the only blockchains among them that was created
during a split, unlike others which only reuse the codebase with
completely new genesis blocks. This is what makes it relevant to
discuss the **principle of maximum consensus and user choices** in
regards of Ethereum Classic.

We must first acknowledge that the original reason ETC artifically
caused the split **was a good reason**. When the ETC side argues that
theDAO breaks the principle of code-is-law and immutability, it is an
apparent philosophical difference that must be respected. However,
that good reason is **no longer accepted** among many ETC core
developers any more -- in Phoenix hard fork of Ethereum Classic,
developers decided to **[intentionally
break](https://gist.github.com/sorpaas/72ce0618829849901e0f83bf43738ecb)**
several low-value smart contracts that have already been deployed
on-chain.

The loss of immutability principle for ETC essentially makes it the
same thing as Ethereum (ETH), both taking the pragmatic position of
immutability, arguing that it should give ways to developments and
experiments, even if that slightly trades off stability. There's
nothing wrong with this approach, and in fact, as ETH core developers
have put it, because we're still in the early days of blockchains,
this approach has many advantages. However, for ETC, by being the same
thing as ETH, it has essentially lost its distingishing factor. If two
things are basically the same without even any principle or
philosophical differences, if the original good reason that caused the
disruptions and splits of ETH and ETC is not longer valid, then I
think for a healthy ecosystem of Ethereum, we should follow the
majority consensus of ETH, or support a merge of ETH and ETC.

One argument from some ETC developers is that ETC also has some other
distinguishing features *on the roadmap*. A notable one is that it
wants to stay in Proof of Work forever, whereas in Ethereum the goal
is to eventually move to Proof of Stake. However, we note that this is
**not** a good reason to cause a split **right now**, because the
split **does not have to be immediate**. Ethereum is still in solid
Proof of Work state, so if only for this reason, both blockchains
could still have stayed together until the final days when the move of
Ethereum to Proof of Stake happens. The disruptions and splits caused
right now are unnecessary.

## Practical reasons

There are also practical concerns regarding supporting ETC.

Ethereum historically has a unique property -- it has multiple client
implementations with competitive shares. It's not the only blockchain
with multiple implementations. Bitcoin has multiple clients as
well. However, Bitcoin Core has always dominated the market.

Ethereum's model requires a collabrative culture among
developers. Péter Szilágyi, the lead developer of Go Ethereum, has
described the culture quite nicely in various core dev meetings. It
basically requires all development teams to hold some basic restraints
when dealing with other teams. This avoids "implementation wars",
where implementations spend unnecessary marketing resources to
downplay other teams. The restraints are held because all teams
recognize that promoting one's own unique features and performance
advantages is beneficial to the team and the ecosystem, while
downplaying other teams only incites anger, hurts relationship with
other teams, and damages the ecosystem. This basic understanding
allows the whole development community to remain competitive, while at
the same time, be able to work together.

ETC inherited Ethereum's multiple implementation development
model. However, it failed to inherit this essential collabrative
culture. Over the past years, we have seen people like Afri Schoedon
[holding public aggresions](https://imgur.com/a/u4rwicO) towards other
clients, teams like ETC Labs actively [asking users to switch away
from
OpenEthereum](https://medium.com/etc-core/migrating-from-parity-to-core-geth-d39606ad00c2),
[copying the MultiGeth codebase to CoreGeth but at the same time
removing the
credits](https://web.archive.org/web/20200611210024/https://github.com/etclabscore/core-geth/pull/106),
and the famous [blame
game](https://that.world/~classic/2020/01/24/controversy/) for the
later-rejected Aztlan hard fork. The aggressive marketings from
various parties have broken the competitive collabration culture of
Ethereum Classic, and since made the multiple implementation ideal
much harder to realize.

The lack of collabrative culture of ETC has made bugs and issues much
harder to handle. When
[provocations](https://github.com/openethereum/openethereum/issues/11744#issuecomment-636822895)
and [not-my-problem
attitudes](https://twitter.com/etc_core/status/1267443141352849408)
become the norm, we can hardly focus on the bug but spend the
resources on blaming others. This has made supporting ETC a huge
liability -- teams do not want to congrats each other because they
want to promote their own implementations, but whenever things go
wrong, teams [will not hesistate to blame
others](https://that.world/~classic/2020/01/24/controversy/#appendix-past-controversies-in-ethereum-classic).

## Conclusion

With ETC dropping its principle of immutability, following the
**principle of maximum consensus and user choices**, it has become a
non-majority blockchain that was in almost all aspects same as
Ethereum, including philosophy and principles. Supporting it will mean
supporting unnecessary disruptions and splits, with no good reasons
**right now**. The future of Ethereum Classic might follow a different
roadmap than Ethereum, but that is not a good reason to have already
split now.

I wrote the first ETC-specific EVM implementation SputnikVM, maintain
MultiGeth and ETC support for OpenEthereum. Involved in Ethereum
Classic for so long, I wish the ETC community well with good
faith. However, in its current form, it has become a blockchain that I
cannot provide development support to.

## FAQ

**What about other Ethereum-based blockchains? Do you continue to
support them?**

Yes. I'll continue to support all other Ethereum-based
blockchains. Unlike ETC, other Ethereum-based blockchains do not
undermine the principle of maximum consensus and user choices. ETC is
the only Ethereum-based blockchain I know that was created in a split
of Ethereum mainnet. Other Ethereum-based blockchains only use the
Ethereum codebase, but with completely different genesis blocks, and
thus do not qualify as splits, and do not cause disruptions.
