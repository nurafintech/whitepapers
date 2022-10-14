# A Blockchain App Architecture

## What is Tendermint?

Created in 2014, [Tendermint](https://tendermint.com/) accelerates the development of distinct blockchains with a ready-made networking and consensus solution, so developers do not have to recreate these features for each new case.
<br/>

## Tendermint-Made Blockchains

You may already use Tendermint without being aware of it, as other blockchains like _Hyperledger Burrow_ and the _Binance Chain_ use Tendermint.

## Tendermint Attends to Consensus and Networking

Tendermint modules attend (notice) to consensus and networking, which are important components of any blockchain.<br/>
**This frees developers to focus on the application level without descending into lower-level blockchain concerns** such as peer discovery, block propagation, consensus, and transaction finalization.

## Blockchain developer without Tendermint

Without Tendermint, developers would be forced to build software to address these concerns, which would add additional time, complexity, and cost to the development of their applications.

# Blockchain Node for Cosmos App Components

A blockchain node for an application-focused Cosmos blockchain consists of a **state-machine, built with the Cosmos SDK, and the consensus and networking layer, which are handled by the Tendermint Core.**

![](https://tutorials.cosmos.network/resized-images/600/academy/2-cosmos-concepts/images/architecture_overview.png)

## What is the Tendermint Core?

The Tendermint Core is a blockchain application platform which supports state machines in any language.The language-agnostic Tendermint Core helps developers securely and consistently replicate deterministic, finite state machines.
<br/>
Tendermint BFT is maintained even when 1/3rd of all machines fail, by providing two components:

<li>A blockchain consensus engine.</li>
<li>A generic application interface.</li>

# Consensus in Tendermint Core and Cosmos

It relies on Proof-of-Stake (PoS) with delegation and Practical Byzantine Fault Tolerance.<br/>
Users signal support by staking ATOM, or the native token of the respective chain. Staking bears the possibility of acquiring a share of the network transaction fees, in addition if you're an unreliable node, it could damage your publicity and your further rewards. _(orginal: but also the risk of reduced returns or even losses should the supported node become unreliable.)_
<br/>

## You do need to continue even in Adverse (harmful) conditions

Network participants are incentivized to stake their ATOM with nodes which are the most likely to provide dependable service, and to withdraw their support should those conditions change. A Cosmos blockchain is expected to adjust the validator configuration and continue even in adverse conditions.

# Who are the Validators?

Only the top 150 nodes (as ranked by staked ATOM) participate in the transaction finalization process as validators:))
<br/>

The privilege of creating a block is awarded in proportion to the voting power a validator has. Voting power is calculated as all ATOM tokens staked by a validator and its delegates.
<br/>

For example, if a given validator's voting power is 15% of the total voting power of all validators, then the validator can expect to receive the block creation privilege 15% of the time.

## Validators should be very Demanding

Validators and delegators are the parties who vote on proposals, with weights proportional to their respective stakes. If a delegator does not vote on a proposal, the delegator's vote is taken as that of its delegated validator.
<br/>
This means that delegators should be very demanding when they act, as they also lend their default vote to the validator.

## Validator's Broadcasting Conditions

The created block is broadcast to the other validators, who are expected to respond promptly and correctly:

<li>Validators confirm candidate blocks.</li>
<li>Validators absorb penalties for failing to do so.(??)</li>
<li>Validators can and must reject invalid blocks.</li>
<li>Validators accept the block by returning their signature.</li>

## Finalized Blocks with no Ambiguity

When sufficient signatures have been collected by the block creator, the block is finalized and broadcast to the wider network.
<br/>

There is no ambiguity in this process: either a block has the necessary signatures or it does not. If it does, insufficient signatories exist to overturn the block and so the block can be understood as finalized - there is no process in which the blockchain would be reorganized. This provides a level of certainty when it comes to transaction finality that a probabilistic system like Proof-of-Work (PoW) cannot match.

##

This is quite different from PoW, which favors inclusion and must accommodate slower nodes with greater latency and less reliability. A Cosmos blockchain can handle thousands of transactions per second, with confirmations taking seven seconds.

##

## Upgradeability of Chains

In any known blockchain, a change in the implementation requires an upgrade to the node software running on each node. In a disorderly process with voluntary participation, this can result in a hard fork: a situation in which one constituency forges ahead with the old rules while another adopts new rules.
<br/>

In a Tendermint blockchain, transactions are irreversibly finalized upon block creation, and upgrades are themselves governed by the block creation and validation process. This leaves no room for uncertainty: either the nodes agree to simultaneously upgrade their protocol, or the upgrade proposal fails.

# Application Blockchain Interface (ABCI)

