# Accounts

An account is a pair of keys:

<pre>PubKey: a public key</pre>
<pre>PrivKey: a private key</pre>

A public key is a unique identifier for a user or entity that is safe to disclose. Private keys are sensitive information that users are required to manage confidentially. Private keys are used to sign information in a way that proves to others that a message was signed by someone using the private key corresponding to a given public key. This is done without revealing the private key itself.

## Asymmetric and Public key cryptography
Modern cryptographic systems leverage computer capabilities to make the power of certain mathematical functions accessible. Public key cryptography is also known as asymmetric cryptography and is a cryptographic system that employs pairs of keys. Every pair consists of a public and a private key. **The security of the system is not endangered as long as the private key is not disclosed.** Compared to symmetric key algorithms, asymmetric ones do not require parties to use a secure channel to exchange the keys for encryption and decryption.

Asymmetric cryptography has two primary applications:
* Authentication:

    The public key serves as a verification instrument for the private key pair.

* Encryption:

     Only the **private key** can **decrypt the information** encrypted with the public key.

**Public key cryptography assures confidentiality, authenticity, and non-repudiation**. Examples of applications include S/MIME (opens new window)and GPG (opens new window), and it is the basis of several internet standards like SSL (opens new window)and TLS (opens new window).

Asymmetric cryptography is normally applied to small data blocks due to its computational complexity. **Symmetric and asymmetric cryptography can be combined in a hybrid system. For example, asymmetric encryption could be employed to transfer a symmetric encryption, then used as an encryption key for the message.** An example of hybrid systems is PGP (opens new window).

Asymmetric keys always come in pairs and offer their owner various capabilities. These capabilities are based on cryptographic mathematics. **The public key is meant to be distributed to whoever is relevant, while the private key is to remain a secret**. This is similar to sharing the address of your house, but keeping the key to your front door private.

The length of keys is vital. Asymmetric cryptographic keys are usually very long. One can keep in mind a general principle: **the longer the key, the more difficult it is to break the code.** Breaking an asymmetric key can only be done with a brute force attack, in which an attacker would need to try every possible key to find a match.

**Private keys are used to prove that messages originate from the owners of accounts** known by their public keys: the signatures prove that messages were signed by someone that knows the private key that corresponds to a given public key. This is the basis of user authentication in a blockchain, and why private keys are strictly guarded secrets.

## Sign and verify Example

Alice and Bob are communicating. Alice wants to make sure that Bob's public announcement is indeed from Bob, so:

* Bob gives Alice his public key.
* Bob signs his announcement with his private key.
* Bob sends Alice his announcement and its signature.
* Alice verifies the signature with Bob's public key.

Alice can verify the source of the announcement by checking if the signature was done with the private key that corresponds to Bob’s public key (which is already known to represent Bob).


## Hierarchical-deterministic wallets

**Blockchains** generally **maintain ledgers of user accounts** and rely on **public key cryptography** for user **authentication**. Knowledge of one's public and private keys is a requirement to execute transactions. **Client software applications** known as **wallets** provide methods to **generate new key pairs** and **store them**, as well as basic services such as **creating transactions**, **signing messages**, **interacting with applications**, and communicating with the ***blockchain**.

Although it is technically feasible to generate and store multiple key pairs in a wallet, key management quickly becomes tedious and error-prone for users. Given that all keys would exist only in one place, **users would need to devise ways to recover their keys in adverse situations such as the loss or destruction of the computer.** The more accounts, the more keys to back up.

### Do I need many addresses?

**Using multiple addresses can help you improve privacy.** You may be a single individual or entity, but you may want to transact with others under different aliases. Additionally, you will likely interact with more than one blockchain in the Cosmos Ecosystem. Conveniently, **your inevitably-different addresses on different blockchains can all stem from a single seed.**

A **hierarchical-deterministic wallet** uses a **single seed phrase** to **generate many key pairs** to reduce this complexity. **Only the seed phrase needs to be backed up.**

### Cryptographic standards

The Cosmos SDK uses **BIP32** , which allows users to generate a set of accounts from an initial secret and a derivation path containing some input data, such as a blockchain identifier and account index. **Since BIP39, this initial secret is mostly generated with 12 or 24 words, known as the mnemonic, taken from a standardized dictionary**. Key pairs can always be mathematically reproduced from the mnemonic and the derivation path, which explains the deterministic nature of wallets.

Like most blockchain implementations, **Cosmos derives addresses from the public keys.**

