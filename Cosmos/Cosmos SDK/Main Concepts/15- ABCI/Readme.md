# ABCI++

## Introduction

ABCI++ is a major evolution of ABCI (**A**pplication **B**lock**c**hain **I**nterface).
Like its predecessor, ABCI++ is the interface between Tendermint (a state-machine
replication engine) and the actual state machine being replicated (i.e., the Application).
The API consists of a set of _methods_, each with a corresponding `Request` and `Response`
message type.

The methods are always initiated by Tendermint. The Application implements its logic
for handling all ABCI++ methods.
Thus, Tendermint always sends the `Request*` messages and receives the `Response*` messages
in return.

All ABCI++ messages and methods are defined in [protocol buffers](../../proto/tendermint/abci/types.proto).
This allows Tendermint to run with applications written in many programming languages.

This specification is split as follows:

- [Overview and basic concepts](./1-%20Basic%20Concepts/Readme.md) - interface's overview and concepts
  needed to understand other parts of this specification.
- [Methods](./2-%20ABCI%20Methods/Readme.md) - complete details on all ABCI++ methods
  and message types.
- [Requirements for the Application](./3-%20Requirements%20for%20the%20Application/Readme.md) - formal requirements
  on the Application's logic to ensure Tendermint properties such as liveness. These requirements define what
  Tendermint expects from the Application; second part on managing ABCI application state and related topics.
- [Tendermint's expected behavior](./4-%20Tendermint%20Expected%20Behavior/Readme.md) - specification of
  how the different ABCI++ methods may be called by Tendermint. This explains what the Application
  is to expect from Tendermint.
- [Client and Server](./5-%20Client%20%26%20Server/Readme.md) - for those looking to implement their
  own ABCI application servers