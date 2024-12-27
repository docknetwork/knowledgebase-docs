# Truvera Credential SDK

The Truvera Credential SDK is an opensource library that powers Truvera SaaS API. It provides the credential management, cryptography, and blockchain storage features for Truvera's supported credential variants:

* W3C VC JSON-LD ed25519 credential using StatusList 2021 for revocation targetted at interoperability
* W3C VC JSON-LD BBS credential using accumulators for revocation targetted at privacy
* W3C VC JSON-LD KVAC credential using accumulators for revocation allowing monetization of credentials

Most of the SDK is written in JavaScript / TypeScript with safety-critical code written in Rust. The SDK depends on [the Arkworks math library](https://github.com/arkworks-rs/algebra).

Some useful references:

1. DID [concepts](https://docknetwork.github.io/sdk/tutorials/concepts_did.html) and the corresponding [SDK API](https://docknetwork.github.io/sdk/tutorials/tutorial_did.html).
2. [DID resolver](https://docknetwork.github.io/sdk/tutorials/tutorial_resolver.html)
3. [Verifiable credentials](https://docknetwork.github.io/sdk/tutorials/concepts_vcdm.html) and its [API](https://docknetwork.github.io/sdk/tutorials/tutorial_ipv.html)
4. [Schema](https://docknetwork.github.io/sdk/tutorials/concepts_blobs_schemas.html) and its [API](https://docknetwork.github.io/sdk/tutorials/tutorial_blobs_schemas.html)
5. [Credential revocation](https://docknetwork.github.io/sdk/tutorials/tutorial_revocation.html)
6. [Claim Deduction](https://docknetwork.github.io/sdk/tutorials/concepts_claim_deduction.html) and its [API](https://docknetwork.github.io/sdk/tutorials/tutorial_claim_deduction.html)
7. [PoE anchoring](https://docknetwork.github.io/sdk/tutorials/concepts_poe_anchors.html) and its [API](https://docknetwork.github.io/sdk/tutorials/tutorial_poe_anchors.html)
8. [Complete examples](https://github.com/docknetwork/sdk/tree/master/example) in SDK for various features
9. Another useful place is the [SDK tests](https://github.com/docknetwork/sdk/tree/master/tests)
10. [API reference](https://docknetwork.github.io/sdk/reference/)
11. To see how to do basic operations like generate addresses, validate addresses, check balance, do token transfer, get block by hash or number, etc, see [this example script](https://github.com/docknetwork/sdk/blob/master/example/chain-ops.js). The script uses functions defined [here](https://github.com/docknetwork/sdk/blob/master/src/utils/chain-ops.js).
