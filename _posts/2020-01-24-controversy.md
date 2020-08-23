---
title: Aztlan controversy in Ethereum Classic
subtitle: What caused Aztlan hard fork to be a disaster for Ethereum Classic?
---

This post serves as a timeline of what happened during the recent
Ethereum Classic controversy. The event caused Aztlan hard fork
(ECIP-1061) being cancelled and eventually rejected because of
specification flaws, and testnets Kotti and Mordor being broken for
weeks.

The goal of this post is not to judge right or wrong, but to provide
references of the controversy history, drama, blame game, and
everything else. I hope what readers take from this post are lessons
learned in the hard and daunting task of managing a specification
repository for a decentralized community.

## Background and people

ECIPs, also known as Ethereum Classic Improvement Proposals, are a set
of specifications and processes that ease the complexity of hard fork
on the Ethereum Classic blockchain.

There are several people and groups involved in the timeline.

* **Wei Tang**: that is me, core developer at Parity Technologies and
  I have also been independently involved in Ethereum Classic and
  participating in core development since 2017.
* **ETC Labs, ETC Labs Core, ETC Core**: A new team that joined
  Ethereum Classic in 2018. The team [took
  over](https://medium.com/@splix/on-the-attempt-to-take-over-ethereum-classic-etc-64d19a70eb6e)
  previous developers from ETCDEV team and arguably caused many
  controversies at that time.
* **ETC Cooperative**: A non-profit organization that has been
  involved in Ethereum Classic since 2018. It focus more on the
  marketing and coordination front, rather than core development.
* **Afri Schoedon**: Also known by handle `5chdn`, `soc1c` and
  `q9f`. Originally focused on Ethereum and famously known for
  [EIP-999](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-999.md). After
  [rage-quitting](https://finance.yahoo.com/news/top-ethereum-developer-afri-schoedon-193119608.html)
  Ethereum development, Afri switched to work on
  [Dothereum](https://blockonomi.com/ethereum-fork-dothereum/), and
  then for ETC Labs on Ethereum Classic in 2019. Although he claims
  that all his handles should be pseudonymous, he has
  [personally](https://twitter.com/a4fri/status/1245404388736282624)
  [associated](https://twitter.com/ameensol/status/1116425919206322176)
  his handles with his real name many times.
* **Bob Summerwill** and **Yaz Khoury**: Works for ETC Cooperative.

## The beginning

After theDAO hard fork, ECIPs are forked from the same process in
Ethereum, called EIPs (Ethereum Improvement Proposals). The initial
process was slow, in that no one, even a core developer, knows the
precise rules on how to write specifications, move it forward, gather
consensus, and apply it in a hard fork. In June 2017, I drafted
ECIP-1000 as an attempt to define the process. The draft moved slowly,
but after two years of iterations and great feedback from the
community, in early 2019, ECIP-1000 was finally enacted as the active
process. In the document, a role called ECIP editors, which handles
administrative tasks of the ECIP repository, was proposed. With the
community's support and enthusiasm, five editors were accepted. Things
initially went well. PRs moved significantly faster than it was
previously, and two successful hard forks, Atlantis and Agharta, were
conducted. The result can be seen clearly on Github's [analytics
page](https://github.com/ethereumclassic/ECIPs/graphs/contributors). Notice
the sudden spike of commits since summer 2019.

ECIP repository is hosted on a platform called Github. On Github,
developers collaborate on code using a quite specific workflow. Code
is first initially "forked", either to another repository or to the
same repository of a different branch. It is then submitted back as
pull requests (PRs) for reviews. After a sufficient number of reviews,
maintainers can proceed to merge PRs. Maintainers can also "request
changes" of a PR, indicating that she or he believes that something
may need to get fixed first before it is merged. 

In addition, Maintainers can "dismiss" other people's review. This
indicates that either the review has already been well-addressed but
the reviewer cannot be contacted (to re-submit the review
herself/himself), or a maintainer wants to bypass another maintainer's
review. "Dismiss" is generally thought to only be used in specific
situations where all other methods do not work. The UI also made this
clear, by making the action of "dismiss" a tedious two-step process --
a reason field that must be filled in, and a confirmation button.

## Provocation

When Afri rage-quited Ethereum, it was arguably due to his unfortunate
tendency of provocation, as shown by the original Polkadot vs Ethereum
tweet. Sadly, when he comes to Ethereum Classic in 2019, that tendency
of provocation seemed not to have changed.

The controversy starts with
[PR#194](https://github.com/ethereumclassic/ECIPs/pull/194) on
ECBP-1076. The PR proposed some changes in the documents, and at the
same time, attempted to move it from "Draft" to "Active". I was
slightly puzzled by the changes, so I submitted a "request changes"
review, for two reasons:

* There were still issues unaddressed in the draft
  specification. ECBP-1065 was indeed discussed in a previous
  meeting. Although I was not able to join, prior to that meeting,
  people (including me) wrote some concerns related to the
  specification, and I couldn't find them addressed. Based on my
  experience with Ethereum's AllCoreDevs, I also find it quite unusual
  to propose a proposal for the first time and accept a proposal in
  the same meeting.
* The move to "Active" status was unheard of and potentially unfit for
  the ECIP process. ECBP corresponds to Ethereum's ERC
  specifications. Specifications in this category usually goes from
  "Draft" into "Last Call" and then to "Final", but not "Active"
  status.

So I asked to put the PR on hold -- it will be better if we could have
more discussions before moving this specification out of draft. What
followed is Afri's immediate action to "dismiss" the review, citing
that the meeting is sufficient to make the decision. After some back
and forth and both parties got more angry, Afri submitted a
[PR#196](https://github.com/ethereumclassic/ECIPs/pull/196) as an
attempt to remove me from the whole ECIP process.

This was the first attempt by Afri to remove me from ECIP
editors. Several days later, the attempt turned out to be not
successful, and the PR was closed.

### Aztlan

Then we came to the Aztlan hard fork. It starts with this
[PR#199](https://github.com/ethereumclassic/ECIPs/pull/199), moving
Aztlan (ECIP-1061) specification from "Draft" to "Accepted". The
initial dispute was on the ECIP number -- as we couldn't figure out
whether the specification we actually accepted in the meeting was
ECIP-1061 or ECIP-1072. Afri's argument was that we should only have
one ECIP for a hard fork, but not any competing ones. My argument was
that at that time ECIP-1072 had the final specification we agreed on,
but copying it back to ECIP-1061 (which had the sad effect of making
ECIP-1061 and ECIP-1072 identical) would not be a good idea. This
might have been a normal argument that would have been resolved like
everything else we had in Ethereum Classic community. However, Afri
decided to do something highly unusual -- instead of engaging in the
discussions and try to persuade the other side, he chose to force
merge the PR by using the privileged "dismiss" functionality in
Github. This was where things went out of hand.

The whole thing then quickly turned into a drama, to be what is known
as the ECIP-1061 vs ECIP-1072 debate and people have already started
to pick sides. Bob Summerwill, the ETC Cooperative executive, first
decided to [support
ECIP-1072](https://github.com/ethereumclassic/ECIPs/pull/199#issuecomment-559185183)
but later switched to supporting ECIP-1061. Employees from ETC Labs
mostly supported ECIP-1061, as Afri is also affiliated with
them. Later, I decided to withdraw ECIP-1072 and in a later meeting,
agreed to move with ECIP-1061 as a compromise.

## Accountability

The drama of ECIP-1061 vs ECIP-1072 might have been over, but the
controversies had not. My concern was on the power of "dismiss". In
the ECIP repository, we have many cases where more than two people
from the same organization have write access. This is true for ETC
Coop, true for ETC Labs, and true for many other organizations. **If
it becomes a norm in using "dismiss" button like what had happened in
ECBP-1076 and Aztlan, then it will be a great centralization
risk. Those organizations will practically be able to merge any
changes into ECIP no matter how many objections there are.**

### Irregular process transition

As I'm quite unsatisfied with the accountability issue of ECIP-1061, I
created [PR#220](https://github.com/ethereumclassic/ECIPs/pull/220) as
an attempt to confirm that the "dismiss" happened in Aztlan ECIP-1061
was an exception and against the process, but not a norm.

This is when people started to take sides and when it went out of
control. One or two people who still thought this was about ECIP-1061
vs ECIP-1072, which was quickly clarified. However, a few people
started to argue that the "dismiss" happened in Aztlan ECIP-1061 is
justified, and even went as far as saying ECIP-1072 was against the
process, this also included Yaz, the person who approved the
[PR](https://github.com/ethereumclassic/ECIPs/pull/184) that merged
ECIP-1072 into master.

In the exchange, I also mentioned some practical issues that those
force merges might result into, for example, higher likelihood of
flawed specifications. 

The issue has nearly turned into an "anti-knowledge movement". **Yaz
Khoury**, an employee from ETC Cooperative, said the following in an
exchange about the accountability issue, of whether we're assured that
Aztlan is safe to be activated, when many parts of the specification
did not adequately follow the process:

> You can ask me about the safety properties of the hardfork, but
> you're just changing the subject to show off how much you know about
> the technical details of the hardfork in question

This has arguably caused Aztlan hard fork to be quite under-reviewed,
and attitudes like this is arguably one of the reasons why later the
Aztlan design flaws were discovered.

### Pseudonymization

To my surprise, later there was attempts in shifting the topic, from
something on process, to "doxxing". I was accused of using Afri's real
name instead of his handle `soc1c` in ECIP-1000's editor list. This
rather comes to a surprise of me, because not only was the editor list
already merged 6 months ago (which everyone agreed on, including
Afri), but also Afri's real name has been well-known [in the
community](https://twitter.com/ameensol/status/1116425919206322176),
to the point that even Afri himself [uses his real name
frequently](https://github.com/ethereumclassic/ECIPs/issues/174#issuecomment-557106181)
before the controversy happened. As `MiKo`, the ETC Discord
administrator, has put it:

> From my perspective, just being on calls in discord. There was
> always a connection of `soc1c` === Afri through the public
> conversations here. IIRC there was a push to try and keep his name
> out of association with ETC early on, but as I recollect, we always
> knew Afri === `soc1c`.

All things considered, you can imagine how I find that argument of
"doxxing" quite absurd. I [raised the
issue](https://github.com/ethereumclassic/ECIPs/pull/267), alongside
with some other concerns on how we can make editors take
responsibilities when they're pseudonymous. However, all of those
concerns also quickly met with Afri's "dismiss" button again.

## Design flaws in Aztlan

In December 2019, I did an additional round of review and wrote down
some design flaws contained in Aztlan ECIP-1061 on [Core
Paper](https://corepaper.org/ethereum/fork/istanbul/#_ethereum_classic). It
was apparent to the whole ETC community that those design flaws will
seriously damage the effect of the hard fork. Leaving them unfixed,
Aztlan would not really be useful.

At that time, ECIP-1061 was already in "accepted" status. In usual
terms, that means clients can start to implement it. The
specification, under "typical paths", cannot be changed. In addition,
it can only be moved to either "final" or "rejected". This is indeed
also how it worked in Ethereum (see Constantinople and Petersburg hard
forks).

Immediately after the flaws were published, a proposal from ETC
Cooperative quickly emerged, aiming at specifically allowing ECIP-1061
to be able to revert back to "draft". That proposal was turned down by
the whole community.

## Blaming the implementors

On February 20th 2020, Yaz Khoury accused me of "implementing the
flawed Aztlan specification in MultiGeth and OpenEthereum". This
clearly looks like a cover-up / muddy-the-water attempt to hide the
fact that they pushed forward Aztlan, and I was literally forced to
implement it as they show me as the "community consensus". I still
find Yaz and ETC Cooperative's action quite unethical as it does not
seem to be willing to take any responsibility of its own actions.

I wrote a tweet thread as
[explanation](https://twitter.com/sorpaas/status/1231104348094189569). I
[also wrote some
posts](https://twitter.com/sorpaas/status/1231197997557583872) on what
I think are actually happening.

## Second attempted expel

Later, Bob Summerwill and Yaz Khoury supported a proposal to "expel"
me from the ETC ecosystem, as "ECIP-0001". It's basically a copy of
ECIP-1000, with my name removed from the editor list.

The community later rejected the proposal and the author of ECIP-0001
declared that he wants to [withdraw the
proposal](https://github.com/ethereumclassic/ECIPs/pull/313).

## Final thoughts

As an independent developer who does not really have any financial
involvements in ETC, I can understand why ETC Cooperative and ETC Labs
consider me as a "trouble-maker". In July 2019, I played a major role
in blocking an attempt from ETC Labs to "accelerate" the Atlantis hard
fork, due to potential issues in client implementations (later, we
indeed found several consensus bugs in Classic Geth). In October 2019,
I strongly questioned ETC Cooperative's motives in rushing Aztlan
ECIP-1061, due to bypassing the process and insufficient reviews
(later, we indeed found some design issues as described in the last
section).

The landscape for Ethereum Classic has changed dramatically in the
last year. After
[Igor](https://medium.com/@splix/on-the-attempt-to-take-over-ethereum-classic-etc-64d19a70eb6e),
the founder of ETCDEV team, was pushed out of the community,
independent "hardcore" developers start to fade. It unfortunately felt
more and more like a cooperate thing, rather than an open source
community. In the mean time, the community is also under considerable
centralization risks. Out of the total 6 ECIP editors we currently
have, ETC Labs controls 3, and ETC Cooperative controls 1 (the number
can raise to 2 soon as Bob has declared his intention to become an
ECIP editor).

I want to be in a community where I can be proven wrong, but not to be
blamed by some obscure reasons like "doxxing" or "blocking the
process". I do like Ethereum Classic for its philosophical baseline,
but based on recent events, I do think it's slightly losing on what it
stands for.

I hope this is not the last post I write for Ethereum Classic. No
matter what happens, I wish ETC to have a good and bright future.

So Long, and Thanks for All the Fish!

## Appendix: Past controversies in Ethereum Classic

Ethereum Classic historically is a blockchain filled with
controversies, and the Aztlan controversy was definitely not the first
one. For reference, below is a list of past controversies I can
remember that has happened on Ethereum Classic.

* **ETC Labs takeover** (December 2018): a take-over attempt by ETC
  Labs, which took advantage of ETCDEV team's financial situation. ETC
  Labs then formed ETC Labs Core consisting of mostly original
  developers from ETCDEV, and later renamed it to ETC
  Core. [Source](https://medium.com/@splix/on-the-attempt-to-take-over-ethereum-classic-etc-64d19a70eb6e).
* **ETC Labs' Atlantis "surprise" announcement** (June 2019): ahead of
  Atlantis hard fork schedule in June, ETC Labs Core did a surprise
  announcement to "accelerate" the Atlantis hard fork from the
  originally scheduled date of September to August. The surprise
  announcement was eventually rejected by the community. The attempt
  caused many controversies during the
  process. [Source](https://medium.com/ethereum-classic-labs/announcement-on-the-etc-atlantis-hard-fork-3742974f5363).
* **Yaz Khoury's using of Ethereum fund to promote Ethereum Classic on
  social media** (February 2020): Yaz, an employee from ETC
  Cooperative, allegedly took advantage of an Ethereum funding scheme
  to promote Ethereum Classic. The amount is relatively small, but
  caused some people to question whether this behavior is
  ethical. Aragon Court later held a trail on its platform to discuss
  whether the funding scheme should blacklist
  Yaz. [Source](https://www.crowdfundinsider.com/2020/02/157679-billionaire-venture-capitalist-tim-draper-acquires-1-million-ant-tokens-worth-825000-joins-aragon-blockchain-platforms-governance-structure/).
* **ETC Labs' accusation of "gross mismanagement" of Bob Summerwill
  from ETC Cooperative** (March 2020): James Wo, who resigned from the
  board of ETC Cooperative, accused Bob Summerwill from ETC
  Cooperative of "gross mismanagement" of the
  organization. [Source](https://web.archive.org/web/20200610075346/https://jameswo888.wordpress.com/2020/03/17/mismanagement-at-ethereum-classic-cooperative/).

## Appendix: Timeline

**On June 28th 2019, the first formal ECIP process (ECIP-1000) was
[merged](https://github.com/ethereumclassic/ECIPs/pull/94) in Ethereum
Classic repository.** Five editors were proposed, addressed by their
real names, and all of them agreed to join. This includes
[Afri](https://github.com/ethereumclassic/ECIPs/pull/94/files#diff-778b8d03b727e6dae8078a7778b5abf6R66),
who is also known by the handle `soc1c`. The real name of Afri
(`soc1c`), however, later turned out to be the point of the drama.

**On November 15th 2019, Afri [made an
attempt](https://github.com/ethereumclassic/ECIPs/pull/176) in PR#176
to add several EIPs in to one of the planned hard fork "Aztlan".** The
PR was put on hold by Yaz and me for several days, because at that
time not everyone agreed to add in those EIPs for the hard fork. In
fact, the specification added by Afri later turned out not to be the
adopted version. At that time, the hard fork was even not formally
discussed yet.

However, as Afri and Bob strongly pushed merging the PR, we later
[agreed on a
compromise](https://discordapp.com/channels/223674353001168906/552567121046011905/644834611888914432)
-- add several [alternative
ECIPs](https://github.com/ethereumclassic/ECIPs/pull/184) for Aztlan,
so that different options can be discussed clearly.

**On November 21st 2019, Afri [made an
attempt](https://github.com/ethereumclassic/ECIPs/pull/194) in PR#194
to move one of his other proposals ECBP-1076 into Active status.** In
my opinion, this PR was problematic in several ways, so I submitted a
"request changes" review:

* There were still issues unaddressed in the draft
  specification. ECBP-1076 was indeed discussed in a previous
  meeting. Although I was not able to join, prior to that meeting,
  people (including me) wrote some concerns related to the
  specification in Github issues, and I couldn't find them
  addressed. Based on my experience with Ethereum's AllCoreDevs, I
  also find it quite unusual to propose a proposal for the first time
  and accept a proposal in the same meeting.
* The move to "Active" status was unheard of and potentially unfit for
  the ECIP process. ECBP corresponds to Ethereum's ERC
  specifications. Specifications in this category usually goes from
  "Draft" into "Last Call" and then to "Final", but not "Active"
  status.
  
Afri, however, did not look like willing to discuss those
concerns. The review was dismissed by Afri citing [80 minute call and
rough
consensus](https://github.com/ethereumclassic/ECIPs/pull/194#event-2820506630). Immediately
after that, he [made an
attempt](https://github.com/ethereumclassic/ECIPs/pull/196) in PR#196
to remove me from ECIP-1000. Both PR#194 and PR#196 were later closed.

This was the first time when someone tried to resolve conflicts by
dismissing another person's objection, and by attempting to exclude
people from the process. As readers will soon learn below, it later
happened again. Fortunately both of those attempts failed.

**On November 27th 2019, Afri [made an
attempt](https://github.com/ethereumclassic/ECIPs/pull/199) in PR#199
to move Aztlan hard fork into Last Call status.** This is when the air
went hot. The initial dispute was on the ECIP number -- as we couldn't
figure out whether the specification we actually accepted in the
meeting was ECIP-1061 or ECIP-1072, to which I submitted a "request
changes" review.

Afri, again, did not look like willing to discuss the issue. The
review was quickly dismissed by Afri citing it's
["resolved"](https://github.com/ethereumclassic/ECIPs/pull/199#event-2837816513)
without any further explanations.

Afri's action resulted in lengthy discussions about this
issue. Irritated by Afri's repeated dismiss of other people's
objections, I
[submitted](https://github.com/ethereumclassic/ECIPs/pull/220)
"irregular process transitons" in PR#220.

In addition, I also raised my
[concern](https://github.com/ethereumclassic/ECIPs/pull/220#issuecomment-561376817)
whether the hard fork actually got enough technical reviews so that it
is safe for Ethereum Classic. Yaz, at that time who were supporting
ECIP-1061,
[replied](https://github.com/ethereumclassic/ECIPs/pull/220#issuecomment-561397891)
me with the following comments:

> You can ask me about the safety properties of the hardfork, but
> you're just changing the subject to show off how much you know about
> the technical details of the hardfork in question ... Stick to the
> subject matter.

Another main argument from Afri and Yaz was that there should only be
one ECIP for a single hard fork.

**On November 29th 2019, realized that I could not get people in ECIP
process to discuss the technical aspects of the hard fork, I [posted a
message](https://twitter.com/sorpaas/status/1200492354819543046) on
Twitter**. I made it clear that I do not think Aztlan is a good hard
fork and may contain flaws.

**Around December 2019 to January 2020, the topic suddenly shifted by
Bob, claiming that in ECIP-1000 I used the real name of `soc1c`, and
that was "doxxing" and "against CoC".** On January 20th 2020, Bob submitted
[PR#267](https://github.com/ethereumclassic/ECIPs/pull/267) to remove
the real name of `soc1c` from ECIP-1000.

Bob's claim of "doxxing" was quite loud at that time, but it really is
quite absurd to me, because not only was the editor list already
merged 6 months ago (which everyone agreed on, including `soc1c`, as
explained in the beginning of this timeline), but also `soc1c`'s real
name has been well-known in the community, to the point that even
`soc1c` himself [uses his real name
frequently](https://github.com/ethereumclassic/ECIPs/issues/174#issuecomment-557106181)
before the controversy happened. As `MiKo`, the ETC Discord
administrator, has put it:

> From my perspective, just being on calls in discord. There was
> always a connection of `soc1c` === Afri through the public
> conversations here. IIRC there was a push to try and keep his name
> out of association with ETC early on, but as I recollect, we always
> knew Afri === `soc1c`.

**On December 20th 2019, although I was still objecting Aztlan hard
fork, believing Bob and Afri had made it as community consensus, I
[implemented](https://github.com/multi-geth/multi-geth/commit/37c806fad772f421dc8cb753cb5cae88fc991e64)
it in MultiGeth.** After the implementation is finalized, I suddenly
realized there may be some issues in EIP-1884 of Aztlan, so I did some
digging on the same day, and [found several
issues](https://corepaper.org/ethereum/fork/istanbul/#_ethereum_classic),
raising them to the community.

**During January and February, several additional issues of Aztlan
were found.** Those issues also caused testnets Kotti and Mordor to
break for several weeks.

**On January 24th 2020, Donald submitted ECIP-0001 as the second
attempt to remove me from ECIP process.** One of the main reason was
the "doxxing" argument, claiming I was "abusing the process".

**On February 20th 2020, Yaz accused me of "implementing the flawed
Aztlan specification in MultiGeth and OpenEthereum".** I find the
accusation quite absurd, because from what actually happened to me, I
discovered the specification flaws through implementations. I wrote a
tweet thread as
[explanation](https://twitter.com/sorpaas/status/1231104348094189569). I
[also wrote some
posts](https://twitter.com/sorpaas/status/1231197997557583872) on what
I think those accusations are all about.

**On February 24th 2020, Afri posted
[PR#299](https://github.com/ethereumclassic/ECIPs/pull/299) and
[PR#300](https://github.com/ethereumclassic/ECIPs/pull/300) as two new
options for the hard fork.** To me, one interesting aspect of this is
that two option EIPs are posted, yet during Aztlan drama one of the
main argument from Afri was "only one EIP per hard fork".

**On February 26th 2020, Aztlan hard fork was cancelled. Phoenix (new)
hard fork was the replacement.**

**On March 18th 2020, Donald submitted
[PR#313](https://github.com/ethereumclassic/ECIPs/pull/313)
withdrawing his attempt to remove me from ECIP process.** It was cited
that there were not enough consensus.

**On April 1st 2020, Afri wrote a
[tweet](https://twitter.com/a4fri/status/1245404388736282624) publicly
revealing that the handle behind `q9f` is also Afri.**

## Appendix: Lessons learned

### Restrict people who can dismiss reviews

Github has the protected branch feature, which restricts a bunch of
things. This also includes who can dismiss reviews. If we had that
protection in ECIP repository, `soc1c` wouldn't be able to casually
hit the "dismiss" button multiple times, and we may be able to have a
more proper conflict resolution without those controversies.

### Keep names out of specifications

Having named ECIP editors and named ECIP authors may not be a good
idea. After all, Ethereum Classic is a decentralized community, and
those names gives people false sense of power and authority. A simple
change like removing the `author` field in specification and only keep
it in "Copyright" section may move the process a long way forward.

### MultiGeth project

Unfortunately, it's no doubt that the drama has caused ECIP process to
lose a considerable amount of reputation. In the future, talking about
the [MultiGeth](https://github.com/multi-geth/multi-geth) project, we
will only take ECIP as reference for a section of the Ethereum Classic
community. Instead, there will be a separate MultiGeth RFCs process to
decide how potentially controversial changes are merged into the
codebase.

## Appendix: FAQ

**Have you blocked attempts to withdraw/deactivate ECIP-1061?**

No. I was always in the position of not supporting ECIP-1061, because
its lack of reviews and bypassing the process. In the mean time, I did
respect community consensus, and thus implemented ECIP-1061 in Parity
Ethereum and MultiGeth. I only blocked attempts to move ECIP-1061 back
to draft and enact the same specification again, because that's an
unusual path of ECIP-1000 process (and thus should not be done unless
in extreme situations). In fact, if we had withdrawn/deactivated
ECIP-1061, Ethereum Classic would have been in a much better position
right now.

**Aren't you the author/co-author of both ECIP-1061 and ECIP-1072?**

Yes. This is what really makes things ironic that the specification
author's view to not support it and not move it forward being
dismissed.
