# Key Standards

## Credential Formats

W3C JSON-LD with JWT

[Dock Anonymous Credential Protocol](https://github.com/docknetwork/crypto-wasm-ts/tree/master/src/anonymous-credentials) which is W3C JSON-LD with BBS2023

W3C JSON-LD with MAC for KVAC

## Credential Standards

[W3C Decentralized Identifiers (DIDs) v1.0](https://w3c.github.io/did-core/)

* [DID:dock](https://github.com/docknetwork/dock-did-driver/blob/master/Dock%20DID%20method%20specification.md)
* [DID:key](https://w3c-ccg.github.io/did-method-key/)
* [DID:polygonid](https://github.com/0xPolygonID/did-polygonid/blob/main/did-polygonid-method.md)

[W3C Verifiable Credentials (VCs) Data Model v1.1](https://www.w3.org/TR/2022/REC-vc-data-model-20220303/)

Our supported revocation approaches are documented here:  [revocation.md](revocation.md "mention")

Credentials are stored in our wallet SDK using [the W3C Universal Wallet 2020 specification](https://w3c-ccg.github.io/universal-wallet-interop-spec/), as implemented in [our open source Universal Wallet library](https://github.com/docknetwork/universal-wallet).

## Exchange Protocols

### Issuance

[OpenID for Verifiable Credential Issuance (OID4VCI) v1.0 Draft 6](https://openid.net/specs/openid-4-verifiable-credential-issuance-1\_0.html)

[Iden3Comm](https://devs.polygonid.com/docs/wallet/wallet-sdk/polygonid-sdk/iden3comm/overview/) for did:polygon

### Presentation Exchange

Our default is the presentation exchange from [DIF Wallet and Credential Interaction (WACI) v1.0 Draft](https://identity.foundation/waci-didcomm/) over [DIDComm Messaging v2.1](https://identity.foundation/didcomm-messaging/spec/v2.1)

We have partial support for [OpenID for Verifiable Presentations (OID4VP) v1.0 Draft 18](https://openid.net/specs/openid-4-verifiable-presentations-1\_0.html)

[Iden3Comm](https://devs.polygonid.com/docs/wallet/wallet-sdk/polygonid-sdk/iden3comm/overview/) for did:polygon

## Cryptography Used

### Signature Formats

Non-anonymous

* Certs defaults to ed25519 signatures
* API can be used to choose between ed25519, sr25519, and secp256k1&#x20;

Anonymous

* BBS2023
* PS sigs

KVAC

* BBDT16 as an algebraic MAC to build keyed anonymous credentials

### Encryption

Encryption at rest in Certs

* Credential documents are stored encrypted with ECDH-ES+A256KW using x25519 key agreement keys. The index is encrypted with searchable encryption.
* Other data is stored on RDS and S3 using AWS's default encryption

Encryption at rest in the Wallet

Encryption in transit

* Queued messages are encrypted per the DIDComm Message packing
