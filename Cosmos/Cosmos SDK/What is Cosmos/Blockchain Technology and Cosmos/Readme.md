# The First Blockchains

 Bitcoin introduced a novel consensus mechanism, now referred to as Nakamoto Consensus, that uses Proof-of-Work (PoW) to enable nodes to reach agreement in a decentralized network. It became possible to send online payments directly between parties independent of financial institutions and trusted third parties. Bitcoin became the first public, decentralized payment application.

Bitcoin uses PoW to achieve Byzantine Fault-Tolerance (BFT) which enables decentralized, trustless networks to function even with malfunctioning or malicious nodes present. It is best described as a cryptographic puzzle solved by a network node called a "miner". The puzzle is a task of pre-defined, arbitrary difficulty. At the current scale of the networks using PoW, the outcome is akin to a lottery with a single winning ticket, the successful miner node.

In most PoW systems, the task consists of a search for an unknown random number - a "nonce". To be a winning nonce, when it is combined with ordered transactions in a block the result is a hash value matching pre-defined criteria. Finding the nonce is evidence of considerable effort or work invested in the search. Each node uses its computing power in a race to solve the puzzle first and win the right to author the latest block.

Financial incentives are in play: the node that first announces a solution receives a reward. Through these rewards the network's native currency is issued and nodes are encouraged to invest computing power into solving the task. Network security scales with computing power; more investment leads to a more secure PoW network.

After the introduction of Bitcoin, several so-called "public chains" came into being, the first of which was Ethereum in 2013. These general-purpose blockchains aim to provide a decentralized network that allows the implementation of a variety of use cases.