* ![](https://tutorials.cosmos.network/resized-images/600/academy/2-cosmos-concepts/images/hd-accounts.png)

When using BIP39 or one of its variants, **a user is required only to store their BIP39 mnemonic in a safe and confidential manner**. All **key pairs** can be **reconstructed** from the mnemonic because it is **deterministic**. There is no practical upper limit to the number of key pairs that can be generated from a single mnemonic. **The input taken from the BIP44 derivation path is used to generate a key pair for every blockchain using one single mnemonic**. Hence the name "hierarchical-deterministic" to describe this key generation approach.

### Can you be tracked across different addresses?
A hierarchical-deterministic wallet also preserves privacy because **the next public key or address cannot be deduced from the previous ones.** Two addresses issued from a single mnemonic or two addresses created from two different mnemonics are **indistinguishable.**

<br>

## Keyrings, addresses, and address types

In the Cosmos SDK, **keys are stored** and managed in an object called a **keyring.**

Authentication is implemented as signature verification:

* Users generate transactions, sign transactions, and send signed transactions to the blockchain.
* Transactions are formatted with the public key as part of the message. Signatures are verified by confirming that the signature's public key matches the public key associated with the sender. If the message is signed by anyone other than the purported sender, the signature is invalid and the transaction is rejected.

Consider the following pseudo message in case the foregoing is unclear:
``` json
"Message": {
  "Payload": {
    "Sender": "0x1234",
    "Data": "Hello World"
  },
  "Signature": "0xabcd"
}
```
Passing <code>Payload</code> and <code>Signature</code> into the signature verification function returns a sender. The derived sender must match the <code>Sender</code> in the <code>Payload</code> itself. This confirms that the Payload could only originate from someone that knows the private key corresponding to <code>Sender: “0x1234”</code>.

## Signature schemes

There is more than one implementation of the public key signature process previously described. The Cosmos SDK supports the following digital key schemes for creating digital signatures:

* ![](https://tutorials.cosmos.network/resized-images/600/academy/2-cosmos-concepts/images/state_machine_2.png)

The different digital key schemes are implemented in different SDK packages:

* **secp256k1**, as implemented in the SDK's <code>crypto/keys/secp256k1</code> package: is **the most common** and **the same one used for Bitcoin**.
* **secp256r1**, as implemented in the SDK's <code>crypto/keys/secp256r1</code> package.
* **tm-ed25519**, as implemented in the SDK's <code>crypto/keys/ed25519</code> package: is supported **only for consensus validation.**

## Accounts [link](https://github.com/cosmos/cosmos-sdk/blob/bf11b1bf1fa0c52fb2cd51e4f4ab0c90a4dd38a0/x/auth/types/auth.pb.go#L31-L36)
The <code>BaseAccount</code> object provides the basic account implementation that **stores authentication** information.

```go
// BaseAccount defines a base account type. It contains all the necessary fields
// for basic account functionality. Any custom account type should extend this
// type for additional functionality (e.g. vesting).
type BaseAccount struct {
	Address       string     `protobuf:"bytes,1,opt,name=address,proto3" json:"address,omitempty"`
	PubKey        *types.Any `protobuf:"bytes,2,opt,name=pub_key,json=pubKey,proto3" json:"public_key,omitempty"`
	AccountNumber uint64     `protobuf:"varint,3,opt,name=account_number,json=accountNumber,proto3"                 json:"account_number,omitempty"`
	Sequence      uint64     `protobuf:"varint,4,opt,name=sequence,proto3" json:"sequence,omitempty"`
}
```

## Public keys [link](https://github.com/cosmos/cosmos-sdk/blob/9fd866e3820b3510010ae172b682d71594cd8c14/crypto/types/types.go#L9)
**Public keys are generally not used to reference accounts.** Public keys do exist and they are accessible through the <code>cryptoTypes.PubKey</code> interface. **This facilitates operations which developers** may find useful, such as **signing off-chain messages** or **using a public key for other out-of-band operations.**

```go
// PubKey defines a public key and extends proto.Message.
type PubKey interface {
	proto.Message

	Address() Address
	Bytes() []byte
	VerifySignature(msg []byte, sig []byte) bool
	Equals(PubKey) bool
	Type() string
}
```

## ADR 028: Public Key Addresses [link](https://github.com/cosmos/cosmos-sdk/blob/main/docs/architecture/adr-028-public-key-addresses.md)
This ADR defines an address format for all addressable Cosmos SDK accounts. That includes: new public key algorithms, multisig public keys, and module accounts.

**The ADR only defines a process for the generation of address bytes. For end-user interactions with addresses (through the API, or CLI, etc.), we still use bech32 to format these addresses as strings. This ADR doesn't change that. Using Bech32 for string encoding gives us support for checksum error codes and handling of user typos.**

Address
An address is public information normally used to reference an account. Addresses are derived from public keys using ADR-28 (opens new window). Three types of addresses specify a context when an account is used:

* [AccAddress](https://github.com/cosmos/cosmos-sdk/blob/1dba6735739e9b4556267339f0b67eaec9c609ef/types/address.go#L129) identifies users, which are the sender of a message.

	```go
	// AccAddress a wrapper around bytes meant to represent an account address.
	// When marshaled to a string or JSON, it uses Bech32.
	type AccAddress []byte

	// AccAddressFromHex creates an AccAddress from a hex string.
	func AccAddressFromHex(address string) (addr AccAddress, err error) {
		bz, err := addressBytesFromHexString(address)
		return AccAddress(bz), err
	}
	```
* [ValAddress](https://github.com/cosmos/cosmos-sdk/blob/23e864bc987e61af84763d9a3e531707f9dfbc84/types/address.go#L298) identifies validator operators.
	```go
	// ValAddress defines a wrapper around bytes meant to present a validator's
	// operator. When marshaled to a string or JSON, it uses Bech32.
	type ValAddress []byte

	// ValAddressFromHex creates a ValAddress from a hex string.
	func ValAddressFromHex(address string) (addr ValAddress, err error) {
		bz, err := addressBytesFromHexString(address)
		return ValAddress(bz), err
	}
	```
* [ConsAddress](https://github.com/cosmos/cosmos-sdk/blob/23e864bc987e61af84763d9a3e531707f9dfbc84/types/address.go#L448) identifies validator nodes that are participating in consensus. Validator nodes are derived using the <b>ed25519</b> curve.

	```go
	// ConsAddress defines a wrapper around bytes meant to present a consensus node.
	// When marshaled to a string or JSON, it uses Bech32.
	type ConsAddress []byte

	// ConsAddressFromHex creates a ConsAddress from a hex string.
	func ConsAddressFromHex(address string) (addr ConsAddress, err error) {
		bz, err := addressBytesFromHexString(address)
		return ConsAddress(bz), err
	}
	```





## Keyring [link](https://github.com/cosmos/cosmos-sdk/blob/bf11b1bf1fa0c52fb2cd51e4f4ab0c90a4dd38a0/crypto/keyring/keyring.go#L55)

**The keyring object stores and manages multiple accounts.** The keyring object implements the <code>Keyring</code> interface in the Cosmos SDK.

```go
// Keyring exposes operations over a backend supported by github.com/99designs/keyring.
type Keyring interface {
	// List all keys.
	List() ([]*Record, error)

	// Supported signing algorithms for Keyring and Ledger respectively.
	SupportedAlgorithms() (SigningAlgoList, SigningAlgoList)

	// Key and KeyByAddress return keys by uid and address respectively.
	Key(uid string) (*Record, error)
	KeyByAddress(address sdk.Address) (*Record, error)

	// Delete and DeleteByAddress remove keys from the keyring.
	Delete(uid string) error
	DeleteByAddress(address sdk.Address) error

	// Rename an existing key from the Keyring
	Rename(from string, to string) error

	// NewMnemonic generates a new mnemonic, derives a hierarchical deterministic key from it, and
	// persists the key to storage. Returns the generated mnemonic and the key Info.
	// It returns an error if it fails to generate a key for the given algo type, or if
	// another key is already stored under the same name or address.
	//
	// A passphrase set to the empty string will set the passphrase to the DefaultBIP39Passphrase value.
	NewMnemonic(uid string, language Language, hdPath, bip39Passphrase string, algo SignatureAlgo) (*Record, string, error)

	// NewAccount converts a mnemonic to a private key and BIP-39 HD Path and persists it.
	// It fails if there is an existing key Info with the same address.
	NewAccount(uid, mnemonic, bip39Passphrase, hdPath string, algo SignatureAlgo) (*Record, error)

	// SaveLedgerKey retrieves a public key reference from a Ledger device and persists it.
	SaveLedgerKey(uid string, algo SignatureAlgo, hrp string, coinType, account, index uint32) (*Record, error)

	// SaveOfflineKey stores a public key and returns the persisted Info structure.
	SaveOfflineKey(uid string, pubkey types.PubKey) (*Record, error)

	// SaveMultisig stores and returns a new multsig (offline) key reference.
	SaveMultisig(uid string, pubkey types.PubKey) (*Record, error)

	Signer

	Importer
	Exporter

	Migrator
}
```

<br>




# References

* https://tutorials.cosmos.network/academy/2-cosmos-concepts/2-accounts.html