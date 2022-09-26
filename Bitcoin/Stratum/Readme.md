# Stratum 
The stratum overlay protocol was extended to support pooled mining as a replacement for
obsolete getwork protocol in late 2012. The mining service specification was initially announced
via Slush's pool's website [2]. 

# Why Stratum? [4]
The main reason why I designed this protocol and implemented opensource pool server is that **the current getwork&LP mining protocol has many flaws and it can hardly be used in any large-scale setup.** 
<br/>
ASIC miners are probably coming at the end of the year 2012 :q, so Bitcoin community definitely needs some solution, which will easily scale to tera-hashes per second per pool user.

# Protocol Summary [1]
The Stratum protocol reduces client-server communications to levels that are usable with very low
bandwidth, and reduces the strain on servers drastically.
<br/>
**The key concept behind Stratum based mining is "push" based work**, where the server pushes
work to the miner, and the miner is able to utilize that work until the next push, regardless of the
hash rate.
<br/>
**This is done by allowing the miner to increase a counter in the coinbase transaction, and build a
new merkleroot for the block header, which effectively means the miner generates new work continuously without contacting the server.**




# The Bitcoin Network

Bitcoin’s P2P network architecture is much more than a topology choice. The term “bitcoin network” refers to the collection of nodes running the bitcoin P2P
protocol. In addition to the bitcoin P2P protocol, there are **other protocols such as
Stratum** that are used for mining and lightweight or mobile wallets. <strong>These additional protocols are provided by gateway routing servers that access the bitcoin network
using the bitcoin P2P protocol and then extend that network to nodes running other
protocols.</strong> For example, **Stratum servers connect Stratum mining nodes via the Stratum protocol to the main bitcoin network and bridge the Stratum protocol to the bit‐
coin P2P protocol.** We use the term **“extended bitcoin network”** to refer to the overall
network that includes the bitcoin P2P protocol, pool-mining protocols, the Stratum
protocol, and any other related protocols connecting the components of the bitcoin
system.

Although nodes in the bitcoin P2P network are equal, they may take on different
roles depending on the functionality they are supporting. A bitcoin node is a collec‐
tion of functions: routing, the blockchain database, mining, and wallet services.

The main bitcoin network, running the bitcoin P2P protocol, consists of between
5,000 and 8,000 listening nodes running various versions of the bitcoin reference cli‐
ent (Bitcoin Core) and a few hundred nodes running various other implementations
of the bitcoin P2P protocol, such as Bitcoin Classic, Bitcoin Unlimited, BitcoinJ, Lib‐
bitcoin, btcd, and bcoin. A small percentage of the nodes on the bitcoin P2P network
are also mining nodes, competing in the mining process, validating transactions, and
creating new blocks. Various large companies interface with the bitcoin network by
running full-node clients based on the Bitcoin Core client, with full copies of the
blockchain and a network node, but without mining or wallet functions. These nodes
act as network edge routers, allowing various other services (exchanges, wallets, block
explorers, merchant payment processing) to be built on top.

Attached to the main bitcoin P2P network are a number of pool servers and protocol gateways that connect nodes running other protocols. These other protocol nodes are mostly pool
mining nodes and lightweight wallet clients, which do not carry a full copy of the blockchain.

All nodes include the routing function to participate in the network and might
include other functionality.



# Ethereum Stratum (EIP-1571)


# References

1- [[bitcoin-dev] [BIP] Stratum protocol specification](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-February/015728.html)

2- [Stratum mining protocol](https://en.bitcoin.it/wiki/Stratum_mining_protocol)

3- [Where are BIPs 40 and 41? :)) ](https://bitcoin.stackexchange.com/questions/114168/where-are-bips-40-and-41)

4- [STRATUM V1 Docs](https://braiins.com/stratum-v1/docs#example)