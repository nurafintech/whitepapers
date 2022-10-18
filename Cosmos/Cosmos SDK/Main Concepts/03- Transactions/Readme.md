# Transactions
Transactions are objects created by end-users to trigger state changes in applications.<br/>
 They are comprised of metadata that defines a context, and one or more [sdk.Msg](#message-interface) that trigger state changes within a module through the module’s Protobuf message service.

### Message Interface
```go
/// sdk.Msg 
Msg interface {
    proto.Message


    // Return the message type.
    // Must be alphanumeric or empty.
    Route() string


    // Returns a human-readable string for the message, intended for utilization
    // within tags
    Type() string


    // ValidateBasic does a simple validation check that
    // doesn't require access to any other information.
    ValidateBasic() error


    // Get the canonical byte representation of the Msg.
    GetSignBytes() []byte


    // Signers returns the addrs of signers that must sign.
    // CONTRACT: All signatures must be present to be valid.
    // CONTRACT: Returns addrs in some deterministic order.
    GetSigners() []AccAddress
}
```

# Transaction process from an end-user perspective

### Decide 
Decide on the messages to put into the transaction. This is normally done with the assistance of a wallet or application and a user interface.

### Generate 
Generate the transaction using the Cosmos SDK's <code>TxBuilder</code>. <code>TxBuilder</code> is the preferred way to generate a transaction.
### Sign
Sign the transaction. Transactions must be signed before a validator includes them in a block.
### Broadcast
Broadcast the signed transaction using one of the available interfaces.
<br/>

**Deciding and signing are the main interactions of a user. Generating and broadcasting are attended to by the user interface and other automation.**

# Transaction objects
Transaction objects are Cosmos SDK types that implement the <code>Tx interface</code>. They contain the following methods:

### Transaction Interface
```go
// Tx defines the interface a transaction must fulfill.
Tx interface {
    // Gets the all the transaction's messages.
    GetMsgs() []Msg

    // ValidateBasic does a simple and lightweight validation check that doesn't
    // require access to any other information.
    ValidateBasic() error
}
```
- **GetMsgs:** unwraps the transaction and returns a list of contained [sdk.Msg](#message-interface). One transaction may have one or multiple messages.

- **ValidateBasic:** includes lightweight, stateless checks used by the ABCI messages' <code>CheckTx</code> and <code>DeliverTx</code> to make sure transactions are not invalid.<br/>

For example, the auth module's <code>StdTx</code> <code>ValidateBasic</code> function checks that its transactions are signed by the correct number of signers and that the fees do not exceed the user's maximum.

### StdTx Struct and Validate Basic
```go
// StdTx is the legacy transaction format for wrapping a Msg with Fee and Signatures.
// It only works with Amino, please prefer the new protobuf Tx in types/tx.
// NOTE: the first signature is the fee payer (Signatures must not be nil).
// Deprecated
type StdTx struct {
	Msgs          []sdk.Msg      `json:"msg" yaml:"msg"`
	Fee           StdFee         `json:"fee" yaml:"fee"`
	Signatures    []StdSignature `json:"signatures" yaml:"signatures"`
	Memo          string         `json:"memo" yaml:"memo"`
	TimeoutHeight uint64         `json:"timeout_height" yaml:"timeout_height"`
}

// ValidateBasic does a simple and lightweight validation check that doesn't
// require access to any other information.
func (tx StdTx) ValidateBasic() error {
	stdSigs := tx.GetSignatures()

	if tx.Fee.Gas > txtypes.MaxGasWanted {
		return sdkerrors.Wrapf(
			sdkerrors.ErrInvalidRequest,
			"invalid gas supplied; %d > %d", tx.Fee.Gas, txtypes.MaxGasWanted,
		)
	}
	if tx.Fee.Amount.IsAnyNegative() {
		return sdkerrors.Wrapf(
			sdkerrors.ErrInsufficientFee,
			"invalid fee provided: %s", tx.Fee.Amount,
		)
	}
	if len(stdSigs) == 0 {
		return sdkerrors.ErrNoSignatures
	}
	if len(stdSigs) != len(tx.GetSigners()) {
		return sdkerrors.Wrapf(
			sdkerrors.ErrUnauthorized,
			"wrong number of signers; expected %d, got %d", len(tx.GetSigners()), len(stdSigs),
		)
	}

	return nil
}
```

### Caution!
There are two <code>ValidateBasic</code>
This function is different from the <code>ValidateBasic</code> functions for [sdk.Msg](#message-interface), which perform basic validity checks on messages only.
<br/>
For example, <code>runTX</code> first runs <code>ValidateBasic</code> on each message when it checks a transaction created from the auth module. Then it runs the auth module's [AnteHandler](#ante-handler), which calls <code>ValidateBasic</code> for the transaction itself.


### Ante Handler
```go
// AnteHandler authenticates transactions, before their internal messages are handled.
// If newCtx.IsZero(), ctx is used instead.
type AnteHandler func(ctx Context, tx Tx, simulate bool) (newCtx Context, err error)
```
You should rarely manipulate a <code>Tx</code> object directly. It is an intermediate type used for transaction generation. Developers usually use the [TxBuilder](#tx-builder) interface.

### Tx Builder
```go
// TxBuilder defines an interface which an application-defined concrete transaction
// type must implement. Namely, it must be able to set messages, generate
// signatures, and provide canonical bytes to sign over. The transaction must
// also know how to encode itself.
TxBuilder interface {
    GetTx() signing.Tx

    SetMsgs(msgs ...sdk.Msg) error
    SetSignatures(signatures ...signingtypes.SignatureV2) error
    SetMemo(memo string)
    SetFeeAmount(amount sdk.Coins)
    SetGasLimit(limit uint64)
    SetTimeoutHeight(height uint64)
    SetFeeGranter(feeGranter sdk.AccAddress)
}
```
# Messages
### Caution
Transaction messages are not to be confused with ABCI messages, which define interactions between Tendermint and application layers.
<br/>

## 

Messages or [sdk.Msg](#message-interface) are module-specific objects that trigger state transitions within the scope of the module they belong to.<br/>
Module developers define module messages by adding methods to the Protobuf <code>Msg</code> service and defining a <code>MsgServer</code>.<br/>

Each [sdk.Msg](#message-interface) is related to exactly one Protobuf <code>Msg</code> service RPC defined inside each module's <code>tx.proto</code> file. A Cosmos SDK app router automatically maps every [sdk.Msg](#message-interface) to a corresponding RPC service, which routes it to the appropriate method. Protobuf generates a <code>MsgServer</code> interface for each module's <code>Msg</code> service and the module developer implements this interface.
<br/>

## Reuseable Functionalities
This design puts more responsibility on module developers. It allows application developers to reuse common functionalities without having to repetitively implement state transition logic.<br/>

While messages contain the information for the state transition logic, a transaction's other metadata and relevant information are stored in the <code>TxBuilder</code> and <code>Context</code>.

# Singing Transactions
Every message in a transaction must be signed by the addresses specified by its <code>GetSigners</code>. The Cosmos SDK currently allows signing transactions in two different ways:

- <code>SIGN_MODE_DIRECT</code> (preferred): the most used implementation of the <code>Tx</code> interface is the <code>Protobuf Tx </code>message, which is used in <code>SIGN_MODE_DIRECT</code>. Once signed by all signers, the <code>BodyBytes</code>, <code>AuthInfoBytes</code>, and <code>Signatures</code> are gathered into <code>TxRaw</code>, whose <code>serialized bytes</code> are broadcast over the network.


# References
[Cosmos Academy - Transactions](https://tutorials.cosmos.network/academy/2-cosmos-concepts/3-transactions.html)

[TxMessages - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx_msg.go#L11-L33)

[StdTx - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/x/auth/legacy/legacytx/stdtx.go#L77-L83)

[Handler - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/handler.go#L8)

[TxConfig - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/client/tx_config.go#L36-L46)