* ![](https://tutorials.cosmos.network/resized-images/600/academy/1-what-is-cosmos/images/timeline.png)

Ethereum is a public blockchain with **smart contract functionality** that enables applications based on self-executing, self-enforcing, and self-verifying account holding objects. **It can be seen as a response to the difficulties of developing applications on Bitcoin.**

With Ethereum, the application layer of the chain took the form of a virtual machine called the **Ethereum Virtual Machine** (EVM). The EVM runs smart contracts, providing a single chain on which to deploy all sorts of programs. Despite its many benefits, the EVM is a **sandbox that delineates the range of implementable use case**s. Simplistic (and sometimes complex) use cases can be implemented with it but **are nonetheless limited regarding design and efficiency** by the **limitations** of the sandbox. Additionally, **developers are limited to programming languages that are tailored to the EVM.**

![](https://miro.medium.com/max/640/1*USoORgStbTqxcJrq_LmfIA.jpeg)

Even though the launch of Ethereum with its EVM was a big step forward, some issues of public, general-purpose blockchains remained: low flexibility for developers, and difficulties with speed, throughput, scalability, state finality, and sovereignty:

* speed:
    
    In the world of blockchains, "speed" means transaction speed. You can understand transaction speed as the time it takes to confirm a transaction. Speed is naturally impacted by the target delay between blocks, which is 10 minutes in Bitcoin and 15 seconds in Ethereum. Speed is also impacted by the backlog of equally worthy pending transactions all competing to be included in new blocks.

* Throughput:  describes how many transactions the network can handle per unit of time. Throughput can be limited for reasons of physical network bandwidth, computer resources, or even by decisions embedded in the protocol. Not all dApps have the same throughput requirements, but they all have to make do with the average resulting throughput of the platform itself if they are implemented on a general-purpose blockchain. This impacts the scalability of dApps.

* State finality: is an additional concern. Finality describes whether and when committed blocks with transactions can no longer be reverted/revoked. It is important to differentiate between probabilistic and absolute finality.

# More on State Finality

* Probabilistic finality:
    
     describes the finality of a transaction dependent on how probable reverting a block is, i.e. the probability of removing a transaction. The more blocks that come after the block containing a specific transaction, the less probable it is that a transaction may be reverted, as longest or heaviest chain rules apply in the case of forks.

* Absolute finality

    it is a trait of protocols based on Proof-of-Stake (PoS). Finality comes as soon as a transaction and block are verified. There are no scenarios in which a transaction can be revoked after it has been finalized.

* Finality in PoW and PoS networks:

    Proof-of-Stake (PoS) networks can have absolute finality because the total staked amount is known at all times. It takes a public transaction to stake, and another to unstake. If some majority of the stakers agree on a block, then the block can be considered "final" because there is no process that could overturn the consensus.

    This is different from PoW networks, where the total hashing capacity is unknown; it can only be estimated by a combination of the puzzle's difficulty and the speed at which new blocks are issued. Hashing capacity can be added or removed simply by turning machines on or off. When hashing capacity is removed too abruptly it results in a drop in the network transaction throughput, as blocks suddenly fail to be issued around the target interval.

    * For axample if you already have a pow blockchain with a samall network and not too many nodes, let's say a set malicious nodes can join to your network; they can continue to make blocks and suddenly they all together can propagate a duble-spended amount of coins in a block they create and propagate to the network, so the block that was created by one of your nodes can be discarded. ( 51% atack )
    The blocks are not Absolute final; in a PoS network, this is not possible if any new node that wants to join the network, should be validated by the amount of the coins it stakes.

# Governance on Ethereum
When developing on Ethereum, the developer needs to contend with two layers of governance:
The **chain's governance** and the **application's governance.** Independently of the dApp's governance needs, developers must come to terms with the underlying chain's governance.

Given the features of existing public blockchain projects and the requirements for privacy in certain industries, a push towards private, or managed, chains followed. Private distributed ledgers are blockchains with access barriers and sophisticated permission management. Examples include platforms for permissioned networks, such as R3's Corda and the Hyperledger Project's Hyperledger Fabric from the Linux Foundation.

The eventual development of more complex applications required a more flexible environment. This led to the launch of **multiple purpose-built/application-specific blockchains,** each providing a platform tailored to the necessities of use cases and applications. Each of these blockchains acted as self-contained environments limited by the use cases they were envisioned for.

**General-purpose chains are limited to simplistic use case applications, while application-specific chains only fit certain use cases.** This provokes the question, Is it possible to build a platform for all use cases that does away with the limitations of general-purpose chains?

# Internet of blockchains

The Cosmos Network is built using Tandermint.

![](https://miro.medium.com/max/640/1*TK54bxWDennWamJqPZW2xQ.jpeg)

![](https://miro.medium.com/max/720/1*Paylj0r4btusZoEZynI7Vg.jpeg)
![](https://miro.medium.com/max/720/1*3ArbFqJq5B95wbXDBMetGg.jpeg)

![](https://miro.medium.com/max/720/1*Bb3GoN3fILX-7hhd3zxWmQ.png)

Tendermint is a consensus algorithm with Byzantine Fault-Tolerance (BFT) and a consensus engine. It enables applications to be replicated in sync on many machines. Blockchain networks require BFT to ensure proper function even with malfunctioning or malicious nodes present. The result is known as **a Replicated State Machine with Byzantine Fault Tolerance**. It guarantees BFT properties for distributed systems and their applications.

It does this:

* **Securely** - Tendermint continues working even if up to **1/3rd** of machines fail or misbehave.
* **Consistently** - every machine computes the same state and accesses the same transaction log.
Tendermint is widely used across the industry and is the most mature BFT consensus engine for Proof-of-Stake (PoS) blockchains.

How is Cosmos an internet of blockchains? Cosmos is a network of interoperable blockchains, each implemented with different properties suitable for their individual use cases. Cosmos lets developers create blockchains that maintain sovereignty free from any "main chain" governance, have fast transaction processing, and are interoperable. With Cosmos, a multitude of use cases becomes feasible.


To achieve this type of network, the ecosystem relies on an open-source toolkit, including the Inter-Blockchain Communication Protocol (IBC) (opens new window), its implementation in the Cosmos SDK (opens new window), and Tendermint (opens new window)as the base layer providing distributed state finality. A set of modular, adaptable, and interchangeable tools helps not only to quickly create a blockchain but also facilitates the customization of secure and scalable chains.

The interoperable application blockchains on Cosmos are built with the Cosmos SDK. The Cosmos SDK includes the prerequisites that make it possible for created blockchains to participate in inter-chain communications using the Inter-Blockchain Communication Protocol (IBC). Chains built with the Cosmos SDK use the Tendermint consensus.

# How does Cosmos solve the scalability issue?
Scalability is a core challenge of blockchain technology. Cosmos allows applications to scale to millions of users. This degree of scalability is possible as Cosmos addresses two types of scalability:

* **Horizontal scalability**: 

    scaling by adding similar machines to the network. When "scaling out", the network can accept more nodes to participate in the state replication, consensus observation, and any activity that queries the state.
* **Vertical scalability**:
    
     scaling by improving the network's components to increase its computational power. When "scaling up", the network can accept more transactions and any activity that modifies the state.
In a blockchain context, vertical scalability is typically achieved through the optimization of the consensus mechanism and applications running on the chain. On the consensus side, Cosmos achieves vertical scalability with the help of the Tendermint BFT. The Cosmos Hub currently conducts transactions in seven seconds. The only remaining bottleneck is then the application.

The consensus mechanism and application optimization of your blockchain can only take you so far. To overcome the limits of vertical scalability, the multi-chain architecture of Cosmos allows for one application to run in parallel on different but IBC-coordinated chains, whether operated by the same validator set or not. This inter-chain, horizontal scalability theoretically allows for infinite vertical-like scalability, minus the coordination overhead.

# One layer instead of two

## How does Cosmos promote sovereignty?

**Applications deployed on general-purpose blockchains all share the same underlying environment.**

 When a change in an application needs to be made, it not only depends on the governance structures of the application but also on that of the environment. The feasibility of implementing changes depends on the governance mechanisms set by the protocol on which the application builds. **The chain's governance limits the application's sovereignty.** For this reason it is often called **two-layer governance**.

For example, an application on a typical blockchain has its governance structure, but it exists atop the blockchain governance, and chain upgrades can potentially break applications. Application sovereignty is therefore diminished in two-layer governance environments.

Cosmos resolves this issue, as developers can build a blockchain tailored to the application. There are no limits to the application's governance when every chain is maintained by its own set of validators. Cosmos follows a **one-layer governance design.**

In the world of traditional general-purpose blockchains, application design and efficiency are limited for blockchain developers. In the Cosmos universe, the standardization of architecture components is combined with customization opportunities to offer the possibility of an unconstrained, seamless, and intuitive user experience.

It becomes easier for users to **navigate between different blockchains and applications, as the same ground rules apply because of the standardization of components.** Cosmos makes the world easier for developers while making dApps more user-friendly. Cosmos enables **sovereignty** with **interoperability**!

Cosmos SDK is a set of tools with out-of-the-box consensus and execution, allowing anyone to create their own PoA/PoS blockchain. Unlike the other ecosystems covered in this piece, Cosmos is built on the premise that smart contract based virtual machines have limited flexibility, sovereignty and performance. Therefore, rather than build a single virtual machine on which multiple applications can run, Cosmos encourages and facilitates the creation of individual blockchains for each use case. Under this construct, application developers have flexibility around specific architecture, language etc. when building, and interoperability is achieved via Cosmos’ multi-chain communication layer, IBC (more on this later). Individual blockchains are called Zones while the connectivity modules are called Hubs.

* ![](https://lh5.googleusercontent.com/NsI1YXPUi8Q8YUPsKsTlIfSN9prpg_5fwWL6ZK5YkZY-r8zrNzafQ9OXDgadxRLLqj_nTNLPbKZIbsz1qFs7DobmWNFl1uO2IKk7r7pvEd5wPdK7xK2UJ9vWq49kADyMBNsAn5cV6rUCDLu1Ow)


![](https://miro.medium.com/max/720/1*I5iaRgiZZz0tiPwqd_Rapw.png)

![](https://miro.medium.com/proxy/1*51xuTm908Cgs5Qzl1vsj1A.png)

![](https://miro.medium.com/max/720/1*RTvLcQ9ItZ_uAcZw61L9kw.jpeg)

# References
* https://tutorials.cosmos.network/academy/1-what-is-cosmos/1-blockchain-and-cosmos.html#
* https://jumpcrypto.com/flavors-of-standalone-multichain-architecture-2/
* https://medium.com/flagship-defi/interchain-modules-will-change-how-cosmos-operates-4af77c89e65e