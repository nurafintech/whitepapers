## Introduction

![](https://polkadot.network/assets/img/dg-network-xl-2.svg?v=9c111bcf61)

فرض کنیم برای ایده ای ناب و جدید به یک بلاکچین مجزا نیاز داشته باشیم. برای توسعه و پیاده سازی، باید قبل از پر و بال دادن به ایده اولیه، باید به فکر پیاده سازی بلاکچین مربوطه باشیم که در آن صورت ناچارا زمان و هزینه بسیاری را صرف پیاده سازی بلاکچین کرده و سپس به سراغ ایده اصلی میرویم.

این مشکل اصلی بسیاری از نوآوران صنعت بلاکچین میباشد. پلتفرم پلکادات دقیقا به حل این مشکل پرداخته است، به این صورت که با بلاکچین اصلی خود یعنی relay chain اجازه ساخت بلاکچین های جانبی را حول محور خود میدهد که این بلاکچین های مربوطه امنیت مورد نیاز خود را برای بلاک های جدید ساخته شده، از relay chain تامین کرده و افرادی که اجازه استفاده از این بلاکچین های جانبی را دارند، دیگر بدون نیاز به فکر کردن درباره پیاده سازی بلاکچین مربوطه، به بسط دادن ایده و پیاده سازی لاجیک و منطق خود بر روی بلاکچین های جانبی خواهند پرداخت.
<br>

#

## Parachains explained
![](https://miro.medium.com/max/1400/1*PZwxym95YvDfSXUWixCJQg.jpeg)

Parachains are next-generation layer-1 blockchains that put the 'multi' in multichain, forming the backbone of the Polkadot network and creating a free alliance of sovereign chains. Polkadot is the layer-0 protocol that underlies and supports this network of layer-1 parachains. Polkadot’s cross-chain interoperability allows any type of data or asset to be sent between parachains, creating a new paradigm of interchain services, communities, and economies.

**The parachain model brings scalability to blockchain technology in a more decentralized and trustless way than relying purely on layer-2 scaling solutions.** Transactions are spread across the network, taking place 'in-parallel' or simultaneously on several blockchains secured by a single set of decentralized validators.


#

## The main benefits of parachains

A parachain (parallelizable chain) is a simpler form of blockchain, which attaches to the security provided by a “relay chain” rather than providing its own. The relay chain is called that because it not only lends security to attached parachains, but also provides a guarantee of secure message-passing between them. One key feature of parachains is that the computations they perform are inherently independent. Fully generalized systems of turing-complete smart contracts run into issues in determining which transactions will “collide” with each other, meaning that transactions which could potentially be parallelized are often run in sequence, wasting valuable computation time. **Drawing clear boundaries between parachains means that we can execute all of them at once without fear of collision — if we have 10 parachains, we can perform 10 times the work using the same source of security.**

## Specialization
Parachains can be specialized for virtually every blockchain use case, and also represent a tool for experimenting with completely new use cases, especially on Kusama. Thanks to this specialization, parachains can do more working together than any single chain can do alone, creating a rich ecosystem where new decentralized economies can flourish.
#
 هر پاراچین که در واقع خود یک بلاکچین جداگانه میباشد را برای یک ایده و کار خاص optimize میکنیم.
#

## Flexibility

Polkadot gives parachain developers the maximum possible flexibility when building their chain. The only technical requirement for being a parachain is that it must be able to prove to Polkadot validators that every block of the parachain follows the agreed-upon protocol. Beyond that, the sky's the limit for designing the perfect chain for any particular use case or set of use cases.

Building a parachain also gives blockchain developers much more flexibility than if they were building on top of a smart contract platform. When building at the smart contract layer, developers are locked into the design decisions of the underlying blockchain, which may not be optimal for their use case. Polkadot allows developers to drill down into the logic of the layer-1 parachain itself, unlocking far more possibilities for optimization.
#
   دست توسعه دهندگان برای کانفیگ پاراچین ها باز میباشد.
#

## Interoperability
A key aspect of the parachain model is the ability for blockchains of differing design to communicate with each other. Polkadot's interoperability, also known as cross-chain composability, means blockchains are no longer isolated islands closed off from each other. Parachains end the era of siloed blockchains, creating a decentralized, connected internet of blockchains where before there existed only isolated networks with their own tribalistic communities.<br/>

Crucially, Polkadot allows parachains to send not only tokens but any type of data between each other, opening up a host of new blockchain use cases. Polkadot developers can build services that take advantage of the features of multiple blockchains, rather than being limited to the features of any one chain.
#
 تمامی پاراچین ها که از طریق Relay chain  امنیت شان برقرار میشود، میتوانند با یکدیگر ارتباط برقرار کرده و message passing داشته باشند. بدین ترتیب کل پلتفرم پلکادات interoperable خواهد بود.
#

## Scalability
With the parachain model, Polkadot achieves scalability at layer-1, which is more decentralized and efficient than relying purely on layer 2. However, parachains can also incorporate layer-2 solutions, further increasing scalability. Polkadot allows transactions to be spread out and processed in parallel over an ecosystem of specialized layer-1 blockchains, significantly improving throughput and scalability over non-sharded networks.<br/>

In addition, several optimizations have been proposed that will allow Polkadot to continue improving scalability and transaction throughput into the future, while maintaining decentralization, security, and data availability. The last point is important, as other networks may prioritize TPS (transactions per second) at the expense of these important factors, but sacrificing decentralization for throughput defeats the underlying purpose of Web3.

## Freedom from platform fees

Parachains connected to Polkadot can access as much computing power as they need without additional fees or “gas” costs. Polkadot's flexibility frees parachain teams and dapp developers to implement whatever fee structure they want for their users.<br/>

Best of all, users of parachains are not required to hold DOT tokens to interact with apps and services, and indeed don't even need to know that they're interacting with a blockchain. In this sense, the parachain model allows blockchain technology to overcome a significant barrier to usability and adoption that exists with legacy networks.

## Security

New blockchains typically need to bootstrap their own security by building a network of validators or miners. This is an incredibly difficult and time consuming process, and many blockchains are left with a level of security that leaves them vulnerable to attacks.<br/>

Parachains get robust security automatically when connecting to Polkadot. This built-in security feature, also called shared security, provides newer blockchain teams with bank-like security at minimal effort on their part. It also gives them fewer barriers to entry and significantly reduces the time necessary to launch a new network.

## Upgradability
We live in a world of constant innovation, where technology is advanced one day and out of date the next. Like all software, blockchains need periodic updates to add new features, fix bugs, and incorporate more advanced technologies as they become available. But upgrading conventional blockchains is a laborious process often involving ‘forking’ or splitting the chain, which slows innovation and sometimes rips communities apart.

Polkadot and its parachains can take advantage of easier, 'forkless' upgrades. This means parachains can be upgraded easily based on the will of their communities — so they can be ready for whatever the future holds. With the parachain model, blockchains can better evolve and adapt to changing conditions, which means they can continue to be relevant into the future as new technologies become available.

### Independent, customizable governance
Parachains on Polkadot are free to adopt whatever governance model they see fit, and can access a number of pre-built modules for implementing various on-chain governance systems. The ability to access sophisticated on-chain governance mechanisms allows teams to significantly reduce the likelihood of hard forks of their chain that could risk splitting their communities in two.

On-chain governance also provides a means of accountable transparency for parachain communities, a prerequisite for many institutions and fiduciaries that often need to see clear decision making processes before getting involved in blockchain technology. When coupled with Polkadot's forkless upgrades feature, a robust system of governance allows parachains to maintain their leading edge while also promoting cohesion in their communities and ensuring all stakeholders have a say in the future of the network.

### Financial agency

Parachains can also leverage on-chain treasuries to gain financial agency, acting autonomously to fund activities based on the will of their communities. Coupled with on-chain governance, treasuries allow parachain communities to easily take on the form of a DAO (decentralized autonomous organisation).

This opens the door to new decentralized funding models, from funding projects that are beneficial to the network, to decentralized philanthropy, decentralized sovereign wealth funds, and even cross-chain mergers and acquisitions. The parachain model thus gives blockchains the ability to 'act in the world' on a financial basis, something once reserved for centralized institutions and corporations.

### Ease of development

Ultimately, the benefits above would have limited impact if developing a parachain was a prohibitively difficult process. But parachain development teams benefit from a wide array of development tools that make building a blockchain easier than it has ever been.

Substrate, a blockchain development framework built by Parity Technologies, is the primary Polkadot parachain SDK, helping teams significantly reduce the time and complexity of building a parachain. With Substrate, developers can take advantage of pre-built modules for common blockchain components that can be mixed and matched like blockchain building blocks to create the custom parachain best suited for their use case.

#

## The many forms of parachains

![](https://polkadot.network/content/images/size/w1000/2021/12/Parachains-value-prop---types--1-.png)

Since Polkadot gives parachain teams maximum flexibility to design the network that best suits their vision, parachains can and do take on a multitude of different forms, including:

* **Independent token economies**: Parachains with their own native tokens, fee structures, and economic ecosystems.
* **Parachain hubs**: Parachains that provide a range of functionality to serve a broader community or use case, such as DeFi hubs and governance hubs.
* **Smart contract platforms**: Platforms for building and hosting smart contract based dapps and services, with support for Wasm-VM, EVM, and other types of virtual machines.
* **Common good parachains**: Designed for the benefit of the entire Polkadot ecosystem, common good chains are approved by governance and operate on a non-profit basis, typically using Polkadot’s native token, DOT.
* **Bridges**: Bridges allow Polkadot parachains and dapps to connect to external networks like Kusama, Bitcoin, and Ethereum.
* **Parathreads**: Pay-as-you-go parachains for early stage networks and those that don’t need continuous connectivity to Polkadot. Parathreads are a proposed feature that will need to be added by Polkadot governance once developed.

## Parachain slot auctions and crowdloans
Parachains connect to Polkadot by leasing an open slot on the Relay Chain via auction, which involves locking up a bond of DOT for the duration of the lease. DOT holders can help their favorite parachains win an auction, potentially earning a reward in return, by contributing to a crowdloan and temporarily locking their own DOT for the parachain’s bond.

**Auctions and crowdloans raise the bar for blockchain projects, incentivizing them to demonstrate their technology and gain community support prior to launch. This reduces the likelihood of so-called ‘vaporware’ projects that raise funds without the intention or technical ability to deliver on their promises.** Crowdloans also represent a fairer, more community-driven way of bootstrapping a native token in a decentralized way.

## The cost of running a parachain
Parachains connected to Polkadot by leasing a parachain slot can access as much computing power as they need without additional fees or “gas” costs. Since the full amount of DOT bonded by a team for a parachain slot is unlocked at the end of the lease period, the cost of running a parachain is best described as the opportunity cost from not having access to the locked DOT for the duration of the lease.<br/>

Teams that choose to fund their slot via crowdloan may choose to reward their contributors in any way they see fit, representing an additional cost. Other minor costs include the expense of running collator nodes on the individual parachain.

**For applications with a lot of users and traffic, running on Polkadot as a parachain is expected to be more economical than running as a solo blockchain or building on an existing smart contract platform.**

#

هر تیمی که بخواهد برای پروژه خود، پاراچین دریافت کند، باید مقداری توکن بومی پلکادات، یعنی دات در شبکه به گرو بگذارد. همچنین اگر توکن داران دات، علاقه مند به این تیم و پروژه آن ها باشند، باید از دات های خود برای رای دادن به این پروژه استفاده کنند. بدین ترتیب برای شبکه پلکادات و توکن آن، استفاده ای واقعی و روزمره ایجاد شده است و این دهنده ارزشمند بودن توکن دات نیز میباشد.
#

## Parachain Slot Acquisition
Polkadot supports a limited number of parachains, currently estimated to be about 100. As the number of slots is limited, there are several ways to allocate them:

* Governance granted parachains, or "common good" parachains
* Auction granted parachains
* Parathreads

    **"Common Good"** parachains are allocated by Polkadot's on-chain governance system, and are deemed as a "common good" for the network, such as bridges to other networks or chains. They are usually considered system-level chains or public utility chains. These typically do not have an economic model and help remove transactions from the Relay Chain, allowing for more efficient parachain processing.

    **Auction granted parachains** are granted in a permissionless auction. Parachain teams can either bid with their own DOT tokens, or source them from the community using the crowdloan functionality .

    **Parathreads** have the same API as parachains, but are scheduled for execution on a pay-as-you-go basis with an auction for each block.

## Slot Expiration
When a parachain wins an auction, the tokens that it bids get reserved until the lease's end. Reserved balances are non-transferrable and cannot be used for staking. At the end of the lease, the tokens are unreserved. Parachains that have not secured a new lease to extend their slot will automatically become parathreads.

## Examples
### Some examples of parachains:

* Encrypted Consortium Chains: These are possibly private chains that do not leak any information to the public, but still can be interacted with trustlessly due to the nature of the XCMP protocol.
* High-Frequency Chains: These are chains that can compute many transactions in a short amount of time by taking certain trade-offs or making optimizations.
* Privacy Chains: These are chains that do not leak any information to the public through use of novel cryptography.
* Smart Contract Chains: These are chains that can have additional logic implemented on them through the deployment of code known as smart contracts.

#

## Sharding: Scaling By Subset Selection

**The goal of sharding is to improve throughput by splitting work, in the form of transactions, across many chains known as shards.** The shards are referenced by and secured by a top-level blockchain. **In Polkadot the top-level blockchain is called the relay chain and the shards are parachains.** Most of the data that appears on the relay chain are transactions that include references to new parachain blocks, which makes processing any fork of the relay chain itself cheap.


![](https://polkadot.network/content/images/size/w1000/2022/01/Relay-Chain.png) <br>

Sharding is only an improvement to scalability if each validator only needs to check some of the submitted parachain blocks, as opposed to all of them. If there were 10 parachains, and each validator had to check all blocks from all 10 chains, we might as well just put all of the transactions onto one blockchain and call it a day. **The trick is to find a way for each validator to do as little verification work as possible while still maintaining economic security:** that validators who advocate for bad parachain blocks are economically disincentivized from doing so. More concretely, it should be impossible for an adversarial group of validators to collude to get a bad parachain block included in the finalized relay chain before losing all of their stake to slashing. Validators, and indeed small subsets of validators, can collude to get bad parachain blocks referenced by unfinalized forks of the relay chain, but we guarantee that these forks are ignored before finality and the offenders are slashed.

Let’s set down some concrete assumptions about the adversary that we defend against:
* The adversary can control up to 1/3 of all validators, and can control all of these validators to behave exactly as desired.
* The adversary can view all network messages between honest validators and the validators it controls
* The adversary can DoS up to X% of the validators at any time, preventing them from sending or receiving messages.
* It takes a fixed delay before the adversary can begin to DoS any validator

#

## Parachain consensus

The base unit of parachain consensus isn't actually a parachain, but something that we call an **availability core** or **core** for short. **These are something like CPU cores: they operate in parallel, and have work scheduled onto them in discrete time-slots.** Each parachain has its own dedicated core, which means that it's always scheduled onto a particular core. However, we can also multiplex multiple chains onto a single core. The only difference is the scheduling algorithm.

Cores serve as an effective description of the throughput of the relay chain. Cores directly correspond to the amount of work validators need to do. Each core can handle up to one parachain block per each relay-chain block, at peak.

In any sharded blockchain system, where only some validators check each parachain block, data availability is a crucial component to make sure that the data necessary to check a parachain block can be recovered for the purposes of fraud detection. <br>
Availability cores are managed by the relay chain and track which parachain blocks are pending data availability. **The main purpose of availability cores is as a scheduling primitive and to provide backpressure when data availability is slower than usual.**

The logic of an availability core looks like this. Cores are empty when they're ready to accept a new parachain block, at which point they become occupied. Then, the data either becomes available or the availability process times out. At that point, the core becomes empty again.

![](https://polkadot.network/content/images/size/w1000/2022/01/Availability-Core-Logic.png)

It's helpful to divide parachain consensus up into 5 distinct protocols that are intertwined in relay-chain consensus:
1. **Collation** is the process by which parachain blocks are created. Collators build a parachain block and send it to validators.
2. **Backing** is the process by which parachain blocks are initially checked by a small group of relay-chain validators and registered on the relay chain. The main byproduct of backing is that it requires validators to put themselves at risk if the later protocols fail.
3. **Availability** is the process by which the backing validators distribute pieces of the data necessary to check the parachain block and ensure it is available to check later.
4. **Approval** Checking is the process by which random validators recover the data and execute the parachain block. They either approve or initiate a dispute based on whether they think the parachain block is valid.
5. **Disputes** are the process by which conflicting opinions by validators on a parachain block are resolved and bad parachain blocks are ignored and offenders punished. Disputes only exist as a failsafe and aren't expected to be triggered often.

Note that validators are likely to be engaging in each of these protocols at the same time, and often multiple instantiations of them. For example, a validator might be engaging in approval-voting for a parachain block that's further down the pipeline at the same time as it participates in backing for a newer block and disputes for an even older block.

This internal parallelism also reflects the architecture of the implementation: each of these protocols is implemented as an independent subsystem, and all the subsystems run in parallel. Every node is always doing a little bit of everything.

#
Due to their parallel nature, they are able to parallelize transaction processing and achieve scalability of the Polkadot system. They share in the security of the entire network and can communicate with other parachains through the XCM format.<br/>

Parachains are maintained by a network maintainer known as a collator. The role of the collator node is to maintain a full node of the parachain, retain all necessary information of the parachain, and produce new block candidates to pass to the Relay Chain validators for verification and inclusion in the shared state of Polkadot . The incentivization of a collator node is an implementation detail of the parachain. They are not required to be staked on the Relay Chain or own the native token unless stipulated by the parachain implementation.<br/>

The Polkadot Host (PH) requires that the state transitions performed on parachains be specified as a Wasm executable. Proofs of new state transitions that occur on a parachain must be validated against the registered state transition function (STF) that is stored on the Relay Chain by the validators before Polkadot acknowledges a state transition has occurred on a parachain. The key constraint regarding the logic of a parachain is that it must be verifiable by the Relay Chain validators. Verification most commonly takes the form of a bundled proof of a state transition known as a Proof-of-Verification (PoV) block, which is submitted to the validators from one or more of the parachain collators to be checked.<br/>

The below diagram or similar ones are distributed widely over the internet. They show how validators are split into groups and assigned to parachains and get parachain block proposals from collators.<br/>

![](https://raw.githubusercontent.com/nurafintech/whitepapers/main/Polkadot/Polkadot%20Architecture.png)

![](https://raw.githubusercontent.com/nurafintech/whitepapers/main/Polkadot/Polkadot%20Consensus%20Roles.png)


## Parachain Economies
Parachains may have their own economies with their own native tokens. Schemes such as Proof-of-Stake are usually used to select the validator set to handle validation and finalization; parachains will not be required to do either of those things. However, since Polkadot is not overly particular about what the parachain can implement, it may be the choice of the parachain to implement a staking token, but it's not generally necessary.

Collators may be incentivized through inflation of a native parachain token. There may be other ways to incentivize the collator nodes that do not involve inflating the native parachain token.

Transaction fees in a native parachain token can also be an implementation choice of parachains. Polkadot makes no hard and fast rules for how the parachains decide on original validity of transactions. For example, a parachain may be implemented so that transactions must pay a minimum fee to collators to be valid. The Relay Chain will enforce this validity. Similarly, a parachain could not include that in their implementation, and Polkadot would still enforce its validity.

Parachains are not required to have their own token. If they do, is up to the parachain to make the economic case for their token, not Polkadot.


## Parachain Hubs
While Polkadot enables crosschain functionality amongst the parachains, it necessitates that there is some latency between the dispatch of a message from one parachain until the destination parachain receives the message. **In the optimistic scenario, the latency for this message should be at least two blocks - one block for the message to be dispatched and one block for the receiving parachain to process and produce a block that acts upon the message.** However, in some cases, we may see that the latency for messages is higher if many messages are in queue to be processed or if no nodes are running both of the parachain networks that can quickly gossip the message across the networks.

**Due to the necessary latency involved in sending crosschain messages, some parachains plan to become hubs for an entire industry**. For example, a parachain project **Acala** is planning to become a hub for decentralized finance (DeFi) applications. Many DeFi applications take advantage of a property known as composability which means that functions of one application can be synergistically composed with others to create new applications. One example of this includes flash loans, which borrow funds to execute some on-chain logic as long as the loan is repaid at the end of the transaction.

#
An issue with crosschain latency means that composability property weakens among parachains compared to a single blockchain. This implication is common to all sharded blockchain designs, including Polkadot, Eth2.0, and others. The solution to this is the introduction of parachain hubs, which maintain the stronger property of single block composability.

#

## Parathreads
![](https://miro.medium.com/max/1400/1*EFqF3Y-yF8yRX7oNtzavKA.png)
Parathreads are an idea for parachains to temporarily participate (on a block by block basis) in Polkadot security without needing to lease a dedicated parachain slot. This is done through economically sharing the scarce resource of a parachain slot among several competing resources (parathreads). Chains that otherwise would not be able to acquire a full parachain slot or do not find it economically sensible to do so, are enabled to participate in Polkadot's shared security — albeit with an associated fee per executed block. It also offers a graceful off-ramp to parachains that no longer require a dedicated parachain slot, but would like to continue using the Relay Chain.

## Origin
Since computers have a limited amount of physical memory, when an application needs more, the computer can create virtual memory by using swap space on a hard disk. Swap space allows the capacity of a computer's memory to expand and for more processes to run concurrently with the trade-off that some processes will take longer to progress.


## How do Parathreads Operate?
A portion of the parachain slots on the Relay Chain will be designated as part of the parathread pool. In other words, some parachain slots will have no parachain attached to them and rather will be used as a space for which the winner(s) of the block-by-block parathread fee auction can have their block candidate included.<br/>

Collators will offer a bid designated in DOT for inclusion of a parathread block candidate. The Relay Chain block author is able to select from these bids to include a parathread block. The obvious incentive is for them to accept the block candidate with the highest bid, which would bring them the most profit. The tokens from the parathread bids will likely be split 80-20, meaning that 80% goes into Polkadot treasury and 20% goes to the block author. This is the same split that applies also to transaction fees and, like many other parameters in Polkadot, can be changed through a governance mechanism.

![](https://miro.medium.com/max/1400/1*Zge-m0Ot81ckvoWpzduZSA.png)

## Parachain vs. Parathread
![](https://miro.medium.com/max/1400/1*lfGWA25QixsjffC-FWhlLg.png)
Parachains and parathreads are very similar from a development perspective. **One can imagine that a chain developed with Substrate can at different points in its lifetime assume one of three states: an independent chain with secured bridge, a parachain, or a parathread.** It can switch between these last two states with relatively minimal effort since the difference is more of an economic distinction than a technological one.

Parathreads have the exact same benefits for connecting to Polkadot that a full parachain has. Namely, it is able to send messages to other para-objects through XCMP and it is secured under the full economic security of Polkadot's validator set.

The difference between parachains and parathreads is economic. Parachains must be registered through a normal means of Polkadot, i.e. governance proposal or parachain slot auction. Parathreads have a fixed fee for registration that would realistically be much lower than the cost of acquiring a parachain slot. Similar to how DOT are locked for the duration of parachain slots and then returned to the winner of the auction, the deposit for a parathread will be returned to the parathread after the conclusion of its term.

Registration of the parathread does not guarantee anything more than the registration of the parathread code to the Polkadot Relay Chain. When a parathread progresses by producing a new block, there is a fee that must be paid in order to participate in a per-block auction for inclusion in the verification of the next Relay Chain block. All parathreads that are registered are competing in this auction for their parathread to be included for progression.

There are two interesting observations to make about parathreads. Since they compete on a per-block basis, it is similar to how transactions are included in Bitcoin or Ethereum. A similar fee market will likely develop, which means that busier times will drive the price of parathread inclusion up, while times of low activity will require lower fees. Two, this mechanism is markedly different from the parachain mechanism, which guarantees inclusion as long as a parachain slot is held; parathread registration grants no such right to the parathread.

## Parathread Economics
There are two sources of compensation for collators:

1. Assuming a parathread has its own local token system, it pays the collators from the transaction fees in its local token. If the parathread does not implement a local token, or its local token has no value (e.g. it is used only for governance), then it can use DOT to incentivize collators.
2. Parathread protocol subsidy. A parathread can mint new tokens in order to provide additional incentives for the collator. Probably, the amount of local tokens to mint for the parathread would be a function of time, the more time that passes between parathread blocks that are included in the Relay Chain, the more tokens the parathread is willing to subsidize in order to be considered for inclusion. The exact implementation of this minting process could be through local parathread inflation or via a stockpile of funds like a treasury.

Collators may be paid in local parathread currency. However, the Relay Chain transacts with the Polkadot native currency only. Collators must then submit block candidates with an associated bid in DOT .

## Parachain Slot Swaps
It will be possible for a parachain that holds a parachain slot to swap this slot with a parathread so that the parathread "upgrades" to a full parachain and the parachain becomes a parathread. The chain can also stop being a chain and continue as a thread without swapping the slot. The slot, if unoccupied, would be auctioned off in the next auction period.

This provides a graceful off-ramp for parachains that have reached the end of their lease and do not have sufficient usage to justify renewal; they can remain registered on the Relay Chain but only produce new blocks when they need to.
<br/>

Parathreads help ease the sharp stop of the parachain slot term by allowing parachains that are still doing something useful to produce blocks, even if it is no longer economically viable to rent a parachain slot.

![](https://miro.medium.com/max/1400/1*uYZgrixc8ek19mZvUA_Mzw.png)



## References
* https://polkadot.network/Polkadot-lightpaper.pdf
* https://polkadot.network/blog/polkadot-v1-0-sharding-and-economic-security/
* https://polkadot.network/blog/the-parachain-advantage-exploring-polkadots-next-generation-model/
* https://wiki.polkadot.network/docs/learn-parachains 
* https://wiki.polkadot.network/docs/learn-parathreads