# Verifiable Random Functions
The name “Verifiable Random Function” may not align well with many folks’ natural intuition.
In cryptography, a verifiable random function (VRF) is a public-key pseudorandom function that provides proofs that its outputs were calculated correctly. <br/>

Obtaining a source of unpredictable auditable and tamper-proof randomness on the blockchain is difficult on-chain randomness solutions like block hashes are subject to block withholding attacks by miners and validators and therefore cannot be trusted on the other hand off-chain randomness solutions are opaque requiring a high degree of trust that the centralized data provider won't manipulate the results to their benefit.<br/>

First, an ideal cryptographic hash function deterministically maps an arbitrary-sized message string to a fixed-size digest that is impossible to direct/predict without brute-force, essentially indistinguishable from a random oracle, and infeasible to run backwards (i.e. invert). <br/>
The hash function makes it incredibly hard to find two input messages mapping to the same digest. The resulting digest is commonly associated with a message (over a safe channel) to support integrity checks.<br/>

Second, a keyed hash function is a simple extension where a symmetric key is included alongside the message string in the deterministic digest calculation. The result is called a Message Authentication Code (MAC, HMAC, or often a ‘tag’), and is also commonly associated with a message to support both integrity and authenticity checks. Note that these two assurances are dependent upon a symmetric key that is somehow generated and securely shared between the communicating parties.<br/>

# Better Defenition for VRF with an Example

More precisely, a VRF involves three primary functions and four data objects. Alice runs a Prove() function that takes an input message (alpha_string) and her secret key (sk), and returns an intermediate proof (pi_string). She next runs a Proof_to_hash() function that takes the proof (pi_string) and returns the final digest (beta_string) to share with Bob. Later, Bob can run a Verify() function that takes Alice’s public key (y), the input message (alpha_string) and proof (pi_string) and returns a locally calculated digest (beta_string') for comparison with the original received digest (beta_string). From this point forward, the four data objects will be referred to as simply alpha_string, sk, proof_string, beta_string and y. There are RSA and elliptic curve VRF variants (and a few other lesser-known approaches), but this post is constrained to an elliptic curve VRF. <br/>


**Regarding naming intuition, consider a Verifiable Random Function to be a function capable of producing deterministic and unique ‘randomness’ that can later be independently verified.** Note that typical digital signature algorithms may have aspects of non-determinism, malleability and insufficient randomness that can prevent their direct applicability for our purposes. Where these aspects are properly addressed, a hashed signature is a very comparable approach.

# VRF in Chainlink
Chainlink VRF (verifiable random function) was created to provide smart contract developers with a source of cryptographically secure randomness invulnerable against manipulation. With every new request Chainlink VRF generates a random number and cryptographic proof of how that number was determined using a combination of unpredictable block data and in oracle's private key the cryptographic proof is published and verified on chain before the randomness is delivered to the application.<br/>

This process ensures that the results are provably fair verifiable and tamper proof chain link VRF unlocks a whole new set of blockchain and off-chain use cases across gaming where verifiably random character distribution and player matchmaking makes gameplay more unpredictable and exciting or NFTs or tamper-proof seating of specific collectible traits can be used to mint truly rare NFTs and even fair selection and ordering where the provably fair distribution of high demand items like token airdrops or the verifiably random selection of lucky draw winners can ensure unbiased outcomes.



# References
https://research.nccgroup.com/2020/02/24/reviewing-verifiable-random-functions/

https://en.wikipedia.org/wiki/Verifiable_random_function#:~:text=In%20cryptography%2C%20a%20verifiable%20random,proof%20for%20any%20input%20value

https://www.youtube.com/watch?v=eRzLNfn4LGc
