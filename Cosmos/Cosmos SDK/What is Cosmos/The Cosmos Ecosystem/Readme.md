# The Modular and Customizable Cosmos SDK

Before Cosmos came along, developing a whole new chain was much more difficult and expensive than building a smart contract.

The main aim of the Cosmos network is to provide an ecosystem for easy blockchain development based on the Tendermint BFT and the Inter-Blockchain Communication Protocol (IBC) with the so-called Cosmos SDK (opens new window).

The Cosmos SDK is a generalized framework to build secure blockchain applications on the Tendermint BFT in Golang. It is a modular framework for application-specific blockchains. The design is based on two major principles:
*  modularity
* capability-based security: 

    The Cosmos SDK is built on the object-capability model (opens new window). It not only favors modularity but also encapsulates code implementation. An object-capability model ensures that:

    * There is no way for objects in the memory to be discovered just by going through the composed objects of others.
    * The only way to have references to objects or to access services is to have been passed the relevant object references.

    we'll talk about later on a separate paper.

 The Cosmos SDK was envisioned **to be an npm-like framework for secure applications** on top of Tendermint. Over time it has become an advanced framework for custom application-specific blockchains.


# The Inter-Blockchain Communication Protocol

The Inter-Blockchain Communication Protocol (IBC) (opens new window)is the basis for **interoperability** in Cosmos. It leverages the instant finality of Tendermint to allow for the transfer of value (token transfers) and communication between heterogeneous chains. Blockchains with different applications and architecture specifications become interoperable whether or not they share a validator set.

Cosmos implements a modular architecture with two blockchain classes: hubs and zones.
* ![](https://tutorials.cosmos.network/resized-images/600/academy/1-what-is-cosmos/images/hub-zones.png)

Zones are heterogeneous blockchains carrying out the authentication of accounts and transactions, the creation and distribution of tokens, and the execution of changes to the chain. Hubs are blockchains designed to connect the so-called zones. Once a zone connects to a hub through an IBC connection, it gets automatic access to the other zones connected to that hub. At this point, data and value can be sent and received between the zones without risk of, for example, double-spending tokens. This helps reduce the number of chain-to-chain connections that need to be established for interoperability.

There is no enforcement of an actual topology. A hub can be understood as a zone with many connections to other zones. Application zones can be expected to join the hubs in the ecosystem, but they are free to coalesce into any topology the developers find appropriate.


Zones are heterogeneous blockchains carrying out the authentication of accounts and transactions, the creation and distribution of tokens, and the execution of changes to the chain. Hubs are blockchains designed to connect the so-called zones. Once a zone connects to a hub through an IBC connection, it gets automatic access to the other zones connected to that hub. At this point, data and value can be sent and received between the zones without risk of, for example, double-spending tokens. This helps reduce the number of chain-to-chain connections that need to be established for interoperability.

**There is no enforcement of an actual topology.** A hub can be understood as a zone with many connections to other zones. **Application zones can be expected to join the hubs in the ecosystem, but they are free to coalesce into any topology the developers find appropriate.**

The **Cosmos Hub** was the first hub created. It is a public Proof-of-Stake (PoS) blockchain with a native token, ATOM. **The Cosmos Hub can be understood as a router facilitating transactions between the chains connected to it.** For example, the Cosmos Hub allows for **transaction fees to be paid in different tokens as long as the zone trusts the Cosmos Hub** and the other zones connected to it.

## Connecting to a non-Tendermint Chain

* Absolute finality chain:

    The IBC connection is not limited to Tendermint-based chains. If another, non-Tendermint blockchain uses **a fast-finality consensus algorithm**, a connection can be established by adapting IBC to work with the non-Tendermint consensus mechanism.

* Probabilistic-finality chain:

    If the other chain is a probabilistic-finality chain, a simple adaptation of IBC is not sufficient. A proxy chain called a **peg-zone** helps establish interoperability. **Peg-zones are fast-finality blockchains** which **track chain states** to establish **finality**. The peg-zone chain itself is IBC-compatible and acts as a **bridge** between the rest of the IBC network's chains and the probabilistic-finality chain.

# Building application-specific blockchains with one command

Ignite CLI (opens new window)is a developer-friendly, **command-line interface (CLI) tool** for application-specific blockchains which **builds on Tendermint and the Cosmos SDK**. The CLI tool offers everything developers need to build, test, and launch a chain. It accelerates blockchain development by scaffolding and assembling all components needed for a production-ready blockchain. Ignite CLI **makes the process** from initial idea to production **95% faster**. This lets developers build a blockchain in minutes, and frees them to **focus more strongly on the business logic** of their application.

With Ignite CLI, developers can:

* Create a modular blockchain written in **Go** with a single command.
* Start a development server to experiment with **token creation and allocation**, as well as module configuration.
* Allow for inter-chain **token transfers** by using a built-in IBC relayer to send value and data to **different chains**.
* Benefit from a fast-developed frontend with automatically **generated APIs and web pages in JavaScript, TypeScript, and Vue**.

When you scaffold with Ignite CLI, things like key management, creating validators, and transferring tokens can all be done through the CLI.

# CosmWasm - multi-chain smart contracts

CosmWasm is a multi-chain solution for smart contracts on Cosmos - that is the Cosm part. It is a way of using **WebAssembly** in the Cosmos universe - that is the Wasm part.

you can create robust decentralized applications (dApps) for Cosmos using smart contracts and building on Tendermint and the Cosmos SDK. Its key features are:

* Mature tools for the development and testing of smart contracts
Close integration with the Cosmos SDK and ecosystem
* A secure architecture to avoid attack vectors
* CosmWasm's design makes your code agnostic to the details of the underlying chains. It only requires that a Cosmos SDK application embeds the Wasm module.

**With CosmWasm, smart contracts can run on multiple chains with the help of the IBC protocol.** It adds further flexibility for developers and makes smart contract development faster. CosmWasm is written as a module to be plugged into the Cosmos SDK and leverages the **speed of Wasm** and the power of **Rust**. CosmWasm is ideal for **Rust developers** looking for a blockchain platform with fast transaction finality.

# Using alternative blockchain frameworks and SDKs

As the Cosmos SDK is modular, **developers can port existing codebases in Go on top of the SDK**. This allows developers to build on Cosmos without having to compromise too much on the toolset and environment used.

For example, with **Ethermint** developers can use the Ethereum Virtual Machine (EVM) from the main Go Ethereum client as a Cosmos SDK module, which is compatible and combinable with existing modules.

**Ethermint is a software developed to port the EVM into a Cosmos module.** It makes scalable, high-throughput, PoS blockchains possible. **These are fully compatible with Ethereum and the Cosmos SDK.**

Ethermint is Web3 compatible, and achieves high throughput with Tendermint and horizontal scaling with IBC. **It provides a Web3, JSON-RPC layer to interact with Ethereum clients and tooling.**

All Ethereum tools (such as Truffle and Metamask) are compatible with Ethermint. Developers can even port their Solidity smart contracts to interact with the Cosmos Ecosystem. **Building a chain is not necessary to develop Cosmos-compatible smart contracts, it can be all done with Ethermint.** However, while Ethermint allows running vanilla Ethereum as a Cosmos application-specific blockchain, developers benefit from the Tendermint BFT.