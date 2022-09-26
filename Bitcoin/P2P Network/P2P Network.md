# P2P Network

The Bitcoin network protocol allows full nodes (peers) to collaboratively maintain a peer-to-peer network for block and transaction exchange.


## Map of the Bitcoin Network


The Bitcoin network is often described as peer-to-peer (P2P), distributed, or decentralized. It’s often drawn as a homogeneous graph:

* ![](https://miro.medium.com/max/265/1*1e88jDA0Lt6Cv31939Nu2Q.png)

Or something similarly structured that suggests variation in the types of vertices and edges:

*![](https://miro.medium.com/max/320/0*gPdbHV49mOckNwcb)

Primarily, the vertices are nodes in the P2P network and the edges are their P2P connections. There are many different types of nodes that can be categorized based on their ability to serve other peers and clients; nodes can act as a server, client, or both at any given point in time.

***Node*** = a participant on the P2P Network that implements the Bitcoin P2P protocol. A node isn’t required to run any specific software as long as it follows this protocol.

***P2P Connection*** = a network connection directly established between two nodes communicating using the Bitcoin P2P protocol. We often use “peer” to refer to other nodes with which a node has a P2P connection.

## Types of Nodes:
In the broadest sense, nodes fall into one of four categories based on how much state they maintain and what services they can provide.

***Full Node (Fully Validating Node)*** = a node that is capable of validating transactions and blocks. Instead of searching through the blocks database every time, full nodes keep some state, i.e. a UTXO (unspent transaction output or “coins”) set.

Thus, Bitcoin nodes don’t necessarily need a complete copy of the blockchain in order to validate, as long as they maintain some block metadata and an up-to-date UTXO set. **Pruning Nodes** implement this exact behavior: they download and process blocks to build the necessary databases for validation, then discard the old blocks to save disk space. Since they have all of the information and can validate all new blocks and transactions, they are full nodes.

<br>

**Archive Node** = a node that has a copy of the entire history of the blockchain. These nodes are capable of validating incoming transactions and blocks, as well as querying block and transaction data from any point in history, including those that are no longer relevant to validation (hence the naming “archive”). It’s crucial that archive nodes exist, as new nodes need to catch up on the entire history in order to become full nodes. They can only do so by downloading the history, one block at a time, from archive nodes.

**Mining Node** = a node that produces new blocks. This involves keeping a mempool of unconfirmed transactions, validating new transactions, and solving the Proof-of-Work hash puzzle (i.e. finding the nonce) to construct a block. Mining nodes often use extra hardware to assist them in solving the hash puzzle (e.g. ASICs) or participate in mining pools. Technically, there are also non-full nodes that join a mining pool, connect to a full node that manages the pool, and help solve PoW on a block without doing any validation (so there are mining but non-full nodes).

**Light Clients** = generic term for a node that doesn’t keep the full state necessary for full validation and instead trusts other full nodes to do so. A light client may keep a limited amount of data in order to verify its own transactions, but not fully validate all blocks. Within Bitcoin Core, “light client” is often used synonymously with **Simplified Payment Verification (SPV) Nodes**, and not to be confused with Pruning Nodes. In some contexts, these aren’t called “nodes” because they don’t do most of the things [full] nodes usually do.

A light node is bitcoin software that does not verify or enforce the rules of the bitcoin network. Light nodes trust third parties to receive block data.

SPV light nodes query and download block headers from full nodes, making it possible for users to verify transactions without running a full node.

Here is an illustration of how these categories overlap:

* ![](https://miro.medium.com/max/560/1*uDBzD2l4b0hVKXPa6pWHSA.png)

* ![](https://learn.saylor.org/pluginfile.php/3452313/mod_book/chapter/18897/image.png)

## Other Concepts for Nodes:
Nodes may also have additional characteristics that impact their participation on the network, but are not mutually exclusive with each other or any of the above four categories. Due to the decentralized nature and focus on accessibility in the Bitcoin ecosystem, **as long as a node implements the P2P protocol and obeys consensus rules**, implementation details and the decision to adopt features are within the node operator’s discretion.

**Initial Block Download (IBD)**: a temporary state in which the node is not yet caught up to the current block height and is in the process of downloading the blockchain. A full node signaling that it keeps a full copy of the blockchain history may still be in IBD and thus be limited in the services it can provide (i.e. won’t be able to tell you about transactions that they haven’t seen yet). The getblockchaininfo RPC returns whether a node is in IBD.

**Blocks Only Mode**: a non-temporary mode in which the full node only validates blocks and the transactions in them. It does not validate any unconfirmed transactions (apart from its own), doesn’t keep a mempool, and asks its peers not to relay transactions to it.

Bitcoin Core: running the open-source software originally authored by Satoshi Nakamoto and currently maintained by various contributors, found at bitcoincore.org. We know that Bitcoin Core isn’t the only software that exists in the Bitcoin P2P Network; some nodes run custom patches that implement specific behaviors, and some might use older versions of Bitcoin Core that don’t understand newly introduced protocol messages. It’s important to be cognizant of what new features require full network cooperation, not expect nodes to behave correctly or honestly, and account for node operators being hesitant or slow to upgrade their software.

Malicious: any type of behavior that intentionally harms the network (not including bugs, networking complications or other unintentional behavior). Bitcoin assumes a highly adversarial environment including the possibility of Denial of Service attacks, sybil/eclipse-attacks intended to double-spend, spy nodes trying to deanonymize addresses, etc.


## Node as a Server

Full nodes are nodes that maintain a full blockchain with all transactions. More accurately, they probably should be called "full blockchain nodes". In the early years of bitcoin, all nodes were full nodes and currently the Bitcoin Core client is a full blockchain node. In the past two years, however, new forms of bitcoin clients have been introduced that do not maintain a full blockchain but run as lightweight clients. We’ll examine these in more detail in the next section.

Full blockchain nodes maintain a complete and up-to-date copy of the bitcoin blockchain with all the transactions, which they independently build and verify, starting with the very first block (genesis block) and building up to the latest known block in the network. A full blockchain node can independently and authoritatively verify any transaction without recourse or reliance on any other node or source of information. The full blockchain node relies on the network to receive updates about new blocks of transactions, which it then verifies and incorporates into its local copy of the blockchain.

Running a full blockchain node gives you the pure bitcoin experience: independent verification of all transactions without the need to rely on, or trust, any other systems. It’s easy to tell if you’re running a full node because it requires more than one hundred gigabytes of persistent storage (disk space) to store the full blockchain. If you need a lot of disk and it takes two to three days to sync to the network, you are running a full node. That is the price of complete independence and freedom from central authority.

There are a few alternative implementations of full blockchain bitcoin clients, built using different programming languages and software architectures. However, the most common implementation is the reference client Bitcoin Core, also known as the Satoshi client. More than 75% of the nodes on the bitcoin network run various versions of Bitcoin Core. It is identified as "Satoshi" in the sub-version string sent in the version message and shown by the command getpeerinfo as we saw earlier; for example, /Satoshi:0.8.6/ .

We’ve seen that each singular node is dependent on its peers to send the information it needs. Also, nodes typically serve a number of users and client software through non-P2P interfaces such as RPC, HTTP/REST, and a GUI.

Some examples of non-node clients that may use a node as a server:

* <b>Users</b> running a node to send and receive bitcoins.
* <b>Wallets</b> which manage keys, create transactions, and maybe keep some UTXO state associated with those keys but don’t have a copy of the blockchain and instead rely on a node to get up-to-date information.
* <b>User-Facing</b> Software Services and Applications such as block explorers, exchanges, and merchants that query full nodes for information and display them on a webpage or application.
* </b>Developers</b> creating nodes in regtest mode to test functionality or the interfaces themselves.
* </b>Developer-Facing Software</b> such as SDKs, APIs, and other interfaces. For example, the Bitcoin Core CLI (bitcoin-cli) uses the RPC interface to implement a command-line interface.
While these connections are not seen by a node’s peers on the P2P Network, they make up a significant portion of Bitcoin functionality. Bitcoin Core developers heavily consider these participants when developing new features or deciding what features to support.

While these connections are not seen by a node’s peers on the P2P Network, they make up a significant portion of Bitcoin functionality. Bitcoin Core developers heavily consider these participants when developing new features or deciding what features to support.

Now that we understand the node as both a server and a client, here’s what an individual node looks like at a high level:

* ![](https://miro.medium.com/max/560/1*iEogUm4NwkqGjWH35u9gig.png)

## Types of P2P connections:
P2P connections in Bitcoin all “speak the same language” in that they all use the P2P protocol to communicate, but are diverse in their conversation contents. The Bitcoin Core implementation attempts to balance stability (which prefers static connections) and accessibility (which encourages accepting connections from new nodes) through facilitating peer discovery and managing connections carefully. Bitcoin Core distinguishes between three main types of connections based on how they are initiated, which often informs the nature of the peer-to-peer relationship.

**Outbound** = automatic connection that your node initiated through peer discovery. Node discovery involves getting a list of IP addresses of established nodes to start out with, then a continuous and dynamic process of advertising your own address and attempting to connect to addresses you hear about. Depending on what your node needs (e.g. in IBD), it may prioritize connections that are able to provide specific services (e.g. serving past blocks and transactions).

**Inbound** = automatic connection that your peer initiated (to your peer, this connection is outbound). For security, inbound traffic is disabled by default and you need to configure some network and firewall settings to enable it.

**Manual** = connection that was made manually (e.g. through CLI or RPC) instead of automatically. You might create a manual connection because there’s a particular node operated by someone you trust or you’re testing the software and need to have control over the connections.

## Other Concepts for P2P Connections:

### Diversity in Outbound Connections

Outbound connections can be broken down into further categories based on the information received and duration of the connection.

**Full-Relay** outbound connections expect to communicate everything, including blocks, transactions, and addrs (used to find peers, similar to IP addresses, and not to be confused with wallet addresses used in transactions). **Block-Only-Relay** outbound connections only expect to receive blocks. Not to be confused with blocks-only mode; it is entirely normal for full nodes to establish Block-Only-Relay connections to 1–2 peers and Full-Relay connections to everyone else.

**One-Shot and Feelers** are temporary outbound connections used in node discovery. One-Shot connections are used to solicit a list of addrs that can be used to find new peers. Feelers are used to verify whether an addr corresponds to a real node.

### Individual Differences

As we have seen, each node may provide different services and be looking for specific information from its peers. Every connection starts with a version handshake in which the nodes send information about themselves (e.g. best block height) and negotiate what to talk about (e.g. only interested in blocks). Connections may also change through subsequent messages, such as a fee filter message to communicate that they’re only interested in being relayed transactions with a minimum fee rate.

### Discouragement, Disconnection, and Banning

Bitcoin Core nodes keep track of which peers behave in a way that indicates they may be malicious or running malfunctioning software. In response to such behavior, a node might choose to discourage (mark its misbehavior and perhaps disconnect in favor of new peers), disconnect, or ban the peer.

### Permissions and Whitelist

Nodes also keep a list of permissions that each peer has, such as particular services it’s allowed to request or tolerance for misbehavior that would normally be penalized. Services are negotiated for every connection during the version handshake. Allowing misbehavior is often manually added for custom, personal light clients and nodes operated by people that trust each other. Related, nodes can also whitelist particular IP addresses.

### Importance of Asymmetry

Note that each individual connection is bidirectional but asymmetric: the initiating peer may understand the connection to be a [full-relay] outbound, block-only-relay, feeler, or one-shot, but the receiving peer just sees an inbound connection with some established rules. This hides information through ambiguity about whether a node’s behavior reveals its internal mechanics or merely reflects the nature of the connection.

For example, if a node knows that its peer is in blocksonly mode (i.e. rejects all incoming transaction messages), it is obvious that all transactions sent from that peer correspond to its own wallet addresses. Instead, the receiving node just sees an inbound connection with transaction relay turned off. This could mean blocksonly mode, block-relay-only connection, or an idiosyncrasy of the connection.

A more detailed view of an individual node could look like this (note that the arrows’ directions just indicate which node initiates, not that the communication isn’t bidirectional):

* ![](https://miro.medium.com/max/560/1*Y1R9SqPb_CWPTyvBQg9kfw.png) 

<br>

## “Full” Map
Each node has limited information about the network as a whole. Nodes really only see their own peers, and peers could be lying about what type of node they are. All peers could even be the same person in the event of an eclipse attack. This is an advantage for privacy and security because it applies to adversaries as well; having limited information makes targeted attacks more difficult. It’s possible to gather approximate information about how many nodes are in the network by creating lots of temporary connections, but this information is far from comprehensive.

For example, whether or not a node participates in a mining pool isn’t immediately apparent on the network. With approximate knowledge about which nodes are part of mining pools and observing how many blocks they mine, some websites are able to generate analytics on computing power proportions. However, they can be misleading as it is entirely possible for groups of nodes or even multiple mining pools to be operated by one entity.

Putting it all together, we can imagine this simplified network map:

* ![](https://miro.medium.com/max/560/1*v2njpHCpwB6hO7DNK8Z7-g.png)

* ![](https://learn.saylor.org/pluginfile.php/3452313/mod_book/chapter/18897/image%20%281%29.png)

This map represents various possibilities instead of network size (which is very large) or topology (which is dynamic and unknown). Notice that the possibilities include:

* A Bitcoin Core full node with various clients connected via non-P2P interfaces, e.g. a user that downloaded the software from bitcoincore.org and is using the command-line or GUI to send and receive coins.
* Light clients that do their best to connect to a variety of full nodes in order to serve its own clients.
* A full node serving one or more light clients, perhaps an individual Bitcoin enthusiast who runs a full node using some cloud service provider and a more lightweight application on their personal device.
* A custom full node (e.g. a pool manager) connected to a group of custom light clients (e.g. individual pool participants) through both the P2P network and some private network.

#

## Network Discovery

When a new node boots up, it must discover other bitcoin nodes on the network in order to participate. To start this process, a new node must discover at least one existing node on the network and connect to it. The geographic location of other nodes is irrelevant; the bitcoin network topology is not geographically defined. Therefore, any existing bitcoin nodes can be selected at random.

To connect to a known peer, nodes establish a TCP connection, usually to port 8333 (the port generally known as the one used by bitcoin), or an alternative port if one is provided. Upon establishing a connection, the node will start a "handshake" (see The initial handshake between peers) by transmitting a version message, which contains basic identifying information, including:

<dt>
<dl>
<b>nVersion</b>
<dl>
<dd>
The bitcoin P2P protocol version the client "speaks" (e.g., 70002)
</dd>
<dl>
<b>nLocalServices</b>
<dl>
<dd>
A list of local services supported by the node, currently just NODE_NETWORK
</dd>
<dl>
<b>nTime</b>
<dl>
<dd>
The current time
</dd>
<dl>
<b>addrYou</b>
<dl>
<dd>
The IP address of the remote node as seen from this node
</dd>
<dl>
<b>addrMe</b>
<dl>
<dd>
The IP address of the local node, as discovered by the local node
</dd>
<dl>
<b>subver</b>
<dl>
<dd>
A sub-version showing the type of software running on this node (e.g., /Satoshi:0.9.2.1/)
</dd>
<dl>
<b>BestHeight</b>
<dl>
<dd>
The block height of this node's blockchain
</dd>
</dt>

The version message is always the first message sent by any peer to another peer. The local peer receiving a version message will examine the remote peer's reported nVersion and decide if the remote peer is compatible. If the remote peer is compatible, the local peer will acknowledge the version message and establish a connection by sending a verack message.

How does a new node find peers? The first method is to query DNS using a number of "DNS seeds," which are DNS servers that provide a list of IP addresses of bitcoin nodes. Some of those DNS seeds provide a static list of IP addresses of stable bitcoin listening nodes. Some of the DNS seeds are custom implementations of BIND (Berkeley Internet Name Daemon) that return a random subset from a list of bitcoin node addresses collected by a crawler or a long-running bitcoin node. The Bitcoin Core client contains the names of nine different DNS seeds. The diversity of ownership and diversity of implementation of the different DNS seeds offers a high level of reliability for the initial bootstrapping process. In the Bitcoin Core client, the option to use the DNS seeds is controlled by the option switch -dnsseed (set to 1 by default, to use the DNS seed).

Alternatively, a bootstrapping node that knows nothing of the network must be given the IP address of at least one bitcoin node, after which it can establish connections through further introductions. The command-line argument -seednode can be used to connect to one node just for introductions using it as a seed. After the initial seed node is used to form introductions, the client will disconnect from it and use the newly discovered peers.

![](https://learn.saylor.org/pluginfile.php/3452313/mod_book/chapter/18899/image.png)

Once one or more connections are established, the new node will send an addr message containing its own IP address to its neighbors. The neighbors will, in turn, forward the addr message to their neighbors, ensuring that the newly connected node becomes well known and better connected. Additionally, the newly connected node can send getaddr to the neighbors, asking them to return a list of IP addresses of other peers. That way, a node can find peers to connect to and advertise its existence on the network for other nodes to find it. Address propagation and discovery shows the address discovery protocol.

![](https://learn.saylor.org/pluginfile.php/3452313/mod_book/chapter/18899/image%20%281%29.png)


A node must connect to a few different peers in order to establish diverse paths into the bitcoin network. Paths are not persistent - nodes come and go - and so the node must continue to discover new nodes as it loses old connections as well as assist other nodes when they bootstrap. Only one connection is needed to bootstrap, because the first node can offer introductions to its peer nodes and those peers can offer further introductions. It's also unnecessary and wasteful of network resources to connect to more than a handful of nodes. After bootstrapping, a node will remember its most recent successful peer connections, so that if it is rebooted it can quickly reestablish connections with its former peer network. If none of the former peers respond to its connection request, the node can use the seed nodes to bootstrap again.

On a node running the Bitcoin Core client, you can list the peer connections with the command getpeerinfo:

<pre> $ bitcoin-cli getpeerinfo </pre>

[
    {
        "addr" : "85.213.199.39:8333",
        "services" : "00000001",
        "lastsend" : 1405634126,
        "lastrecv" : 1405634127,
        "bytessent" : 23487651,
        "bytesrecv" : 138679099,
        "conntime" : 1405021768,
        "pingtime" : 0.00000000,
        "version" : 70002,
        "subver" : "/Satoshi:0.9.2.1/",
        "inbound" : false,
        "startingheight" : 310131,
        "banscore" : 0,
        "syncnode" : true
    },
    {
        "addr" : "58.23.244.20:8333",
        "services" : "00000001",
        "lastsend" : 1405634127,
        "lastrecv" : 1405634124,
        "bytessent" : 4460918,
        "bytesrecv" : 8903575,
        "conntime" : 1405559628,
        "pingtime" : 0.00000000,
        "version" : 70001,
        "subver" : "/Satoshi:0.8.6/",
        "inbound" : false,
        "startingheight" : 311074,
        "banscore" : 0,
        "syncnode" : false
    }
]

To override the automatic management of peers and to specify a list of IP addresses, users can provide the option -connect=\<IPAddress\>  and specify one or more IP addresses. If this option is used, the node will only connect to the selected IP addresses, instead of discovering and maintaining the peer connections automatically.

If there is no traffic on a connection, nodes will periodically send a message to maintain the connection. If a node has not communicated on a connection for more than 90 minutes, it is assumed to be disconnected and a new peer will be sought. Thus, the network dynamically adjusts to transient nodes and network problems, and can organically grow and shrink as needed without any central control.

## Exchanging "Inventory"

The first thing a full node will do once it connects to peers is try to construct a complete blockchain. If it is a brand-new node and has no blockchain at all, it only knows one block, the genesis block, which is statically embedded in the client software. Starting with block #0 (the genesis block), the new node will have to download hundreds of thousands of blocks to synchronize with the network and reestablish the full blockchain.

The process of syncing the blockchain starts with the version message, because that contains BestHeight, a node's current blockchain height (number of blocks). A node will see the version messages from its peers, know how many blocks they each have, and be able to compare to how many blocks it has in its own blockchain. Peered nodes will exchange a getblocks message that contains the hash (fingerprint) of the top block on their local blockchain. One of the peers will be able to identify the received hash as belonging to a block that is not at the top, but rather belongs to an older block, thus deducing that its own local blockchain is longer than its peer's.

The peer that has the longer blockchain has more blocks than the other node and can identify which blocks the other node needs in order to "catch up." It will identify the first 500 blocks to share and transmit their hashes using an inv (inventory) message. The node missing these blocks will then retrieve them, by issuing a series of getdata messages requesting the full block data and identifying the requested blocks using the hashes from the inv message.

Let's assume, for example, that a node only has the genesis block. It will then receive an inv message from its peers containing the hashes of the next 500 blocks in the chain. It will start requesting blocks from all of its connected peers, spreading the load and ensuring that it doesn't overwhelm any peer with requests. The node keeps track of how many blocks are "in transit" per peer connection, meaning blocks that it has requested but not received, checking that it does not exceed a limit (MAX_BLOCKS_IN_TRANSIT_PER_PEER). This way, if it needs a lot of blocks, it will only request new ones as previous requests are fulfilled, allowing the peers to control the pace of updates and not overwhelm the network. As each block is received, it is added to the blockchain, as we will see in [blockchain]. As the local blockchain is gradually built up, more blocks are requested and received, and the process continues until the node catches up to the rest of the network.

This process of comparing the local blockchain with the peers and retrieving any missing blocks happens any time a node goes offline for any period of time. Whether a node has been offline for a few minutes and is missing a few blocks, or a month and is missing a few thousand blocks, it starts by sending getblocks, gets an inv response, and starts downloading the missing blocks. Node synchronizing the blockchain by retrieving blocks from a peer shows the inventory and block propagation protocol.

![](https://learn.saylor.org/pluginfile.php/3452313/mod_book/chapter/18901/image.png)


# 

## A Deeper Dive

Full nodes download and verify every block and transaction prior to relaying them to other nodes. Archival nodes are full nodes which store the entire blockchain and can serve historical blocks to other nodes. Pruned nodes are full nodes which do not store the entire blockchain. Many SPV clients also use the Bitcoin network protocol to connect to full nodes.

Consensus rules do not cover networking, so Bitcoin programs may use alternative networks and protocols, such as the high-speed block relay network used by some miners and the dedicated transaction information servers used by some wallets that provide SPV-level security.

To provide practical examples of the Bitcoin peer-to-peer network, this section uses Bitcoin Core as a representative full node and BitcoinJ as a representative SPV client. Both programs are flexible, so only default behavior is described. Also, for privacy, actual IP addresses in the example output below have been replaced with RFC5737 reserved IP addresses.

## Peer Discovery
When started for the first time, programs don’t know the IP addresses of any active full nodes. In order to discover some IP addresses, they query one or more DNS names (called DNS seeds) hardcoded into Bitcoin Core and BitcoinJ. The response to the lookup should include one or more DNS A records with the IP addresses of full nodes that may accept new incoming connections. For example, using the Unix ***dig*** command.

#### dig (command)
dig is a network administration command-line tool for querying the Domain Name System (DNS).
dig ( Domain Information Groper) is useful for network troubleshooting and for educational purposes. It can operate based on command line option and flag arguments, or in batch mode by reading requests from an operating system file. When a specific name server is not specified in the command invocation, it uses the operating system's default resolver, usually configured in the file resolv.conf. Without any arguments it queries the DNS root zone.

dig supports Internationalized domain name (IDN) queries.

dig is a component of the domain name server software suite BIND. dig supersedes in functionality older tools, such as nslookup and the program host; however, the older tools are still used in complementary fashion.

<pre> ;; QUESTION SECTION:
;seed.bitcoin.sipa.be.      IN  A

;; ANSWER SECTION:
seed.bitcoin.sipa.be.   60  IN  A  192.0.2.113
seed.bitcoin.sipa.be.   60  IN  A  198.51.100.231
seed.bitcoin.sipa.be.   60  IN  A  203.0.113.183
[...] </pre>

The DNS seeds are maintained by Bitcoin community members: some of them provide dynamic DNS seed servers which automatically get IP addresses of active nodes by scanning the network; others provide static DNS seeds that are updated manually and are more likely to provide IP addresses for inactive nodes. In either case, nodes are added to the DNS seed if they run on the default Bitcoin ports of 8333 for mainnet or 18333 for testnet.

DNS seed results are not authenticated and a malicious seed operator or network man-in-the-middle attacker can return only IP addresses of nodes controlled by the attacker, isolating a program on the attacker’s own network and allowing the attacker to feed it bogus transactions and blocks. For this reason, programs should not rely on DNS seeds exclusively.

Once a program has connected to the network, its peers can begin to send it ***addr*** (address) messages with the IP addresses and port numbers of other peers on the network, providing a fully decentralized method of peer discovery. Bitcoin Core keeps a record of known peers in a persistent on-disk database which usually allows it to connect directly to those peers on subsequent startups without having to use DNS seeds.

However, peers often leave the network or change IP addresses, so programs may need to make several different connection attempts at startup before a successful connection is made. This can add a significant delay to the amount of time it takes to connect to the network, forcing a user to wait before sending a transaction or checking the status of payment.

To avoid this possible delay, BitcoinJ always uses dynamic DNS seeds to get IP addresses for nodes believed to be currently active. Bitcoin Core also tries to strike a balance between minimizing delays and avoiding unnecessary DNS seed use: if Bitcoin Core has entries in its peer database, it spends up to 11 seconds attempting to connect to at least one of them before falling back to seeds; if a connection is made within that time, it does not query any seeds.

Both Bitcoin Core and BitcoinJ also include a hardcoded list of IP addresses and port numbers to several dozen nodes which were active around the time that particular version of the software was first released. Bitcoin Core will start attempting to connect to these nodes if none of the DNS seed servers have responded to a query within 60 seconds, providing an automatic fallback option.

As a manual fallback option, Bitcoin Core also provides several command-line connection options, including the ability to get a list of peers from a specific node by IP address, or to make a persistent connection to a specific node by IP address. See the -help text for details. BitcoinJ can be programmed to do the same thing.

## Connecting To Peers
Connecting to a peer is done by sending a “version” message, which contains your version number, block, and current time to the remote node. The remote node responds with its own “version” message. Then both nodes send a “verack” message to the other node to indicate the connection has been established.

Once connected, the client can send to the remote node ***getaddr*** and “addr” messages to gather additional peers.

In order to maintain a connection with a peer, nodes by default will send a message to peers before 30 minutes of inactivity. If 90 minutes pass without a message being received by a peer, the client will assume that connection has closed.

## Initial Block Download

Initial Block Download
Before a full node can validate unconfirmed transactions and recently-mined blocks, it must download and validate all blocks from block 1 (the block after the hardcoded genesis block) to the current tip of the best block chain. This is the Initial Block Download (IBD) or initial sync.

Although the word “initial” implies this method is only used once, it can also be used any time a large number of blocks need to be downloaded, such as when a previously-caught-up node has been offline for a long time. In this case, a node can use the IBD method to download all the blocks which were produced since the last time it was online.

Bitcoin Core uses the IBD method any time the last block on its local best block chain has a block header time more than 24 hours in the past. Bitcoin Core 0.10.0 will also perform IBD if its local best block chain is more than 144 blocks lower than its local best header chain (that is, the local block chain is more than about 24 hours in the past).

## Blocks-First

Bitcoin Core (up until version 0.9.3) uses a simple initial block download (IBD) method we’ll call blocks-first. The goal is to download the blocks from the best block chain in sequence.
* ![](https://developer.bitcoin.org/_images/en-blocks-first-flowchart.svg)

The first time a node is started, it only has a single block in its local best block chain—the hardcoded genesis block (block 0). This node chooses a remote peer, called the sync node, and sends it the “getblocks” message illustrated below.

* ![](https://developer.bitcoin.org/_images/en-ibd-getblocks.svg)

In the header hashes field of the “getblocks” message, this new node sends the header hash of the only block it has, the genesis block (6fe2…0000 in internal byte order). It also sets the stop hash field to all zeroes to request a maximum-size response.

Upon receipt of the “getblocks” message, the sync node takes the first (and only) header hash and searches its local best block chain for a block with that header hash. It finds that block 0 matches, so it replies with 500 block inventories (the maximum response to a “getblocks” message) starting from block 1. It sends these inventories in the “inv” message illustrated below.

* ![](https://developer.bitcoin.org/_images/en-ibd-inv.svg)

Inventories are unique identifiers for information on the network. Each inventory contains a type field and the unique identifier for an instance of the object. For blocks, the unique identifier is a hash of the block’s header.

The block inventories appear in the “inv” message in the same order they appear in the block chain, so this first “inv” message contains inventories for blocks 1 through 501. (For example, the hash of block 1 is 4860…0000 as seen in the illustration above.)

The IBD node uses the received inventories to request 128 blocks from the sync node in the “getdata” message illustrated below.

* ![](https://developer.bitcoin.org/_images/en-ibd-getdata.svg)

It’s important to blocks-first nodes that the blocks be requested and sent in order because each block header references the header hash of the preceding block. That means the IBD node can’t fully validate a block until its parent block has been received. Blocks that can’t be validated because their parents haven’t been received are called orphan blocks; a subsection below describes them in more detail.

Upon receipt of the “getdata” message, the sync node replies with each of the blocks requested. Each block is put into serialized block format and sent in a separate “block” message. The first “block” message sent (for block 1) is illustrated below.

* ![](https://developer.bitcoin.org/_images/en-ibd-block.svg)

The IBD node downloads each block, validates it, and then requests the next block it hasn’t requested yet, maintaining a queue of up to 128 blocks to download. When it has requested every block for which it has an inventory, it sends another “getblocks” message to the sync node requesting the inventories of up to 500 more blocks. This second “getblocks” message contains multiple header hashes as illustrated below:

* ![](https://developer.bitcoin.org/_images/en-ibd-getblocks2.svg)

Upon receipt of the second “getblocks” message, the sync node searches its local best block chain for a block that matches one of the header hashes in the message, trying each hash in the order they were received. If it finds a matching hash, it replies with 500 block inventories starting with the next block from that point. But if there is no matching hash (besides the stopping hash), it assumes the only block the two nodes have in common is block 0 and so it sends an inv starting with block 1 (the same “inv” message seen several illustrations above).

This repeated search allows the sync node to send useful inventories even if the IBD node’s local block chain forked from the sync node’s local block chain. This fork detection becomes increasingly useful the closer the IBD node gets to the tip of the block chain.

When the IBD node receives the second “inv” message, it will request those blocks using “getdata” messages. The sync node will respond with “block” messages. Then the IBD node will request more inventories with another “getblocks” message—and the cycle will repeat until the IBD node is synced to the tip of the block chain. At that point, the node will accept blocks sent through the regular block broadcasting described in a later subsection.

## Blocks-First Advantages & Disadvantages

The primary advantage of blocks-first IBD is its simplicity. The primary disadvantage is that the IBD node relies on a single sync node for all of its downloading. This has several implications:

* Speed Limits: All requests are made to the sync node, so if the sync node has limited upload bandwidth, the IBD node will have slow download speeds. Note: if the sync node goes offline, Bitcoin Core will continue downloading from another node—but it will still only download from a single sync node at a time.

* Download Restarts: The sync node can send a non-best (but otherwise valid) block chain to the IBD node. The IBD node won’t be able to identify it as non-best until the initial block download nears completion, forcing the IBD node to restart its block chain download over again from a different node. Bitcoin Core ships with several block chain checkpoints at various block heights selected by developers to help an IBD node detect that it is being fed an alternative block chain history—allowing the IBD node to restart its download earlier in the process.

* Disk Fill Attacks: Closely related to the download restarts, if the sync node sends a non-best (but otherwise valid) block chain, the chain will be stored on disk, wasting space and possibly filling up the disk drive with useless data.

* High Memory Use: Whether maliciously or by accident, the sync node can send blocks out of order, creating orphan blocks which can’t be validated until their parents have been received and validated. Orphan blocks are stored in memory while they await validation, which may lead to high memory use.

The table below summarizes the messages mentioned throughout this subsection. The links in the message field will take you to the reference page for that message.

| Message      | From → To | Payload |
| ----------- | ----------- | ----------- |
| “getblocks”  |IBD → Sync  | One or more header hashes |
| “inv” | Sync → IBD  |  Up to 500 block inventories (unique identifiers) |
| “getdata”  | IBD → Sync  | One or more block inventories |
| “block”  | Sync → IBD  | One serialized block |


## Headers-First

Bitcoin Core 0.10.0 uses an initial block download (IBD) method called headers-first. The goal is to download the headers for the best header chain, partially validate them as best as possible, and then download the corresponding blocks in parallel. This solves several problems with the older blocks-first IBD method.

* ![](https://developer.bitcoin.org/_images/en-headers-first-flowchart.svg)

The first time a node is started, it only has a single block in its local best block chain—the hardcoded genesis block (block 0). The node chooses a remote peer, which we’ll call the sync node, and sends it the “getheaders” message illustrated below.

* ![](https://developer.bitcoin.org/_images/en-ibd-getheaders.svg)

In the header hashes field of the “getheaders” message, the new node sends the header hash of the only block it has, the genesis block (6fe2…0000 in internal byte order). It also sets the stop hash field to all zeroes to request a maximum-size response.

Upon receipt of the “getheaders” message, the sync node takes the first (and only) header hash and searches its local best block chain for a block with that header hash. It finds that block 0 matches, so it replies with 2,000 header (the maximum response) starting from block 1. It sends these header hashes in the “headers” message illustrated below.

* ![](https://developer.bitcoin.org/_images/en-ibd-headers.svg)

The IBD node can partially validate these block headers by ensuring that all fields follow consensus rules and that the hash of the header is below the target threshold according to the nBits field. (Full validation still requires all transactions from the corresponding block.)

After the IBD node has partially validated the block headers, it can do two things in parallel:

1. Download More Headers: the IBD node can send another “getheaders” message to the sync node to request the next 2,000 headers on the best header chain. Those headers can be immediately validated and another batch requested repeatedly until a “headers” message is received from the sync node with fewer than 2,000 headers, indicating that it has no more headers to offer. As of this writing, headers sync can be completed in fewer than 200 round trips, or about 32 MB of downloaded data.<br><br>
Once the IBD node receives a “headers” message with fewer than 2,000 headers from the sync node, it sends a “getheaders” message to each of its outbound peers to get their view of best header chain. By comparing the responses, it can easily determine if the headers it has downloaded belong to the best header chain reported by any of its outbound peers. This means a dishonest sync node will quickly be discovered even if checkpoints aren’t used (as long as the IBD node connects to at least one honest peer; Bitcoin Core will continue to provide checkpoints in case honest peers can’t be found).

2. Download Blocks: While the IBD node continues downloading headers, and after the headers finish downloading, the IBD node will request and download each block. The IBD node can use the block header hashes it computed from the header chain to create “getdata” messages that request the blocks it needs by their inventory. It doesn’t need to request these from the sync node—it can request them from any of its full node peers. (Although not all full nodes may store all blocks.) This allows it to fetch blocks in parallel and avoid having its download speed constrained to the upload speed of a single sync node.<br><br>
To spread the load between multiple peers, Bitcoin Core will only request up to 16 blocks at a time from a single peer. Combined with its maximum of 8 outbound connections, this means headers-first Bitcoin Core will request a maximum of 128 blocks simultaneously during IBD (the same maximum number that blocks-first Bitcoin Core requested from its sync node).

* ![](https://developer.bitcoin.org/_images/en-headers-first-moving-window.svg)

Bitcoin Core’s headers-first mode uses a 1,024-block moving download window to maximize download speed. The lowest-height block in the window is the next block to be validated; if the block hasn’t arrived by the time Bitcoin Core is ready to validate it, Bitcoin Core will wait a minimum of two more seconds for the stalling node to send the block. If the block still hasn’t arrived, Bitcoin Core will disconnect from the stalling node and attempt to connect to another node. For example, in the illustration above, Node A will be disconnected if it doesn’t send block 3 within at least two seconds.

Once the IBD node is synced to the tip of the block chain, it will accept blocks sent through the regular block broadcasting described in a later subsection.

The table below summarizes the messages mentioned throughout this subsection. The links in the message field will take you to the reference page for that message.

| Message      | From → To | Payload |
| ----------- | ----------- | ----------- |
| “getheaders”  |IBD → Sync  | One or more header hashes |
| “inv” | Sync → IBD  | Up to 2,000 block headers) |
| “getdata”  | IBD → Many  | One or more block inventories derived from header hashes |
| “block”  | Many → IBD  | One serialized block |


## Block Broadcasting
When a miner discovers a new block, it broadcasts the new block to its peers using one of the following methods:

* Unsolicited Block Push: the miner sends a “block” message to each of its full node peers with the new block. The miner can reasonably bypass the standard relay method in this way because it knows none of its peers already have the just-discovered block.

* Standard Block Relay: the miner, acting as a standard relay node, sends an “inv” message to each of its peers (both full node and SPV) with an inventory referring to the new block. The most common responses are:
    * Each blocks-first (BF) peer that wants the block replies with a “getdata” message requesting the full block.
    * Each headers-first (HF) peer that wants the block replies with a “getheaders” message containing the header hash of the highest-height header on its best header chain, and likely also some headers further back on the best header chain to allow fork detection. That message is immediately followed by a “getdata” message requesting the full block. By requesting headers first, a headers-first peer can refuse orphan blocks as described in the subsection below.
    * Each Simplified Payment Verification (SPV) client that wants the block replies with a “getdata” message typically requesting a merkle block.

    The miner replies to each request accordingly by sending the block in a “block” message, one or more headers in a “headers” message, or the merkle block and transactions relative to the SPV client’s bloom filter in a “merkleblock” message followed by zero or more “tx” messages.

* Direct Headers Announcement: a relay node may skip the round trip overhead of an “inv” message followed by getheaders by instead immediately sending a “headers” message containing the full header of the new block. A HF peer receiving this message will partially validate the block header as it would during headers-first IBD, then request the full block contents with a “getdata” message if the header is valid. The relay node then responds to the getdata request with the full or filtered block data in a block or “merkleblock” message, respectively. A HF node may signal that it prefers to receive headers instead of inv announcements by sending a special “sendheaders” message during the connection handshake.

By default, Bitcoin Core broadcasts blocks using direct headers announcement to any peers that have signalled with “sendheaders” and uses standard block relay for all peers that have not. Bitcoin Core will accept blocks sent using any of the methods described above.

Full nodes validate the received block and then advertise it to their peers using the standard block relay method described above. The condensed table below highlights the operation of the messages described above (Relay, BF, HF, and SPV refer to the relay node, a blocks-first node, a headers-first node, and an SPV client; any refers to a node using any block retrieval method.)

<table class="docutils align-default table table-sm table-bordered table-striped">
<colgroup>
<col style="width: 47%">
<col style="width: 10%">
<col style="width: 43%">
</colgroup>
<thead class="thead-inverse">
<tr class="row-odd"><th class="head"><p>Message</p></th>
<th class="head"><p>From → To</p></th>
<th class="head"><p>Payload</p></th>
</tr>
</thead>
<tbody>
<tr class="row-even"><td><p><a class="reference external" >“getheaders”</a></p></td>
<td><p>IBD → Sync</p></td>
<td><p>One or more header hashes</p></td>
</tr>
<tr class="row-odd"><td><p><a class="reference external">“headers”</a></p></td>
<td><p>Sync → IBD</p></td>
<td><p>Up to 2,000 block headers</p></td>
</tr>
<tr class="row-even"><td><p><a class="reference external" >“getdata”</a></p></td>
<td><p>IBD → <em>Many</em></p></td>
<td><p>One or more block inventories derived from header hashes</p></td>
</tr>
<tr class="row-odd"><td><p><a class="reference external">“block”</a></p></td>
<td><p><em>Many</em> → IBD</p></td>
<td><p>One serialized block</p></td>
</tr>
</tbody>
</table>

## Orphan Blocks
Blocks-first nodes may download orphan blocks—blocks whose previous block header hash field refers to a block header this node hasn’t seen yet. In other words, orphan blocks have no known parent (unlike stale blocks, which have known parents but which aren’t part of the best block chain).

* ![](https://developer.bitcoin.org/_images/en-orphan-stale-definition.svg)

When a blocks-first node downloads an orphan block, it will not validate it. Instead, it will send a “getblocks” message to the node which sent the orphan block; the broadcasting node will respond with an “inv” message containing inventories of any blocks the downloading node is missing (up to 500); the downloading node will request those blocks with a “getdata” message; and the broadcasting node will send those blocks with a “block” message. The downloading node will validate those blocks, and once the parent of the former orphan block has been validated, it will validate the former orphan block.

Headers-first nodes avoid some of this complexity by always requesting block headers with the “getheaders” message before requesting a block with the “getdata” message. The broadcasting node will send a “headers” message containing all the block headers (up to 2,000) it thinks the downloading node needs to reach the tip of the best header chain; each of those headers will point to its parent, so when the downloading node receives the “block” message, the block shouldn’t be an orphan block—all of its parents should be known (even if they haven’t been validated yet). If, despite this, the block received in the “block” message is an orphan block, a headers-first node will discard it immediately.

However, orphan discarding does mean that headers-first nodes will ignore orphan blocks sent by miners in an unsolicited block push.

## Transaction Broadcasting

In order to send a transaction to a peer, an “inv” message is sent. If a ***getdata*** response message is received, the transaction is sent using ***tx***. The peer receiving this transaction also forwards the transaction in the same manner, given that it is a valid transaction.

## Memory Pool
Full peers may keep track of unconfirmed transactions which are eligible to be included in the next block. This is essential for miners who will actually mine some or all of those transactions, but it’s also useful for any peer who wants to keep track of unconfirmed transactions, such as peers serving unconfirmed transaction information to SPV clients.

Because unconfirmed transactions have no permanent status in Bitcoin, Bitcoin Core stores them in non-persistent memory, calling them a memory pool or mempool. When a peer shuts down, its memory pool is lost except for any transactions stored by its wallet. This means that never-mined unconfirmed transactions tend to slowly disappear from the network as peers restart or as they purge some transactions to make room in memory for others.

Transactions which are mined into blocks that later become stale blocks may be added back into the memory pool. These re-added transactions may be re-removed from the pool almost immediately if the replacement blocks include them. This is the case in Bitcoin Core, which removes stale blocks from the chain one by one, starting with the tip (highest block). As each block is removed, its transactions are added back to the memory pool. After all of the stale blocks are removed, the replacement blocks are added to the chain one by one, ending with the new tip. As each block is added, any transactions it confirms are removed from the memory pool.

SPV clients don’t have a memory pool for the same reason they don’t relay transactions. They can’t independently verify that a transaction hasn’t yet been included in a block and that it only spends UTXOs, so they can’t know which transactions are eligible to be included in the next block.

## Misbehaving Nodes
Take note that for both types of broadcasting, mechanisms are in place to punish misbehaving peers who take up bandwidth and computing resources by sending false information. If a peer gets a banscore above the ***-banscore=\<n>*** threshold, he will be banned for the number of seconds defined by ***-bantime=\<n>***, which is 86,400 by default (24 hours).

## AlertsAlerts
Removed inBitcoin Core 0.13.0

Earlier versions of Bitcoin Core allowed developers and trusted community members to issue Bitcoin alerts to notify users of critical network-wide issues. This messaging system was retired in Bitcoin Core v0.13.0; however, internal alerts, partition detection warnings and the ***-alertnotify*** option features remain.

#

## References

* https://developer.bitcoin.org/devguide/p2p_network.html
* https://medium.com/@gloriazhao/map-of-the-bitcoin-network-c6f2619a76f3
* https://bitcoin.design/guide/how-it-works/nodes/#:~:text=A%20light%20node%20is%20bitcoin,parties%20to%20receive%20block%20data.
* https://learn.saylor.org/mod/book/view.php?id=36307&chapterid=18897