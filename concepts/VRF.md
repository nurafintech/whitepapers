# Verifiable Random Functions
The name “Verifiable Random Function” may not align well with many folks’ natural intuition.
First, an ideal cryptographic hash function deterministically maps an arbitrary-sized message string to a fixed-size digest that is impossible to direct/predict without brute-force, essentially indistinguishable from a random oracle, and infeasible to run backwards (i.e. invert). <br/>
The hash function makes it incredibly hard to find two input messages mapping to the same digest. The resulting digest is commonly associated with a message (over a safe channel) to support integrity checks.<br/>

Second, a keyed hash function is a simple extension where a symmetric key is included alongside the message string in the deterministic digest calculation. The result is called a Message Authentication Code (MAC, HMAC, or often a ‘tag’), and is also commonly associated with a message to support both integrity and authenticity checks. Note that these two assurances are dependent upon a symmetric key that is somehow generated and securely shared between the communicating parties.<br/>

# Better Defenition for VRF with an Example

More precisely, a VRF involves three primary functions and four data objects. Alice runs a Prove() function that takes an input message (alpha_string) and her secret key (sk), and returns an intermediate proof (pi_string). She next runs a Proof_to_hash() function that takes the proof (pi_string) and returns the final digest (beta_string) to share with Bob. Later, Bob can run a Verify() function that takes Alice’s public key (y), the input message (alpha_string) and proof (pi_string) and returns a locally calculated digest (beta_string') for comparison with the original received digest (beta_string). From this point forward, the four data objects will be referred to as simply alpha_string, sk, proof_string, beta_string and y. There are RSA and elliptic curve VRF variants (and a few other lesser-known approaches), but this post is constrained to an elliptic curve VRF.


# References
https://research.nccgroup.com/2020/02/24/reviewing-verifiable-random-functions/