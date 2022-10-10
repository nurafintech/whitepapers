# Tendermint & Cosmos SDK Demystified

## Blockchains Architecture
Each blockchain has 3 main layers:

#1 — Consensus Layer
Blockchain is a distributed ledger in which the validity and order of the transactions are guaranteed through the consensus process. During this process, a set of network participants (miners, validators, or similar names) try to propose, validate, and pass a set of blocks with transactions. These nodes do not necessarily trust each other. Moreover, the algorithm for assigning tasks to different nodes differs in each consensus model. The consensus layer is the module responsible for handling all consensus-related tasks.

**#2 — Network Layer**
Communication between network participants is an essential feature of every blockchain system. There are many types of needed communication in distributed ledger-based systems. First of all, the nodes responsible for reaching consensus need to communicate with each other for making decisions. Users also should be able to send their transactions through. Finally, third-party applications such as smart contracts, wallets, or dApps need to find a channel to transact with the blockchains. **The network layer is responsible for facilitating all types of these communications.**

**#3 — Application Logic Layer**
Blockchain is the general term we use to define distributed ledger systems. In principle, each blockchain is an infrastructure for making decentralized applications. For example, Bitcoin is a decentralized peer-to-peer payment system. Ethereum is a blockchain for developing smart contracts. Therefore, it is safe to say that each project defined in the space need to have its own business logic. This is exactly the feature that distinguishes the use-cases of different projects. **Application Logic Layer is the module through which such logics will be defined and implemented.**

#

## Approaches to Develop Blockchains

#1 — Fork Existing Blockchains

The source code for almost all well-known blockchains is open-source. This means that anyone can get a copy of these source codes, make modifications to them, and redeploy them under a new name. This is what we call a fork project. If you review the blockchain projects, you will find many examples of such forks. For example, Litecoin is a fork of Bitcoin. More interestingly, Dogecoin is a fork of Litecoin. The beautiful thing about forking is that developers do not need to build something from scratch. They can use already developed codes, and add some more features to them, when needed. However, this needs a high level of technical knowledge.

Example Projects:

* Litecoin (LTC)
* Dogecoin (DOGE)
* Bitcoin Cash (BCH)
* eCash (XEC)
* Ethereum Classic (ETC)

#2 — Develop Smart Contracts on Existing Blockchains<br>
There are many blockchains offering smart contracts features. Smart contracts are pieces of code running on virtual machines. Using these codes, many different applications such as wallets, DeFi apps, fungible and non-fungible tokens can be implemented easily. The nice thing about smart contracts is that developers do not need to worry about the core blockchain and infrastructure. They only need to focus on the logic of the contract. The rest (security, decentralization, etc) will be handled by the blockchain in which the code will be deployed. However, the main issue here is that the dApp written with these contracts will have the same limitations as the parent blockchain. A famous example is the Ethereum blockchain and its smart contracts. Ethereum — at its current version — has scalability issues. Therefore, the smart contracts deployed in this Blockchain also are suffering a lot from transaction throughput and fees.

Example Projects:
* Chainlink (LINK)
* Shiba Inu (SHIBA)
* Tether (USDT)
* Wrapped Bitcoin (WBTC)
* Decentraland (MANA)

#3 — Develop Blockchains From Scratch <br>
This is probably the most complicated option on this list. Here, we are talking about building a blockchain from zero. For this, it is necessary to:

1. Build Consensus Layer
2. Build Network Layer
3. Build Application Logic Layer

As discussed in the previous sections, each one of these layers has lots of technical considerations. Therefore, building blockchains using this approach most probably will take more time and energy. The advantage of this approach is that the project will not depend on any external code. Therefore, 100% of the design can be done by the developers of the project, and with complete flexibility.

Example Projects:
* Bitcoin (BTC)
* Ethereum (ETH)
* Solana (SOL)
* Cardano (ADA)
* Polkadot (DOT)

#4 — Use Existing APIs and SDKs<br>
The last option of this list is probably the most interesting one. Developers can use existing APIs and SDKs to develop blockchain projects. These tools are basically the ready-to-use components for programmers. Some examples are:
* Consensus Models
* Networking Protocols
* Cryptography methods
* Storage APIs
* Client Side Frameworks
* Web Frameworks
* Authentication/Authorization modules

This means that developers do not build everything from the scratch (a.k.a core blockchain), and at the same time, they do not rely on the security, and performance of the existing projects (a.k.a forks, smart contracts). Therefore, this approach mixes the best features of all previous ones.

Example Projects:

* Hyperledger
* Binance Chain
* Terra (LUNA)
* Kava (KAVA)
* Oasis Network (ROSE)

#

