# Messages
Messages are one of two primary objects handled by a module in the Cosmos SDK. The other primary object handled by modules is queries. While messages inform the state and have the potential to alter it, queries inspect the module state and are always read-only.<br/>

In the Cosmos SDK, a transaction contains one or more messages. The module processes the messages after the transaction is included in a block by the consensus layer.<br/>

### Signing a Message 
Remember from the previous section on transactions that transactions must be signed before a validator includes them in a block. Every message in a transaction must be signed by the addresses as specified by <code>GetSigners</code>.
<br/>

The Cosmos SDK currently allows signing transactions with either <code>SIGN_MODE_DIRECT</code> or <code>SIGN_MODE_LEGACY_AMINO_JSON</code> methods.
<br/>
When an account signs a message it signs an array of bytes. This array of bytes is the outcome of serializing the message. <br/>

For the signature to be verifiable at a later date, this conversion needs to be **deterministic**. For this reason, you define a canonical bytes-representation of the message, typically with the parameters ordered alphabetically.<br/>

### Messages and the transaction lifecycle
Transactions containing one or more valid messages are serialized and confirmed by the Tendermint consensus engine.<br/>
As you might recall, Tendermint is agnostic to the transaction interpretation and has absolute finality. **When a transaction is included in a block, it is confirmed and finalized with no possibility of chain re-organization or cancellation.** <br/>

The confirmed transaction is relayed to the Cosmos SDK application for interpretation. Each message is routed to the appropriate module via <code>BaseApp</code> using <code>MsgServiceRouter</code>. <code>BaseApp</code> decodes each message contained in the transaction. Each module has its own <code>MsgService</code> that processes each received message.<br/>

### MsgService
Although it is technically feasible to proceed to create a novel <code>MsgService</code>, the recommended approach is to define a Protobuf <code>Msg service</code>.
<br/>

Each module has exactly one Protobuf <code>Msg</code> service defined in <code>tx.proto</code> and there is an RPC service method for each message type in the module. The Protobuf message service implicitly defines the interface layer of the state, mutating processes contained within the module.<br/>

### Example of MsgService [(Link)](https://docs.cosmos.network/v0.46/modules/bank/)
Here is an example <code>MsgService</code> from the <code>bank module</code>.<br/>


> The bank module is responsible for handling multi-asset coin transfers between accounts and tracking special-case pseudo-transfers which must work differently with particular kinds of accounts (notably delegating/undelegating for vesting accounts). It exposes several interfaces with varying capabilities for secure interaction with other modules which must alter user balances.<br/>
In addition, the bank module tracks and provides query support for the total supply of all assets used in the application.
<br/>This module will be used in the Cosmos Hub.

```go
// Msg defines the bank Msg service.
service Msg {
  // Send defines a method for sending coins from one account to another account.
  rpc Send(MsgSend) returns (MsgSendResponse);

  // MultiSend defines a method for sending coins from some accounts to other accounts.
  rpc MultiSend(MsgMultiSend) returns (MsgMultiSendResponse);
}

```
In this example:<br/>

- Each <code>Msg service</code> method has exactly one argument, such as <code>MsgSend</code>, which must implement the <code>sdk.Msg</code> interface and a Protobuf response.
- The **standard naming convention** is to call the RPC argument <code>Msg</code> \<service-rpc-name> and the RPC response <code>Msg</code> \<service-rpc-name>Response.

### Client and server code generation
The Cosmos SDK uses Protobuf definitions to generate client and server code:<br/>
- The <code>MsgServer</code> interface defines the server API for the Msg service. Its implementation is described in the Msg services [documentation](https://docs.cosmos.network/main/building-modules/msg-services.html).
- Structures are generated for all RPC requests and response types.

### Implementation of a module <code>Msg service</code>
Each module should define a Protobuf <code>Msg service</code>, which will be responsible for processing requests (implementing <code>sdk.Msg</code>) and returning responses.<br/>

Protobuf generates a <code>MsgServer</code> interface based on a definition of <code>Msg service</code>. It is the role of the module developer to implement this interface, by implementing the state transition logic that should happen upon receival of each <code>sdk.Msg</code>. As an example, here is the generated <code>MsgServer</code> interface for <code>x/bank</code>, which exposes two <code>sdk.Msgs</code>:

#### [x/bank/types/tx.pb.go](https://github.com/cosmos/cosmos-sdk/blob/v0.46.0/x/bank/types/tx.pb.go#L288-L294)
```go
// MsgServer is the server API for Msg service.
type MsgServer interface {
	// Send defines a method for sending coins from one account to another account.
	Send(context.Context, *MsgSend) (*MsgSendResponse, error)
	// MultiSend defines a method for sending coins from some accounts to other accounts.
	MultiSend(context.Context, *MsgMultiSend) (*MsgMultiSendResponse, error)
}
```

# References
[Message Services](https://docs.cosmos.network/main/building-modules/msg-services.html)

[BankTypes - Github](https://github.com/cosmos/cosmos-sdk/blob/v0.46.0/x/bank/types/tx.pb.go#L288-L294)

[Cosmos Network - Bank](https://docs.cosmos.network/v0.46/modules/bank/)

[Cosmos Academy - Messages](https://tutorials.cosmos.network/academy/2-cosmos-concepts/4-messages.html)