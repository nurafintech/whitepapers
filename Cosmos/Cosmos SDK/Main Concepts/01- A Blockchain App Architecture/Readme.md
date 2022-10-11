# A Blockchain App Architecture
## What is Tendermint?
Created in 2014, [Tendermint](https://tendermint.com/) accelerates the development of distinct blockchains with a ready-made networking and consensus solution, so developers do not have to recreate these features for each new case.
<br/>

## Tendermint-Made Blockchains 
You may already use Tendermint without being aware of it, as other blockchains like *Hyperledger Burrow* and the *Binance Chain* use Tendermint.

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
Users signal support by staking ATOM, or the native token of the respective chain. Staking bears the possibility of acquiring a share of the network transaction fees which means if you're an unreliable node, it could damage your publicity and your further rewards. *(orginal: but also the risk of reduced returns or even losses should the supported node become unreliable.)*
<br/>



# Resources
[Cosmos Academy - A Blockchain App Architecture](https://tutorials.cosmos.network/academy/2-cosmos-concepts/1-architecture.html)

[Tendermint - Building the most powerful tools for distributed networks](https://tendermint.com/)

[Tendermint Core - The leading BFT engine for building blockchains](https://tendermint.com/core/)

[Tendermint - Github](https://github.com/tendermint/tendermint)