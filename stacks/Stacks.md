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

# Proof of Transfer (PoX)

we have built the first consensus algorithm between two blockchains, called Proof of Transfer (PoX), that connects the Bitcoin and the Stacks blockchains and extends the functionality of Bitcoin.

# Stacks 2.0 Design

Stacks 2.0 is a layer-1 blockchain that connects to Bitcoin for security and enables decentralized apps and predictable smart contracts. Stacks 2.0 implements PoX mining that anchors to Bitcoin security. <br/>
With PoX there is no need to modify Bitcoin to enable smart contracts and apps around it.

# STX miners

**STX miners** can view state on both the Bitcoin blockchain and the Stacks blockchain. STX miners participate in leader election by sending transactions on the Bitcoin blockchain, a **Verifiable Random Function (VRF)** randomly _selects leader of each round (while giving more weight to higher BTC bids)_, and the leader writes the new block on the Stacks chain. <br/>

STX miners get newly minted STX (coinbase rewards), transaction fees paid to them in STX, and Clarity contract execution fees of each block also paid in STX. <br/>

STX miners express the cost of mining in BTC and spend BTC to participate in leader election. The STX miners can model the total value of a new Stacks block as a BTX/STX on-chain trading pair, and will participate in mining if they can get cheaper STX from mining than from outside exchanges.<br/>