## Tendermint 
Tendermint is a set of ready-to-use tools and technologies for implementing consensus and networking layers of blockchain projects. In other words, developers can connect their application business logic to the Tendermint components and build complete projects. Now let's explore more two main components of the Tendermint.

#1 — Blockchain Consensus Engine (Tendermint Core)

![](https://miro.medium.com/max/700/1*iPl16YZ6UmtI-S9yrF0fYQ.png)

The consensus engine of the Tendermint is called Tendermint Core and is powered by Byzantine Fault Tolerant (BFT) consensus model. In simple words, Byzantine means traitor (or bad actor), and the BFT model can tolerate less than one-third of the Byzantine validators to reach consensus.

In the image above, you can see the summary of the BFT process. It has four main steps:
1. Propose: a new validator proposes a block at a specific height.
2. Prevote (first voting stage): at least 2/3 of validators prevote for the proposed block.
3. Precommit (second voting stage): at least 2/3 of validators precommit for the proposed block.
4. Commit: validator will commit the proposed block to the blockchain.

At each stage, if something goes wrong, there are some rules and conditions to address the situation. For example, if a validator fails to commit a block, other validators skip that block after some waiting time and move to the next round of decision-making.

#2 — Application BlockChain Interface (ABCI)

![](https://miro.medium.com/max/700/1*hGo54qaEOvAjBFKx3mQZIA.png)

Application Blockchain Interface (ABCI) is a set of ready-to-use methods for connecting the consensus engine to the application layer logic. Therefore, ABCI is the main component of the networking layer, and all the messages and transactions should be channeled through the ABCI. There can be multiple ABCI socket connections to an application. Here are the most important ones:

* CheckTx: to validate the received transactions from users before entering to the mempool.
* BeginBlock: a hook that is called before every new block that has been agreed upon by the majority of the validators in the validator set.
* DeliverTx: invoke the application logic to interpret and process the transaction and update the state.
* EndBlock: a hook to terminate the processing of each block.
* Commit: to finalize the processing of block after the block’s processing.

It is also worth mentioning that ABCI at its core is a set of API calls. Therefore, developers have complete flexibility to use different programming languages (e.g. Solidity, Rust, C++) to use these methods in their application logic layer.

## Tendermint Pros

### Separated of concerns
As discussed, Tendermint has two main components. Tendermint Core is the consensus engine, and ABCI is the networking layer API. Under this approach, the different layers of each blockchain project can be separated. This indeed gives flexibility to developers to focus on each layers’ concerns.

### BFT Consensus
Byzantine Fault Tolerant (BFT) consensus model is a secure, and trustworthy model to reach consensus between nodes. Tendermint uses this model in its consensus engine and implemented lots of features on top of it to ensure that it works perfectly fine in the projects.
### Tendermint Cons: 33% Attack
As discussed earlier, the BFT model can tolerate 1/3 traitor (Byzantine) nodes. This means that if one-third of validator nodes act maliciously in the network, the blockchain potentially can experience attacks (hacks). In comparison to other consensus models, this fault-tolerance rate is lower. For example, in the Proof of Work (PoW) consensus model, this rate is 51%.
### Number of Validators
![](https://miro.medium.com/max/700/0*SX2d0t4ZqQClKBFi.png)

Tendermint is not a complete asynchronous system. To reach consensus, and propagate the transactions/blocks, validators need to communicate with each other through different steps (prevote, precommit, commit). Therefore, the throughput of the whole system is highly dependent on the number of validators. The more validators presented in the system, the lower the throughput will be.

#

## Cosmos SDK
Cosmos SDK is a set of tools and frameworks developed by the Cosmos team. Using this SDK, developers can start to build the application logic layer. ***Furthermore, they can use Cosmos SDK in conjunction with Tendermint Core and ABCI to use the existing functionalities of the consensus engine and networking layer.**

**Here are some of the cool things you can do using Cosmos SDK:*
* Implementation of the required ABCI methods.
* Implementation of the storage layer.
* Implementation of cryptography features such as digital signatures and key generation.
* Implementation of client applications in Go programming language.
* Storage and management of user accounts.
* Transactions management (format, structure, validation, etc.)
* Maintaining balances and transferring different tokens.
* Delegated Proof of Stake and slashing feature of DPoS.
* On-chain governance.
* Wallet/Key Management.

Using Cosmos SDK, you can do all these things (and more). There are ready-to-use methods in the SDK. **Furthermore, you can override existing methods with your own logic.** This will save you lots of time and energy for making projects.

<br>

**Cosmos SDK Pros**
1. Independent Blockchains: <br>
One of the best features of Cosmos SDK is that it allows to develop Interblockchain communication (IBC) protocol. Using this approach, users can build a blockchain of blockchains (e.g. Cosmos, Oasis Network). The needed code and methods for implementing such networks already exist, and minor modifications can be applied if needed.

2. Ready to Use Modules in the Application Logic Layer: <br>
Cosmos SDK handles most of the needed tasks in the application logic layer. This includes, and is not limited to transactions, storage, cryptography, governance, tokens, wallets, balances, and so on. Developers can plug these ready-to-use components into their projects without the need to reinvent the wheel.

<br>

**Cosmos SDK Cons**
1. Smaller Community: <br>
Ethereum is still by far the most popular framework for developing smart contracts and dApps. Standards such as ERC20, ERC721, or ERC1155 rule the market. The community around these standards is big, and there are lots of available online resources. On the other hand, the Cosmos SDK community is still not big enough. In some cases, the documentation and resources are also seldom.
2. Learning Curve: <br>
Most of the codes you find in the Cosmos SDK are in the Go programming language. **Although Go is a very modern and rich programming language, in some cases understanding it is complicated.** Moreover, to use the full potential of Cosmos SDK, it is necessary to understand how Tendermint Core, ABCI, and Interblockchain Communication (IBC) protocol work. **Therefore, one needs to learn lots of stuff before really starting to use the SDK itself.**

مخاطب این قسمت که bold   هم کردم شمایی آقای مرتضی ئییییی!


#

## Examples of Projects in Cosmos and Tendermint Ecosystem
**Cosmos (ATOM):** <br>
Cosmos is one of the leaders of the “Blockchain 3.0” movement developed using Tendermint and Cosmos SDK. Implementing scalable and sustainable “Interblockchain Communication Protocol” is the main focus of the project.<br>
For making blockchain interoperability possible, Cosmos is using two concepts called “hubs” and “zones”. Hubs are central ledgers of the whole Cosmos system. Zones are independent blockchains.<br>
Cosmos is not just a single blockchain. It offers blockchain interoperability. In other words, using Hubs, the different blockchain can communicate with each other. In order to make this happen, two types of transactions are used:
  1. IBCBlockCommitTx: allows a blockchain to prove to any observer of its most recent block-hash.
  2. IBCPacketTx: allows a blockchain to prove to any observer that the given packet was indeed published by the sender’s application, via a Merkle-proof to the recent block-hash.


**Terra:**<br>
Terra is an innovative blockchain platform powering various algorithmic stablecoins such as TerraUSD (pegged to US dollar) and TerraKRW (pegged to Korean Won). It also offers LUNA tokens to its users as an stakable token to earn rewards.<br>
The Terra Blockchain is powered by Tendermint and Cosmos SDK.<br>
To propose and add new blocks into the blockchain, a proposer validator is selected first. This validator proposes a block and all other validators vote in favor or against the proposed block. If the block is getting rejected in votes, another proposer is selected and this process continues until validators vote in favor of a proposed block.<br>
During this process, all validators and delegators are rewarded with transaction fees from the block. Furthermore, the proposer validator who successfully managed to pass her block will be rewarded extra.<br>
Using this consensus model, batches of transactions can be validated and confirmed in a matter of seconds (approximately 6 seconds according to the official documentation).

**Oasis Network:**<br>
Oasis Network is a layer 1 blockchain that promotes data privacy and user confidentiality. Thanks to its high throughput and secure design, the Oasis Network intends to power scalable solutions on DeFi and data privacy.

Oasis Network has 2 main layers:

1. The Consensus Layer is responsible for accepting values from clients (ParaTimes), writing transactions (submitted by ParaTimes) into the blockchain, validator and ParaTime committee selection, handling consensus operations, and handling native tokens operations (e.g staking). **The consensus layer is a simple BFT / Proof of Stake blockchain, powered by the Tendermint BFT consensus model.**

2. ParaTimes Layer is responsible for defining smart contract execution environment, defining semantics for the interfaces it exposes, defining mechanisms and parameters for verifying contracts execution, and implementing confidentiality measurements for smart contracts execution.

Users can run validator nodes on Oasis Network and earn staking rewards. By design (Cosmos Tendermint), the maximum number of validators is 110. The top validators will be elected according to their staking weight, with the minimum 100 tokens defined as a threshold. The staking rewards will be somewhere between 2%–20%.

 نکته منفی این SDK ، وجود سقف 100 عددی تعداد ولیدیتور هاست که خب به نوعی برای اینکه عملکرد بهبود پیدا کنه مجبور شده تا از غیرمتمرکز بودن آن کم بکند.


#

References:
* https://medium.com/coinmonks/tendermint-cosmos-sdk-demystified-47385cf77cf6