# Stratum
The stratum overlay protocol was extended to support pooled mining as a replacement for
obsolete **getwork protocol** in late 2012. The mining service specification was initially announced
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


# HTTP: Communication is Driven by Miners [4]
HTTP was designed for web site browsing where clients ask servers for specific content. **Pooled mining is different - server knows very well what clients need and can control the communication in a more efficient way.** 


# The Bitcoin Network [5]

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
<br/>

![](https://learn.saylor.org/pluginfile.php/3452313/mod_book/chapter/18897/image%20(1).png)

All nodes include the routing function to participate in the network and might
include other functionality.
# How is getwork? [4]
Strictly following getwork specification, one getwork job is enough for 4.2GHash/s mining rig and (thanks to ntime rolling) this job is usable for one minute or until a new Bitcoin block arrives (depending on what happens first).
<br/>
So, **for 42 GHash/s rig you’ll need 10 getwork requests at once, but usually a few more because of some pre-caching strategies implemented by miners to prevent idling on network latencies.** 
<br/>
And what about 1 THash/s ASIC miners coming soon? We simply need some solution where network load is not at all bounded to miners performance.

# Long Polling: An Anti-Pattern [4]
When pools came into the game, people found out that they must decide between short polling intervals (=higher network load, lower stale ratio) and intervals, which don't overload network and servers, but lead to a much higher ratio of rejected shares, and **long polling pattern was the answer.** 
<br/>
Long polling is a great way to achieve real-time updates using standard web technologies. But as I already mentioned in the text above, web technologies are not ideal for Bitcoin mining.<br/>
Long polling uses separate connection to pool server, which leads to various issues on server side, like load balancing of connections between more backends.
<br/>
<br/>
**Another problem consists of packet storms, coming from clients trying to reconnect to the server after long polling broadcasts. Sometimes it's hard to distinguish valid long polling reconnections from DDoS attacks.** All this makes pool architecture more complicated and harder to maintain, which is reflected in less reliable pool service and has a real impact on miners.

# What's Stratum Protocol use case?
I originally designed Stratum protocol for lightweight Bitcoin client called Electrum.
<br/>

## **Stratum by simpilified manner**
In a simplified manner, Stratum is a line-based protocol using plain TCP socket, with payload encoded as JSON-RPC messages. That's all. Client simply opens TCP socket and writes requests to the server in the form of JSON messages finished by the newline character \n. Every line received by the client is again a valid JSON-RPC fragment containing the response.


# Ethereum Stratum (EIP-1571)


# References

1- [[bitcoin-dev] [BIP] Stratum protocol specification](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-February/015728.html)

2- [Stratum mining protocol](https://en.bitcoin.it/wiki/Stratum_mining_protocol)

3- [Where are BIPs 40 and 41? :)) ](https://bitcoin.stackexchange.com/questions/114168/where-are-bips-40-and-41)

4- [STRATUM V1 Docs](https://braiins.com/stratum-v1/docs#example)

5- [Mastering Bitcoin](https://www.amazon.com/Mastering-Blockchain-Distributed-technology-decentralization/dp/1788839048)