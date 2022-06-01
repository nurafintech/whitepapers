# Centrifuge
Centrifuge is a network that provides access to fast, cheap capital for small businesses and stable yield for investors. Centrifuge bridges real-world assets into DeFi (“Decentralized Finance”) to bring down the cost of capital for small to medium‐sized enterprises (SMEs) and provide DeFi investors with a stable source of yield **uncorrelated from volatile crypto assets.**
</br>
Tinlake is Centrifuge’s investment app that acts as an open marketplace of real-world asset pools. Investors can look through the pools provided by Asset Originators and invest in the ones that work for them.

## Centrifuge Chain
Centrifuge Chain is the home for real-world assets (RWA) on-chain. It is a Proof-of-Stake blockchain built on Substrate that enables users to bring their assets on-chain as non-fungible tokens (NFTs). This is the starting point to unlock financing for any type of asset through DeFi. Centrifuge Chain is bridged to Ethereum, but uses its own native token - the Centrifuge (CFG) token.
<br/>


## Centrifuge token (CFG)
Centrifuge token (CFG) is a crypto economic primitive and a native token that utilizes a nominated-Proof-of-Stake consensus algorithm to stake validators and provide incentives for Centrifuge adoption. CFG empowers holders to guide the development of Centrifuge through on-chain governance.
<br/>

<li>The Centrifuge token (CFG) powers the Centrifuge Chain. </li>
<li> CFG is designed to incentivize desirable behavior on Centrifuge Chain — so called mechanism design — to create a robust, decentralized system.</li>
<li>Owning CFG gives users a stake in the Centrifuge network and can be used to pay for transaction fees, stake towards Collators, and participate in Centrifuge on-chain governance.</li>
<li>It will also incentivize chain security - both by rewarding DOT holders in the Parachain Loan Offering, and by distributing a block reward to Collators and Nominators.</li>

<li>Centrifuge also empowers its holders with governance. Centrifuge Chain uses Substrate’s native governance module, comprising an elected council and the ability to administer network upgrades.</li>
<br/>

> As the utility of Centrifuge grows, the Centrifuge token will capture the growing value provided to users of the network through each of its utilities. <br/>
This value is primarily captured in the use of CFG for transaction fees, and additionally through its importance in Governance of the network. **The token will also serve as a store-of-value through the implementation of the insurance DAO in which CFG will be staked.**

<br/>

## NFTs - The link to traditional finance
Centrifuge’s privacy-enabled NFTs are tokenized representations of individual assets, keeping some of the assets attributes private on a p2p protocol, while the Centrifuge Chain - a public, decentralized ledger - tracks the asset ownership. This structure allows us to create something unique in DeFi.


# Why Centrifuge and A DeFi Platform?
In today’s financial system, only the largest businesses get direct access to liquid capital markets. Most depend on banks for their capital needs. The lack of an **open and transparent marketplace** denies these smaller businesses access to competitive interest rates mostly due to market inefficiencies and transaction costs.<br/>

DeFi is a growing financial system without any barriers of entry. Centrifuge wants to bring this benefit to all borrowers that until now had no access to DeFi liquidity.

# Tinlake: Brief Explanation
With our first user facing product - Tinlake - **Centrifuge allows anyone to launch an on-chain credit fund creating collateral-backed pools of loans.** Tinlake offers an easy way into DeFi liquidity for any business. For DeFi investors, these assets will create a safe, stable yield for their money uncorrelated from attractive yet volatile returns in crypto markets. Through CFG Rewards, investors can farm additional yield and participate in the ecosystem.

# Tinlake is currently built on Ethereum 
Tinlake is currently built on Ethereum, however going forward it will be fully migrated to our *Centrifuge Chain* and our secure p2p protocol. This will allow **accurate pricing and risk assessment** of any kind of assets (be that your future revenue as a business, a house or some farm land) and create liquid markets for these assets. As this ecosystem grows, more data will be on chain reducing the trust in the off-chain world and reducing the dependence on a single point of failure.


