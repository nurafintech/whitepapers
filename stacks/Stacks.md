# Stacks (STX)

We're going to talk about Stacks project which using Bitcoin for its privacy.

# Why Bitcoin?

Why Bitcoin Bitcoin is the strongest sovereign blockchain. Bitcoin is a tamper-proof source of truth; a value settlement protocol.

# Challenges to build apps and smart contracts on Bitcoin

> **Scalability** The base Bitcoin blockchain has a limited capacity for transactions.
> <br /> > **Secure contracts** The Bitcoin blockchain has a limited scripting language and does not allow general smart contracts. This design choice ensures security at the base layer.
> <br />

We do this through a unique consensus algorithm that runs between two blockchains.

# Enabling the smart-contracts on Bitcoin

We enable this without modifying Bitcoin, a critical design requirement for enabling such apps and smart contracts.

# Earning Bitcoin

Bitcoin’s fixed, limited supply and adoption as a hedge against inflation makes earning BTC attractive. Further, as smart contract usage increases on the Stacks blockchain, BTC earning rate also increases.

# Stacks 2.0 Design

Stacks 2.0 is a layer-1 blockchain that connects to Bitcoin for security and enables decentralized apps and predictable smart contracts. Stacks 2.0 implements PoX mining that anchors to Bitcoin security. (We'll talk about PoX further) <br/>
With PoX there is no need to modify Bitcoin to enable smart contracts and apps around it.

# STX miners

**STX miners** can view state on both the Bitcoin blockchain and the Stacks blockchain. STX miners participate in leader election by sending transactions on the Bitcoin blockchain, a **Verifiable Random Function (VRF)** randomly _selects leader of each round (while giving more weight to higher BTC bids)_, and the leader writes the new block on the Stacks chain. <br/>

STX miners get newly minted STX (coinbase rewards), transaction fees paid to them in STX, and Clarity contract execution fees of each block also paid in STX. <br/>

STX miners express the cost of mining in BTC and spend BTC to participate in leader election. The STX miners can model the total value of a new Stacks block as a BTX/STX on-chain trading pair, and will participate in mining if they can get cheaper STX from mining than from outside exchanges.<br/>

# STX Holders

**STX holders** can participate in consensus and earn BTC rewards by participating in a process called Stacking.
<br/>
To participate, users lock their STX for a reward cycle (approx two weeks), run or support a full node, and send useful information on the network as STX transactions.<br/>
STX holders who actively participate in Stacking earn the Bitcoin rewards of that cycle.
_Unlike proof of stake, there is no risk of slashing (economic penalties by protocol) for STX holders._

# Scalability of Transactions

The Stacks blockchain transactions can scale independently of Bitcoin; they only depend on Bitcoin for finality. Thousands of Stacks transactions result in a single hash on Bitcoin; _Stacks transactions “settle” on Bitcoin automatically every Bitcoin block as part of consensus._<br/>

# Microblocks

**Stacks introduces the concept of _Microblocks_ that give initial confirmation in seconds.** Microblocks are a main venue for future scalability research, where theoretically faster consensus algorithms can run for microblocks that settle data on Bitcoin per Bitcoin block.<br/>
Bitcoin is used as a settlement protocol by Stacks. It serves as the source of ultimate truth and archives hashes of Stacks block history. Finality of transactions is currently tied to Bitcoin and we believe that Bitcoin offers a strong notion of finality that our design benefits from.<br/>
The Stacks 2.0 blockchain is written in Rust. Protocol details and the open-source code is available in the Stacks [GitHub repository.](https://github.com/blockstack/)

# Proof of Transfer (PoX)

Proof of Transfer (PoX) is the first consensus algorithm between two blockchains. Specifically we present an implementation of PoX by using Bitcoin as the base chain and Stacks as the connected chain.<br/> In PoX, leader election happens on the Bitcoin blockchain. **Instead of burning electricity on proof of work, PoX reuses already minted bitcoins as “proof of computation” and miners represent their cost of mining in bitcoins directly.**<br/>
For detail you could visit [“PoX, Proof of Transfer Mining with Bitcoin”](https://blockstack.org/pox.pdf)
