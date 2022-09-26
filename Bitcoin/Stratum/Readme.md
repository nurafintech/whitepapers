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

# What's Stratum Protocol use case? [4]
I originally designed Stratum protocol for lightweight Bitcoin client called Electrum.
<br/>

## Stratum by simpilified manner
In a simplified manner, Stratum is a line-based protocol using plain TCP socket, with payload encoded as JSON-RPC messages. That's all. Client simply opens TCP socket and writes requests to the server in the form of JSON messages finished by the newline character \n. Every line received by the client is again a valid JSON-RPC fragment containing the response.

## It's very easy to implement and very easy to debug!
There are good reasons for such solution: it is very easy to implement and very easy to debug, because both sides are talking in human-readable format.
<br/>
The protocol is unlike many other solutions easily extensible **without messing up the backwards compatibility.**
<br/>

As a bonus, JSON is widely supported on all platforms and current miners already have JSON libraries included. So packing and unpacking of the message is really simple and convenient.
<br/>

## There is no HTTP overhead
There's no HTTP overhead involved and there're no hacks like mining extension flags encoded in HTTP headers anymore.
<br/>

But the biggest improvement from HTTP-based getwork is the fact, that server can drive the load by itself, it can send broadcast messages to miners at any time without any long-polling workarounds, load balancing issues and packet storms.


# Extranonce Rolling: The New Dimension [4]
This is probably the most innovative part of the new protocol. In contrary to current mining where only *ntime* and *nonce* can be iterated, **Stratum mining protocol gives a power to miners to easily build unique coinbase transactions locally, so they'll be able to produce unique block headers locally.**
<br/>

I recommend to iterate four bytes of extranonce, which gives the possibility to serve 18 EHash/s (Exa-hashes/s) mining rig from a single TCP connection. But it can be easily changed by the pool operator anytime.


# Technical Explanation [4]
Block header (that string what is in getwork response and what miners are hashing) is composed from following parts:
<li>
Block version, nbits, hash of previous block in the blockchain and some padding bytes, which are constants.
</li>
<li>Nonce and ntime, which miner can modify already.</li>
<li>Merkle root hash, which is created by hashing of bitcoin transactions included in the particular mining job.</li>

<br/>

## Produce More Unique Block Headers 
To produce more unique block headers (and thus be able to generate more unique hashes), we have to modify something.
<br/>

Every bitcoin block contains so-called coinbase transaction which specify the bitcoin address for sending block reward.
<br/>
Fortunately there's a chance to modify this transaction without breaking anything. **By changing coinbase transaction, merkle root will change and we will have unique block header to hash. Currently this (creating unique coinbase) happens on pool servers. So let's move it to miners!**
<br/>

## JSON Versus Your-Preferred-Protocol
I considered many solutions for serializing and deserializing message payloads. I wrote some reasons for JSON above, but let's sumarize them again:

<li>JSON payload is human readable, easy to implement and debug.</li>
<li>All bitcoin miners already have JSON libraries included. JSON has native support in almost every language.</li>
<li>In contrary of most binary protocol, JSON payload can be easily extended without breaking backward compatibility.</li>
<li>JSON-RPC already specifies three native message types which Stratum uses: request, response and notification. We don't need to reinvent a wheel.</li>
<li>JSON has definitely some data overhead, but Stratum mining messages typically fits into one TCP packet...</li>
<br/>

## Stratum Versus Getblocktemplate
Getblocktemplate introduced in bitcoind 0.7 is a very progressive solution for delegating block creation from full bitcoin client to standalone, specialized software.
<br/>
Stratum mining server uses getblocktemplate mechanism under the hood. There are still some reasons why Stratum is, in my opinion, a better solution for pooled mining:

<li>It is less complex, much easier to implement in existing miners and it still does the job perfectly.</li>

<li>For historical reasons getblocktemplate still uses HTTP protocol and long polling mechanism. I described above why this fails on large scale mining.</li>

<li>Stratum scales much better for rising amount of processed Bitcoin transactions, because it transfers only merkle branch hashes, in the contrary to complete dump of server’s memory pool in getblocktemplate.</li>






# Ethereum Stratum (EIP-1571) (To be continued...)
The main Stratum design flaw is the absence of a well defined standard. This implies that miners (and mining software developers) have to struggle with different flavours which make their life hard when switching from one pool to another or even when trying to “guess” which is the flavour implemented by a single pool. Moreover all implementations still suffer from an excessive verbosity for a chain with a very small block time like Ethereum. A few numbers may help understand. A normal mining.notify message weigh roughly 240 bytes: assuming the dispatch of 1 work per block to an audience of 50k connected TCP sockets means the transmission of roughly 1.88TB of data a month. And this can be an issue for large pools. But if we see the same figures the other way round, from a miner’s perspective, we totally understand how mining decentralization is heavily affected by the quality of internet connections.

# References

1- [[bitcoin-dev] [BIP] Stratum protocol specification](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2018-February/015728.html)

2- [Stratum mining protocol](https://en.bitcoin.it/wiki/Stratum_mining_protocol)

3- [Where are BIPs 40 and 41? :)) ](https://bitcoin.stackexchange.com/questions/114168/where-are-bips-40-and-41)

4- [STRATUM V1](https://braiins.com/stratum-v1/docs#example)

5- [Mastering Bitcoin - Second Edition](https://www.amazon.com/Mastering-Blockchain-Distributed-technology-decentralization/dp/1788839048)

6- [Stratum V2](https://braiins.com/stratum-v2)

7- [Ethereum Stratum (EIP-1571)](https://eips.ethereum.org/EIPS/eip-1571)