# The Ecosystem
## Our Tech Stack
![](https://developer.centrifuge.io/5713d7bb0b3889831a27cfb8f7d07f50/centrifuge_tech_stack.png)

## Tinlake
Tinlake is the consumer facing Dapp used by asset originators and investors to finance assets. This is currently built on Ethereum, Tinlake communicates to the Centrifuge Chain via a Chainsafe bridge, but moving forward Tinlake will fully migrate to the Centrifuge Chain.<br/>

Tinlake allows for on-chain borrowing against collateralized assets completely managed by smart contracts. <br/>

Not only does Tinlake enable Asset Originators to access the growing liquidity in the Decentralized Finance ecosystem, it also enables stablecoin issuers to offer a stable store of value backed by collateralized asset pools. <br/>

> Ultimately, Tinlake will become a fully decentralized financing protocol that interoperates with different blockchains and plugs into a variety of funding sources, including a variety of stablecoins.

# Centrifuge Chain
Centrifuge Chain is the home for real-world assets (RWA) on-chain. It is a **Proof-of-Stake** blockchain built on Substrate that enables users to bring their assets on-chain as non-fungible tokens (NFTs). <br/>

Bridged to Ethereum from day 1. Centrifuge Chain uses its own native token - the Centrifuge (CFG) token. It also incentivizes nodes (known as Collators) and Nominators to participate through a block reward. <br/>

This public chain is owned and operated by no single party: the Centrifuge token empowers its holders with an on-chain governance mechanism that empowers token holders to guide the development of Centrifuge. The chain also employs the Centrifuge token to stake value and provides rewards for security and for Centrifuge adoption, currently through liquidity rewards.


## Centrifuge on Polkadot

Centrifuge Chain is built on Parity Substrate, and is currently transitioning from a sovereign chain to a parachain on Polkadot.<br/> 

It relies on staked nodes (Collators) to author blocks and, once Centrifuge Chain becomes a parachain, they will maintain the Centrifuge parachain by collecting transactions from users and producing state transition proofs for Polkadot Relay Chain validators.<br/>

Any node can offer itself as a Collator candidate, but only a limited number will be selected. Only top Collators by stake are elected into the Active Set. Collators can stake their own CFG and can be elected by staked Nominators.<br/>

In order to secure a parachain slot, Centrifuge will host a Crowd Loan from DOT holders in a Parachain Loan Offering (timeline TBA!). DOT holders who stake their tokens on behalf of the Centrifuge parachain slot will receive CFG as a reward.<br/>

> **You can see the complete explanation about Parachain and its mechanism in Concepts/Parachain.md


# P2P protocol and Node (important**)
> The p2p protocol provides a method to create, exchange and verify asset data and is used for private, off-chain data exchange.<br/>

Asset originators can selectively share asset details with service providers who can assess the data and contribute pricing and underwriting information to the document. The data origin can be verified using cryptographic signatures.<br/>

>**The components of the p2p protocol are a collection of Ethereum smart contracts and a peer to peer (p2p) network implemented on libp2p.**


## Ethereum smart contracts are used for:

<li>Maintaining identities in a similar format to the ERC725 standard</li>
<li>Anchoring state commitments</li>
<li>Minting NFTs from off chain Centrifuge documents (important**)</li>
<br/>

>The Centrifuge Node provides a simple API interface to interact with the peer to peer network as well as the Ethereum smart contracts.



# Integrations/Composability

## The ETH/DOT Relationship

Centrifuge Chain bridges the Ethereum and Polkadot ecosystems - bringing DeFi liquidity from both to finance real-world assets on Tinlake.

![](https://developer.centrifuge.io/f65624f472b6b2207525202efefb3a20/centrifuge_ecosystem.png)


> **This gives Centrifuge an edge on accessing two of the biggest ecosystems in crypto: one for DeFi liquidity today (ETH) and one for speed and a growing ecosystem (DOT).**











## Future
We believe that Tinlake is only the first step. The Protocol we are building will enable use cases such as **Deep Tier Finance** fulfilling our vision to foster economic opportunity everywhere.



# References 

>Centrifuge Docs <br/>
https://developer.centrifuge.io/