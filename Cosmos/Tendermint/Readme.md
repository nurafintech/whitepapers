# Tendermint: Consensus without Mining
Tendermint provides Byzantine Fault Tolerant State Machine Replication using hash-linked batches of transactions. Such transaction batches are called "blocks". Hence, Tendermint defines a "blockchain" [2].
</br>
Each block in Tendermint has a unique index - its Height. Height's in the blockchain are monotonic.
</br>
Each block is committed by a known **set of weighted Validators**. Membership and weighting within this validator set may change over time. Tendermint guarantees the safety and liveness of the blockchain so long as less than 1/3 of the total weight of the Validator set is malicious or faulty.




# References
1- [Tendermint: Consensus without Mining](https://tendermint.com/static/docs/tendermint.pdf)

2- [Tendermint Spec](https://github.com/tendermint/tendermint/blob/main/spec/README.md)