Tendermint BFT packages the networking and consensus layers of a blockchain and presents an interface to the application layer, the Application Blockchain Interface (ABCI).
<br/>

![](https://tutorials.cosmos.network/resized-images/600/academy/2-cosmos-concepts/images/ABCI_3.png)

The Tendermint BFT engine is connected to the application by a socket protocol. ABCI provides a socket for applications written in other languages.
<br/>

## How is actually Tendermint connecting with ABCI?

Tendermint passes confirmed transactions to the application layer through the Application Blockchain Interface (ABCI). The application layer must implement ABCI, which is a socket protocol. If the application is written in the same language as the Tendermint implementation, the socket is not used.

## Tendermint and ABCI are completing each other

Tendermint is unconcerned with the interpretation of transactions, and the application layer can be unconcerned with propagation, broadcast, confirmation, network formation, and other lower-level concerns that Tendermint attends to (unless it wants to inspect such properties).

# Tendermint Guarantees

The Tendermint BFT provides security guarantees, including the following:

<li>Forks are never created, provided that at least half the validators are honest.</li>

<li>Determination of liability is achieved through the implementation of strict accountability for fork creation. <i>(original: Strict accountability for fork creation allows determination of liability.)</i></li>

<li>Transactions are finalized as soon as a block is created.</li>

##

The Tendermint BFT is not concerned with the interpretation of transactions. That occurs at the application layer, and Tendermint is un-opinionated about the meaning any transactions have.
<br/>

## Block time and Finality

The block time is approximately seven seconds, and blocks may contain thousands of transactions. Transactions are finalized and cannot be overturned as soon as they appear in a block.

## Two Board Approaches to Application-Level Concerns

<li>Create an application-specific blockchain where everything that can be done is defined in the protocol.</li>

<li>Create a programmable state machine and push application concerns to a higher level, such as bytecode created by compilers interpreting higher-level languages.</li>

## Ethereum-like Blockchains

Ethereum-like blockchains are part of the second category above: **only the state machine is defined in the on-chain protocol, which defines the rules of contract creation, interaction, execution, and little else.**

## What's the concerns of Ethereum-like systems development?

- Very little is universally defined: **standards** for basic concerns such as tokens **emerge organically through voluntary participation.**

- Contracts can and **do contain repetitive code that may or may not correctly implement the developer's intentions.**

- This inherent flexibility makes it **challenging to reason about what is correct, or even what is friendly.**

- There are practical limits to the complexity of operations, which are very low compared to what is possible in other settings.

##

**These limitations make it especially difficult to perform analysis or reorganize data, and developers are forced to adapt to the constraints.**

##

## A purpose-built or application-specific blockchain is different

There is no need to present a "Turing-complete" language or a general-purpose, programmable state machine because application concerns are addressed by the protocol the developers create.
<br/>

## Developing Experience With EVMs

Developers who have worked with blockchains based on the Ethereum Virtual Machine (EVM) will recognize a shift in the way concerns are addressed.
<br/>
Authorization and access control, the layout of storage and the state, and application governance are not implemented as contracts on a state machine.<br/>

They instead become properties of a unique blockchain that is built for a singular purpose.

# The Cosmos SDK

Developers create the application layer using the **Cosmos SDK**.
<br/>

- **A scaffold to get started:** The Cosmos SDK provides a development head start and a pre-established framework for new applications.

- **A rich set of modules:** The Cosmos SDK provides a rich set of modules that address common concerns such as **governance, tokens, other standards, and interactions with other blockchains** through the Inter-Blockchain Communication Protocol (IBC).

## Application Creating With Cosmos SDK

The creation of an application-specific blockchain with the Cosmos SDK is largely a process of selecting, configuring, and integrating well-solved modules, also known as **"composing modules".**

##

This greatly reduces the scope of original development required, as development becomes **mostly focused on the truly novel aspects of the application.**
<br/>

The application, consensus, and network layers are contained within the custom blockchain node that forms the foundation of the custom blockchain.

# What's Inter-Blockchain Communication Protocol (IBC)?

The Inter-Blockchain Communication Protocol (IBC) is a common framework for exchanging information between blockchains and also, It enables communication between applications that run on separate application-specific blockchains.

# Resources

[Cosmos Academy - A Blockchain App Architecture](https://tutorials.cosmos.network/academy/2-cosmos-concepts/1-architecture.html)

[Tendermint - Building the most powerful tools for distributed networks](https://tendermint.com/)

[Tendermint Core - The leading BFT engine for building blockchains](https://tendermint.com/core/)

[Tendermint Specification](https://github.com/tendermint/tendermint/tree/main/spec)
