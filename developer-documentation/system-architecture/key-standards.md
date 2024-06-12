# Supported Standards

The Dock Certs Platform is built on W3C open standards. This ensures that users can store their Credentials on any digital wallet that adheres to these standards and that any stakeholder, wherever they are in the world, can verify the authenticity of the data as long as their verification system adheres to these standards. If there is a standard for which you would like further clarification or support, please [contact us](../../support/).

## Standards Bodies

* [World Wide Web Consortium (W3C)](https://www.w3.org/)
* [OpenID Foundation (OIDF)](https://openid.net/foundation/)
* [Decentralized Identity Foundation (DIF)](https://identity.foundation/)
* [Internet Engineering Task Force (IETF)](https://www.ietf.org/)

## Supported Standards

Dock Supports the following open standards:

<table><thead><tr><th width="180">Technology</th><th width="367">Open Standard</th><th>Standard Body</th></tr></thead><tbody><tr><td>Data model</td><td><a href="https://www.w3.org/TR/2022/REC-vc-data-model-20220303/">W3C Verifiable Credentials (VCs) Data Model v1.1</a></td><td>W3C</td></tr><tr><td>Credential format</td><td><a href="https://www.w3.org/TR/vc-data-model/#json-ld">W3C JSON-LD with JWT</a><br><a href="https://github.com/docknetwork/crypto-wasm-ts/tree/master/src/anonymous-credentials">W3C JSON-LD with BBS2023 for </a><a href="https://github.com/docknetwork/crypto-wasm-ts/tree/master/src/anonymous-credentials">Anonymous Credentials</a><br><a href="https://github.com/docknetwork/crypto-wasm-ts/tree/master/src/accumulator">W3C JSON-LD with MAC for KVAC paid verifications</a></td><td>W3C</td></tr><tr><td>Decentralized Identifier</td><td><p><a href="https://github.com/docknetwork/dock-did-driver/blob/master/Dock%20DID%20method%20specification.md">DID:dock</a></p><p><a href="https://w3c-ccg.github.io/did-method-key/">DID:key</a></p><p><a href="https://github.com/0xPolygonID/did-polygonid/blob/main/did-polygonid-method.md">DID:polygonid</a></p></td><td>W3C</td></tr><tr><td>Credential Issuance</td><td><a href="https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html">OpenID for Verifiable Credential Issuance (OID4VCI) v1.0 Draft 6</a><br><a href="https://devs.polygonid.com/docs/wallet/wallet-sdk/polygonid-sdk/iden3comm/overview/">Iden3Comm</a> for did:polygon</td><td>OIDF</td></tr><tr><td>Presentation</td><td>Default presentation exchange from <a href="https://identity.foundation/waci-didcomm/">DIF Wallet and Credential Interaction (WACI) v1.0 Draft</a> over <a href="https://identity.foundation/didcomm-messaging/spec/v2.1">DIDComm Messaging v2.1</a><br>Partial support for <a href="https://openid.net/specs/openid-4-verifiable-presentations-1_0.html">OpenID for Verifiable Presentations (OID4VP) v1.0 Draft 18</a><br><a href="https://devs.polygonid.com/docs/wallet/wallet-sdk/polygonid-sdk/iden3comm/overview/">Iden3Comm</a> for did:polygon</td><td>DIF<br>OIDF</td></tr><tr><td>Revocation</td><td><a href="https://www.w3.org/TR/vc-status-list/">Verifiable Credential Status List</a><br><a href="https://github.com/docknetwork/sdk/blob/ffcf8bd6135b740465463042cb9a0a93c13fc672/tutorials/src/tutorial_revocation.md">Dock Revocation Registry</a><br><a href="../../open-source-community/trust-registry/JSON-RPC.md">Trust Registry JSON-RPC API</a><br></td><td>W3C</td></tr><tr><td>Credential Wallet</td><td>Credentials are stored in our wallet SDK using <a href="https://w3c-ccg.github.io/universal-wallet-interop-spec/">the W3C Universal Wallet 2020 specification</a>, as implemented in <a href="https://github.com/docknetwork/universal-wallet">our open source Universal Wallet library</a>.</td><td>W3C</td></tr></tbody></table>

## Interoperability <a href="#interoperability" id="interoperability"></a>

Dock believes that credentials are most useful when they are interoperable across service providers. Our W3C compliant credential format is designed for maximum interoperability. Our anonymous credential format adheres to many W3C standards, but are designed for maximum privacy protection. We also leverage standards from OpenID, IETF, DIF, and related organizations.

## Signature Formats

Dock supports following signature formats

<table><thead><tr><th width="186">Credential type</th><th width="466">Signature formats</th></tr></thead><tbody><tr><td>Non-anonymous</td><td><p>Certs defaults to ed25519 signatures</p><p>API can be used to choose between ed25519, sr25519, and secp256k1 </p></td></tr><tr><td>Anonymous</td><td><p>BBS2023</p><p>PS sigs</p></td></tr><tr><td>KVAC</td><td>BBDT16 as an algebraic MAC to build keyed anonymous credentials</td></tr></tbody></table>

### Encryption

#### Encryption at rest in Dock Certs

Credential documents are stored encrypted with ECDH-ES+A256KW using x25519 key agreement keys. The index is encrypted with searchable encryption.

Other data is stored on RDS and S3 using AWS's default encryption.

#### Encryption in transit

Queued messages are encrypted per the DIDComm Message packing
