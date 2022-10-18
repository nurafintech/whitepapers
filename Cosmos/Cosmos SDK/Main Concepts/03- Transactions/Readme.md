# Transactions
Transactions are objects created by end-users to trigger state changes in applications.<br/>
 They are comprised of metadata that defines a context, and one or more [sdk.Msg](#message-interface) that trigger state changes within a module through the module’s Protobuf message service.

### Message Interface [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx_msg.go#L11-L33)
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

### Transaction Interface [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx_msg.go#L50-L57)
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

### Standard Tx [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/x/auth/legacy/legacytx/stdtx.go#L77-L83)
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
```
### Validate Basic [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx_msg.go#L56)
```go
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


### Ante Handler [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/handler.go#L8)
```go
// AnteHandler authenticates transactions, before their internal messages are handled.
// If newCtx.IsZero(), ctx is used instead.
type AnteHandler func(ctx Context, tx Tx, simulate bool) (newCtx Context, err error)
```
You should rarely manipulate a <code>Tx</code> object directly. It is an intermediate type used for transaction generation. Developers usually use the [TxBuilder](#tx-builder) interface.

### Tx Builder [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/client/tx_config.go#L36-L46)
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

### Sign Mode Direct [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx/signing/signing.pb.go#L36) 
```go
const (
	// SIGN_MODE_UNSPECIFIED specifies an unknown signing mode and will be
	// rejected
	SignMode_SIGN_MODE_UNSPECIFIED SignMode = 0
	
    // SIGN_MODE_DIRECT specifies a signing mode which uses SignDoc and is
	// verified with raw bytes from Tx
	SignMode_SIGN_MODE_DIRECT SignMode = 1
	
    // SIGN_MODE_TEXTUAL is a future signing mode that will verify some
	// human-readable textual representation on top of the binary representation
	// from SIGN_MODE_DIRECT
	SignMode_SIGN_MODE_TEXTUAL SignMode = 2
	
    // SIGN_MODE_LEGACY_AMINO_JSON is a backwards compatibility mode which uses
	// Amino JSON and will be removed in the future
	SignMode_SIGN_MODE_LEGACY_AMINO_JSON SignMode = 127
)

```

### Protobuf Tx [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx/tx.pb.go#L32-L42)
```go
// Tx is the standard type used for broadcasting transactions.
type Tx struct {
	// body is the processable content of the transaction
	Body *TxBody `protobuf:"bytes,1,opt,name=body,proto3" json:"body,omitempty"`
	// auth_info is the authorization related content of the transaction,
	// specifically signers, signer modes and fee
	AuthInfo *AuthInfo `protobuf:"bytes,2,opt,name=auth_info,json=authInfo,proto3" json:"auth_info,omitempty"`
	// signatures is a list of signatures that matches the length and order of
	// AuthInfo's signer_infos to allow connecting signature meta information like
	// public key and signing mode by position.
	Signatures [][]byte `protobuf:"bytes,3,rep,name=signatures,proto3" json:"signatures,omitempty"`
}
```


### Tx Raw [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx/tx.pb.go#L113)
```go
// TxRaw is a variant of Tx that pins the signer's exact binary representation
// of body and auth_info. This is used for signing, broadcasting and
// verification. The binary `serialize(tx: TxRaw)` is stored in Tendermint and
// the hash `sha256(serialize(tx: TxRaw))` becomes the "txhash", commonly used
// as the transaction ID.
type TxRaw struct {
	// body_bytes is a protobuf serialization of a TxBody that matches the
	// representation in SignDoc.
	BodyBytes []byte `protobuf:"bytes,1,opt,name=body_bytes,json=bodyBytes,proto3" json:"body_bytes,omitempty"`
	// auth_info_bytes is a protobuf serialization of an AuthInfo that matches the
	// representation in SignDoc.
	AuthInfoBytes []byte `protobuf:"bytes,2,opt,name=auth_info_bytes,json=authInfoBytes,proto3" json:"auth_info_bytes,omitempty"`
	// signatures is a list of signatures that matches the length and order of
	// AuthInfo's signer_infos to allow connecting signature meta information like
	// public key and signing mode by position.
	Signatures [][]byte `protobuf:"bytes,3,rep,name=signatures,proto3" json:"signatures,omitempty"`
}
```
- **SIGN_MODE_LEGACY_AMINO_JSON:** the legacy implementation of the <code>Tx interface</code> is the [StdTx](#standard-tx-link) struct from <code>x/auth</code>. The document signed by all signers is [StdSignDoc](#standard-sign-doc-link), which is encoded into [bytes](#standard-sign-bytes-link) using Amino JSON.
Once all signatures are gathered into [StdTx](#standard-tx-link), <code>StdTx</code> is serialized using Amino JSON and these bytes are broadcast over the network. **This method is being deprecated.**

### Standard Sign Doc [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/x/auth/legacy/legacytx/stdsign.go#L24-L32)
```go
// StdSignDoc is replay-prevention structure.
// It includes the result of msg.GetSignBytes(),
// as well as the ChainID (prevent cross chain replay)
// and the Sequence numbers for each signature (prevent
// inchain replay and enforce tx ordering per account).
type StdSignDoc struct {
	AccountNumber uint64            `json:"account_number" yaml:"account_number"`
	Sequence      uint64            `json:"sequence" yaml:"sequence"`
	TimeoutHeight uint64            `json:"timeout_height,omitempty" yaml:"timeout_height"`
	ChainID       string            `json:"chain_id" yaml:"chain_id"`
	Memo          string            `json:"memo" yaml:"memo"`
	Fee           json.RawMessage   `json:"fee" yaml:"fee"`
	Msgs          []json.RawMessage `json:"msgs" yaml:"msgs"`
}
```

### Standard Sign Bytes [(Link)](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/x/auth/legacy/legacytx/stdsign.go#L35-L58)
```go
// StdSignBytes returns the bytes to sign for a transaction.
func StdSignBytes(chainID string, accnum, sequence, timeout uint64, fee StdFee, msgs []sdk.Msg, memo string) []byte {
	msgsBytes := make([]json.RawMessage, 0, len(msgs))
	for _, msg := range msgs {
		// If msg is a legacy Msg, then GetSignBytes is implemented.
		// If msg is a ServiceMsg, then GetSignBytes has graceful support of
		// calling GetSignBytes from its underlying Msg.
		msgsBytes = append(msgsBytes, json.RawMessage(msg.GetSignBytes()))
	}

	bz, err := legacy.Cdc.MarshalJSON(StdSignDoc{
		AccountNumber: accnum,
		ChainID:       chainID,
		Fee:           json.RawMessage(fee.Bytes()),
		Memo:          memo,
		Msgs:          msgsBytes,
		Sequence:      sequence,
		TimeoutHeight: timeout,
	})
	if err != nil {
		panic(err)
	}

	return sdk.MustSortJSON(bz)
}
```

# Generating Transactions



# References
[Cosmos Academy - Transactions](https://tutorials.cosmos.network/academy/2-cosmos-concepts/3-transactions.html)

[TxMessages - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx_msg.go#L11-L33)

[StdTx - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/x/auth/legacy/legacytx/stdtx.go#L77-L83)

[Handler - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/handler.go#L8)

[TxConfig - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/client/tx_config.go#L36-L46)

[Sign Mode Direct  - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx/signing/signing.pb.go#L36)

[Protobuf Tx - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx/tx.pb.go#L32-L42)

[Tx Raw](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/types/tx/tx.pb.go#L113)

[Standard Sign Doc - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/x/auth/legacy/legacytx/stdsign.go#L24-L32)

[Standard Sign Bytes - Github](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/x/auth/legacy/legacytx/stdsign.go#L35-L58)