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



## Current Integrations
Centrifuge Chain is built on substrate and bridged to Ethereum from day 1 through Tinlake. This enables us to plug into on-chain DeFi liquidity across platforms as is reflected in our partnerships with e.g. MakerDAO and Aave.<br/>

With MakerDAO, Centrifuge has been collaborating as the first protocol to back its Multi Collateral DAI with tokenized, real-world assets. <br/>

DeFi opens up a whole new (financial) universe to those companies that have been traditionally neglected by the prevailing financial system. Predatory lending and banks are replaced by smart contracts: a decentralized line of credit approved by a DAO.<br/>

MakerDAO is a first, and Centrifuge continues innovating with Aave and other large DeFi protocols to unlock instant liquidity.


# Introduction to Tinlake

Through Tinlake pools, businesses or "Asset Originators" can responsibly finance real-world assets, such as invoices, mortgages or streaming royalties through DeFi and access bankless liquidity. They do this by tokenizing their financial assets into Non-Fungible Tokens (“NFTs”) and use these NFTs as collateral in their Tinlake pool to finance their assets.

![](https://developer.centrifuge.io/3843697c5a64e5a00ba601fe848c25e4/tinlake.png)

## Earn yield and CFG rewards (TIN and DROP Tokens)
For every Tinlake pool, investors can invest in two different tokens: TIN and DROP. TIN, known as the “risk token,” takes the risk of defaults first but also receives higher returns. DROP, known as the “yield token,” is protected against defaults by the TIN token and receives stable (but usually lower) returns. This is similar to Junior/Senior investment structures common in traditional finance.


# Revolving Pools

## Intro (**important)
Revolving pools allow investors to invest/redeem independently at any time. A decentralized solver mechanism matches investments and redemptions and ensures that certain preferences (e.g. DROP redeem seniority) are considered and the pool's risk metrics are intact. This ensures that Asset Originators have a constant source of liquidity while investors can flexibly invest and redeem.

## Investing into Tinlake

<li>Investors can be whitelisted for either one (or both) of Tinlake's two tranches. To invest into TIN or DROP investors lock their investment in DAI into the Tinlake pool at any time during an epoch.</li>

<li> Investments and redemptions are then executed at the end of an epoch, usually every 24 hours.</li>

<li>A decentralized, automatic mechanism matches investments and redemptions making sure the pool's risk metrics remain intact, e.g. the DROP tranche is always protected by a minimum of TIN investors who take the loss first.</li>

<li>When the investments are executed the investors receive TIN or DROP tokens in exchange for the DAI locked. Transactions are executed at the current token prices reflecting the accrued interest and value according to the underlying NAV model over time.</li>

<li>
TIN and DROP tokens for investments and received DAI for redemptions can be collected at any time, independent of an epoch. Until collection TIN and DROP tokens remain securely locked in the Tinlake smart contracts and already accrue interest and earn CFG rewards.
</li><br/>

# Financing an asset
The Asset Originator can use the capital provided by investors to finance assets.<br/>
To do this, he locks an NFT representing a tokenized **"Real-World Asset"** into the set of smart contract as collateral.<br/>

**The NFT is minted based on a document created and shared through Centrifuge's P2P protocol.**<br/>

Financing fees and Principal/Maximum Financing amounts for these NFTs/tokenized assets are provided by an on-chain pricing scorecard and going forward determined by external service providers through **"Pricing Oracles"**. <br/>

**Once the NFT is priced the Asset Originator can draw down the financing. Upon repayment of the financing, the NFT is unlocked and transferred back into the Asset Originator's wallet.**


# Introducing Centrifuge Chain

## Intro
Centrifuge Chain is optimized specifically for the transactions required by our specific use case. **This focus allows us to improve upon our current architecture in a few key ways: speed, cost, storage efficiencies, and privacy.**

## ETH is great but ...
Ethereum works well for low volumes of high value transactions. High volumes of privacy-requiring use-cases require a different solution.<br/>

The average business user, SMBs and large enterprises alike, would be paying many times more using Centrifuge on Ethereum compared to their existing solutions. It wouldn’t be worth it for most businesses to make a switch. But what if we could lower that cost and have high throughput capabilities?


## Cenrtifuge Chain Wants to be optimized for the Small Operations but How?
The transactions on the Centrifuge Chain are optimized for the small subset of operations required by the Centrifuge protocol. This allows for faster execution of logic and finality of transactions.
<br/>

The optimization of transactions, together with our PoS architecture, is also what brings down the transaction costs dramatically. 

*(They claimed that they would make transactions faster with lower costs but how?)*

## State Rent Model
Centrifuge Chain also implements a state rent model that **requires users to pay for continuous availability of their data over long periods of time.**<br/>

This encourages decentralization because less resources are required to run a node. *(How?)*


## Building our own chain also allows us to improve upon the user and developer experience for Centrifuge 
 
Our users require privacy, and this is something we can build for directly — targeting the features they need from the start. For developers, we can provide custom APIs and tools that come with the blockchain node itself instead of smart contract APIs which are harder to integrate with.


## Downsides and Advantages to Building a Single Purpose Chain
While there are downsides to building a single purpose chain, the advantages for our use case outweigh the costs.<br/>

Integration with other Ethereum and DeFi projects becomes a bit more involved. Our experience with Ethereum development, **combined with a standardized bridge to get data to/from our Parity Substrate based chain reduces the overhead substantially, while still benefiting from the upside of our own chain.**

# Substrate/Polkadot
Centrifuge Chain is built on Substrate and will connect to the Polkadot Relay Chain as a Parachain. A parachain is a blockchain that is connected to a larger relay chain. The goal is for the relay chain to provide a high level of security, with its large validator set and high value at stake, to all of its connected parachains.<br/>

**<li>Centrifuge plans to become a parachain to outsource its chain security to achieve a higher level of security at a better cost - allowing Centrifuge to focus on its core features.**</li>

**<li>Another important benefit for Centrifuge will be using the relay chain to bridge to other chains in the Polkadot ecosystem.</li>**


*Polkadot will auction the first parachain slots later this year - and Centrifuge plans to be one of the first projects to obtain a parachain slot.*

## Future
We believe that Tinlake is only the first step. The Protocol we are building will enable use cases such as **Deep Tier Finance** fulfilling our vision to foster economic opportunity everywhere.



# References 

>Centrifuge Docs <br/>
https://developer.centrifuge.io/