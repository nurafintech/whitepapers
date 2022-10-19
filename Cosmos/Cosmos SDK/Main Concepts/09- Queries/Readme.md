# Queries

A query is a request for information, made by end-users of an application through an interface, and processed by a full node. Available information includes:

* Information about the network.
* Information about the application itself.
* Information about the application state.

** Queries do not require consensus to be processed as they do not trigger state transitions. Therefore queries can be handled entirely independently by a full node.** 

## Creating A Query

For the purpose of explaining the query lifecycle, let's say <code>MyQuery</code> is requesting a list of delegations made by a certain delegator address in the application called <code>simapp</code>. As to be expected, the staking module handles this query. But first, there are a few ways <code>MyQuery</code> can be created by users.

* Query Creation With CLI

    The main interface for an application is the command-line interface. Users connect to a full-node and run the CLI directly from their machines - the CLI interacts directly with the full-node. To create MyQuery from their terminal, users type the following command:

    ```cmd
    simd query staking delegations <delegatorAddress>
    ```

    This query command was defined by the <code>staking</code> module developer and added to the list of subcommands by the application developer when creating the CLI.

    Note that the general format is as follows:
    ```cmd
    simd query [moduleName] [command] <arguments> --flag <flagArg>
    ```
    The CLI understands a specific set of commands, defined in a hierarchical structure by the application developer: from the **root command** <code>(simd)</code>, the type of command <code>(Myquery)</code>, the module that contains the command <code>(staking)</code>, and command itself (delegations). Thus, the CLI knows exactly which module handles this command and directly passes the call there.

* Query Creation With gRPC

    gRPC requests to a gRPC server. The endpoints are defined as Protocol Buffers service methods inside .proto files, written in Protobuf's own language-agnostic interface definition language (IDL). The Protobuf ecosystem developed tools for code-generation from *.proto files into various languages. These tools allow to build gRPC clients easily.    
    One such tool is grpcurl, and a gRPC request for MyQuery using this client looks like:
    ```cmd
    grpcurl \
    -plaintext                                           # We want results in plain test
    -import-path ./proto \                               # Import these .proto files
    -proto ./proto/cosmos/staking/v1beta1/query.proto \  # Look into this .proto file for the Query protobuf service
    -d '{"address":"$MY_DELEGATOR"}' \                   # Query arguments
    localhost:9090 \                                     # gRPC server endpoint
    cosmos.staking.v1beta1.Query/Delegations             # Fully-qualified service method name
    ```
* REST
    HTTP Requests to a **REST server**. The REST server is fully auto-generated from Protobuf services, using [gRPC-gateway](https://github.com/grpc-ecosystem/grpc-gateway).

    ![](https://raw.githubusercontent.com/grpc-ecosystem/grpc-gateway/80e5aefd94f005d4346cbe911bac4d9005feb69e/docs/assets/images/architecture_introduction_diagram.svg)

    An example HTTP request for <code>MyQuery</code> looks like:
    ```cmd
    GET http://localhost:1317/cosmos/staking/v1beta1/delegators/{delegatorAddr}/delegations
    ```

## How Queries are Handled by the CLI

### Context

The first thing that is created in the execution of a CLI command is a <code>client.Context.</code> A <code>client.Context</code> is an object that **stores all the data needed to process a request on the user side.**

In particular, a client.Context stores the following:

* Codec: The [encoder/decoder](https://docs.cosmos.network/main/core/encoding) used by the application, used to marshal the parameters and query before making the Tendermint RPC request and unmarshal the returned response into a JSON object. The default codec used by the CLI is Protobuf.
* Account Decoder: The account decoder from the [auth](https://docs.cosmos.network/main/modules/auth) module, which translates []bytes into accounts.
* RPC Client: The Tendermint RPC Client, or node, to which the request will be relayed to.
* Keyring: A [Key Manager](https://docs.cosmos.network/main/basics/accounts#keyring) used to sign transactions and handle other operations with keys.
* Output Writer: A [Writer](https://pkg.go.dev/io#Writer) used to output the response.
* Configurations: The flags configured by the user for this command, including <code>--height</code>, specifying the height of the blockchain to query and <code>--indent</code>, which indicates to add an indent to the JSON response.

The <code>client.Context</code> also contains various functions such as <code>Query()</code> which retrieves the RPC Client and makes an ABCI call to relay a query to a full-node.

```go
// Context implements a typical context created in SDK modules for transaction
// handling and queries.
type Context struct {
	FromAddress       sdk.AccAddress
	Client            rpcclient.Client
	GRPCClient        *grpc.ClientConn
	ChainID           string
	Codec             codec.Codec
	InterfaceRegistry codectypes.InterfaceRegistry
	Input             io.Reader
	Keyring           keyring.Keyring
	KeyringOptions    []keyring.Option
	Output            io.Writer
	OutputFormat      string
	Height            int64
	HomeDir           string
	KeyringDir        string
	From              string
	BroadcastMode     string
	FromName          string
	SignModeStr       string
	UseLedger         bool
	Simulate          bool
	GenerateOnly      bool
	Offline           bool
	SkipConfirm       bool
	TxConfig          TxConfig
	AccountRetriever  AccountRetriever
	NodeURI           string
	FeePayer          sdk.AccAddress
	FeeGranter        sdk.AccAddress
	Viper             *viper.Viper

	// IsAux is true when the signer is an auxiliary signer (e.g. the tipper).
	IsAux bool

	// TODO: Deprecated (remove).
	LegacyAmino *codec.LegacyAmino
}
```

The <code>client.Context</code>'s primary role is to **store data used during interactions with the end-user and provide methods to interact with this dat**a - it is used **before** and **after** the query is processed by the full-node. Specifically, in handling MyQuery, the client.Context is utilized to encode the query parameters, retrieve the full-node, and write the output.

Prior to being relayed to a full-node, the **query** needs to be **encoded into a []byte** form, as full-nodes are application-agnostic and do not understand specific types. 

The **full-node (RPC Client)** itself is retrieved using the <code>client.Context</code>, which knows which node the user CLI is connected to. The query is relayed to this full-node to be processed.

Finally, the <code>client.Context</code>
contains a <code>Writer</code> to write output when the response is returned.

#

## Refrences
* https://tutorials.cosmos.network/academy/2-cosmos-concepts/9-queries.html
* https://docs.cosmos.network/main/basics/query-lifecycle.html
* https://github.com/cosmos/cosmos-sdk/blob/v0.46.0/client/context.go#L25-L63
* https://github.com/grpc-ecosystem/grpc-gateway
