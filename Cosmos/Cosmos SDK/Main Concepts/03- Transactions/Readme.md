# Transactions
Transactions are objects created by end-users to trigger state changes in applications.<br/>
 They are comprised of metadata that defines a context, and one or more [sdk.Msg](#sdk.Msg)  that trigger state changes within a module through the module’s Protobuf message service.

 ### sdk.Msg

 <code>
 
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
 </code>