---
icon: landmark-flag
---

# Supported standards

Truvera is built on W3C open standards, it ensures that users can store their credentials on any digital wallet that adheres to these standards and that any stakeholder, wherever they are in the world, can verify the authenticity of the data as long as their verification system adheres to these standards. If there is a standard for which you would like further clarification or support, please [contact us](../support/).

## Standards bodies

* [World Wide Web Consortium (W3C)](https://www.w3.org/)
* [OpenID Foundation (OIDF)](https://openid.net/foundation/)
* [Decentralized Identity Foundation (DIF)](https://identity.foundation/)
* [Internet Engineering Task Force (IETF)](https://www.ietf.org/)

## Supported standards

Dock Supports the following open standards:

<table><thead><tr><th width="180">Technology</th><th width="367">Open Standard</th><th>Standard Body</th></tr></thead><tbody><tr><td>Data model</td><td><a href="https://www.w3.org/TR/2022/REC-vc-data-model-20220303/">W3C Verifiable Credentials (VCs) Data Model v1.1</a></td><td>W3C</td></tr><tr><td>Credential variant</td><td><p>Non-Anonymous</p><p><a href="https://www.w3.org/TR/vc-data-model/#json-web-token">W3C-VC with JWT (API only)</a></p><p><a href="https://www.w3.org/TR/vc-data-model/#json-ld">W3C-VC with JSON-LD and Ed25519Signature2020</a></p><p>Anonymous</p><p><a href="https://github.com/docknetwork/crypto-wasm-ts/tree/master/src/anonymous-credentials">W3C JSON-LD with BBS2023</a></p><p><a href="https://github.com/docknetwork/crypto-wasm-ts/tree/master/src/accumulator">W3C JSON-LD with BBDT16</a></p></td><td>W3C<br>IETF</td></tr><tr><td>Decentralized Identifier</td><td><p><a href="https://docs.cheqd.io/product/architecture/adr-list/adr-001-cheqd-did-method">DID:cheqd</a></p><p><a href="https://w3c-ccg.github.io/did-method-key/">DID:key</a></p></td><td>W3C</td></tr><tr><td>Credential Issuance</td><td><a href="https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0-14.html">OpenID for Verifiable Credential Issuance - draft 14</a><br></td><td>OIDF</td></tr><tr><td>Presentation</td><td>Default presentation exchange from <a href="https://identity.foundation/waci-didcomm/">DIF Wallet and Credential Interaction (WACI) v1.0 Draft</a> over <a href="https://identity.foundation/didcomm-messaging/spec/v2.1">DIDComm Messaging v2.1</a><br><a href="https://openid.net/specs/openid-4-verifiable-presentations-1_0-ID3.html">OpenID for Verifiable Presentations - draft 23</a><br></td><td>DIF<br>OIDF</td></tr><tr><td>Revocation</td><td><a href="https://www.w3.org/community/reports/credentials/CG-FINAL-vc-status-list-2021-20230102/">Verifiable Credential Status List 2021</a></td><td>W3C</td></tr><tr><td>Credential Wallet</td><td>Credentials are stored in our wallet SDK using <a href="https://w3c-ccg.github.io/universal-wallet-interop-spec/">the W3C Universal Wallet 2020 specification</a>, as implemented in <a href="https://github.com/docknetwork/universal-wallet">our open source Universal Wallet library</a>.</td><td>W3C</td></tr></tbody></table>

<figure><img src="../.gitbook/assets/Screenshot 2025-04-22 at 17.29.31.png" alt=""><figcaption></figcaption></figure>

## Key standards during issuance

<figure><img src="../.gitbook/assets/Screenshot 2025-04-22 at 17.30.27.png" alt=""><figcaption></figcaption></figure>

## Key standards during verification

<figure><img src="../.gitbook/assets/Screenshot 2025-04-22 at 17.30.54.png" alt=""><figcaption></figcaption></figure>

## Signature formats

Truvera supports following signature formats

<table><thead><tr><th width="186">Credential variant</th><th width="466">Signature formats</th></tr></thead><tbody><tr><td>Standard signature</td><td>ed25519</td></tr><tr><td>Anonymous</td><td>dockbbs23</td></tr><tr><td>Anonymous Ecosystem-Bound</td><td>BBDT16 as an algebraic MAC to build keyed anonymous credentials</td></tr><tr><td>EUDI</td><td>SD-JWT-VC</td></tr></tbody></table>

### Encryption

#### Encryption at rest in Truvera Workspace

Credential documents are stored encrypted with ECDH-ES+A256KW using x25519 key agreement keys. The index is encrypted with searchable encryption.

Other data is stored on RDS and S3 using AWS's default encryption.

#### Encryption in transit

Queued messages are encrypted per the DIDComm Message packing.

## Interoperability

Truvera believes that credentials are most useful when they are interoperable across service providers. Our W3C compliant credential format is designed for maximum interoperability. Our anonymous credential format adheres to many W3C standards, but are designed for maximum privacy protection. We also leverage standards from OpenID, IETF, DIF, and related organizations.
