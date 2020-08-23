---
title: Choosing mining algorithms
subtitle: Three criteria for Proof of Work mining algorithm selection.
---

Recently, there is a discussion in Ethereum Classic community on
changing the currently-used mining algorithm, Ethash. It resulted in
some controversial debate among the community members on whether the
change is approriate, and what will be the criteria for choosing the
new algorithm.

Still up till today, how mining algorithms are chosen, and how
evaluations should be done remain largely unexplored, with only
various small pieces of information clattered in the Internet. Below,
we try to provide three basic categorization of selection criteria for
chooing a mining algorithm. Hopefully, this can be a small step
forward in improving our vocabulary when we talk about mining
algorithm selection, and can provide some further ideas to the
Ethereum Classic community for the ongoing discussion.

## Soundness

In this section, we talk about **safety** of a mining algorithm. Two
important properties must be satisfied in order for an algorithm to be
considered a sound choice for mining:

* **Uniformity**: A good mining algorithm should produce roughly
  uniform distribution for its output range. This is mostly due to how
  **difficulty** calculation works in Proof of Work -- the probability
  of generating a specific output is calculated and then used to
  derive how much work should be put in producing the next block. If a
  mining algorithm does not have uniformity, then the difficulty
  calculated becomes unrealiable.
* **Pre-image resistance**: This makes sure the algorithm is a
  *one-way function*. This ensures that miners cannot cheat when
  producing work.
  
The above two properties are shared with hashing algorithms. However,
mining algorithms and hashing algorithms do not have the same strong
safety requirements. Mining algorithms safety requirement is slightly
relaxed, in that it's nice to have, but not the end of the world, if
*second pre-image resistance* and *collision resistance* is violated.

## Deliberation

Public blockchains are permisionless. Everyone is free to join, and
free to leave at any moment. Miners as well. Because of this, one
thing for Proof of Work is that we must ensure **mining is a
deliberate action**. In order for the honest majority assumption to be
satisfied, miners must be aware that they are mining, and miners must
be aware that they are actively spending their own resources.

Below we discuss two examples of the opposite of deliberation.

* **Botnets**: Those are attacker-controlled computation resources,
  such as vulnerable laptops, servers, IoT devices, or even
  routers.
* **Browser-based mining**: Those are usually WebAssembly based binary
  running when a user visits a particular website. The binary then
  execute in the background, without awareness of the user.
  
Those two scenarios are examples where the owners of the hardwares do
not aware that they are participating in blockchain mining, and do not
aware that they are spending resources. It is easy to see why in
scenarios like this honest majority assumption can be easily violated.

*Deliberation* has been an issue that many mining algorithms have been
trackling. Common methods includes:

* **Memory-hard mining algorithms**: In those algorithms, to
  efficiently participate in mining, miners are required to allocate a
  considerable amount of memory. This makes botnets and browser-based
  mining impractical. Even if the attacker managed to initiate the
  mining process, the large amount of resources consumed can be easily
  noticed by the device owner.
* **ASICs with massive efficiency improvements**: The current most
  notable example of this is Bitcoin. Currently, ASICs are around 4
  million times more efficient in mining compared with a normal
  CPU. In this case, even if botnets or browser-based mining exist in
  large scale, it's hard to compete with a single mining farm.
  
## Availability

Availability refers to how easy or hard it is for miners to acquire
hardwares used for mining. Two entirely opposite approaches have been
adopted in Proof of Work blockchains for this issue:

* **ASIC resistance**: Some mining algorithms aim to be ASIC
  resistance. The goal is to make mining on general-purpose hardwares,
  such as CPUs or GPUs, to always be the most efficient. In this, the
  *availability* property is reached because miners can easily aquire
  or already own general-purpose hardwares.
* **ASIC friendly**: Other mining algorithms choose an entirely
  opposite approach. The goal is to encourage design and manufacture
  of ASICs.
  
Years of attempts from a large number of PoW blockchains have shown
that the availability issue is not a easy problem. On the ASIC
resistance side, ASICs emerges for algorithms originally for this
purpose, such as Ethash and Cryptonight. On the ASIC friendly side,
centralization of mining power and closed-door hardware design have
shown many issues, for example, Siacoin was forced to fork away due to
a closed-door hardware design from Bitmain, which led to
centralization issues.
