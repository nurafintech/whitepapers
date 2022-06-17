## Introduction
Polkadot network and its wild cousin Kusama are decentralized systems run by a large number of servers (i.e., nodes) that cannot be controlled by a single entity. This permissionless design offers more freedom and inclusion than centralized systems such as Google and Facebook. Whereas those centralized systems base their trustworthiness on their authority, decentralized systems draw security from rigorous economic incentive schemes. As a prominent variant of this concept, proof-of-stake networks emerged. These require nodes participating in consensus, often called validators, to put monetary resources at risk as a security deposit.

### Nominated Proof of Stake
A key question is how such a network determines who may act as a validator. Here, Polkadot and Kusama utilize the Nominated Proof-Of-Stake protocol to calculate the active set of validators based on the total amount of nominated stake backing them. This includes both the validator's own stake and that of other token holders who back them (nominators). Specifically, this protocol partitions all the nominators' and validators' stake into a fixed number of stake pools – one per validator – so that the stake pool sizes are as evenly distributed as possible. In contrast to other proof-of-stake systems, this advanced mechanism guarantees proportional representation[1] of minorities’ preferences, which improves fairness and further democratizes the process. This also empowers the users of the network to take part in the regular election of validators and thereby have a direct influence on the active set. <br>
To motivate nominators to select only suitable and trustworthy validators, they share the same consequences as their validators. That means that they get rewarded for the validator's good behavior and fined ("slashed") for bad behavior.

### What behavior or criteria should the Nominators expect from validators?
* First, nominators must expect their selected validators to act according to the rules of the network. Breaking those rules includes malicious behavior where an adverse validator (or cartel of validators) runs modified software in an attempt to double-spend or build a competitive fork.
* Second, nominators must expect validators to be sufficiently competent to maintain their hardware and handle the infrastructure, preventing downtimes and unintended equivocations, thereby guaranteeing availability and constant block production. Third, nominators must expect their validators to value their implicit agreement of not increasing the commission significantly without giving notice and to frequently pay out the accumulated rewards.

<br>


### Canary Netwrok
Over 130 blockchain development teams around the world are currently building and launching their own parachains in Polkadot's growing ecosystem, due in large part to the distinct advantages the parachain model gives them over alternative technologies. In the case of Kusama, Polkadot's 'canary network,' several parachains are already live and running, and have processed several million transactions since summer 2021.

![](https://polkadot.network/content/images/2020/04/Artboard-1-copy@2x.png)


## References

* https://polkadot.network/blog/nominating-and-validator-selection-on-polkadot/
* https://polkadot.network/blog/kusama-polkadot-comparing-the-cousins/


