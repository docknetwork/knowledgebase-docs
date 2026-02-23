# Reusable identity without a wallet application

## Overview

Users are often asked to perform duplicative identity checks when doing business with an organization. Instead of asking repeatedly for the same evidence, it is better to issue a credential that can be verified the next time the user's identity data is required. However, most users will not have an identity wallet application already provisioned. The Truvera Cloud Wallet allows your platform to store credentials on behalf of your users and help your users to access them when needed.

This guide walks through a simple example of provisioning a wallet for credential storage and integrating it in issuer and verifier services. It achieves this using the following Truvera products:

* [**Truvera Wallet SDK**](../credential-wallet/wallet-sdk/) ([@docknetwork/wallet-sdk-web](https://www.npmjs.com/package/@docknetwork/wallet-sdk-web)) — which is used by the client-side wallet to store credentials in [the Truvera Cloud Wallet](../credential-wallet/wallet-sdk/cloud-wallet.md)'s Encrypted Data Vault (EDV)
* [**Truvera REST API**](../truvera-api/) — which is accessed by your [credential issuance](../truvera-api/credentials.md#issue-credentials) and [proof verification](../truvera-api/presentations/) services

The flow has three actors: **Issuer** (e.g., a bank), **Holder** (user's cloud wallet), and **Verifier** (e.g., a financial exchange). For simplicity, this example combines these roles by allowing the issuer and verifier to have access to the holder's wallet access key. It also uses [the OpenID4VCs protocol](../key-standards/interoperability-with-openid.md) which many developers are already familiar with. Once you understand the example, you should review [the next steps](reusable-identity-without-a-wallet-application.md#next-steps) for guidance on a production architecture.

### Example flow

```
1. SETUP   
- Create Issuer DID and Verifier DID in Truvera workspace   
- Create a Proof Template with ZK predicates (e.g., age >= 18)   
- Add Issuer DID to template's trusted issuers
2. ISSUANCE (Bank/Issuer side)
    POST /openid/issuers  --> get issuerId   
    POST /openid/credential-offers --> get offerUrl   
    wallet.addCredential(offerUrl) --> credential stored in EDV
3. VERIFICATION (Exchange/Verifier side)
    POST /proof-templates/{id}/request --> get proofRequestId + qr URL   
    wallet.submitPresentation({ proofRequestUrl: qr }) --> ZKP submitted
    GET /proof-requests/{id}  (poll) --> verified: true
```

***

### Prerequisites

You'll need these items from the [Truvera Workspace](https://truvera.io/):

| Secret                 | Purpose                                                   | Where used                |
| ---------------------- | --------------------------------------------------------- | ------------------------- |
| TRUVERA\_API\_KEY      | REST API authentication                                   | Issuer / Verifier service |
| TRUVERA\_API\_URL      | Base URL for REST API (e.g., https://api-testnet.dock.io) | Issuer / Verifier service |
|                        |                                                           |                           |
| TRUVERA\_ISSUER\_DID   | DID for signing credentials during issuance               | Issuer service            |
| TRUVERA\_VERIFIER\_DID | DID for creating proof requests during verification       | Verifier service          |

You also need a [**Schema**](../truvera-api/api-docs.md) and a  [**Proof Template**](../truvera-api/presentations/proof-templates.md) configured in the Truvera workspace with your [Issuer DID](../truvera-api/dids.md) added as a trusted issuer.

To create the cloud wallet, you will also need to request a key from Truvera Support (support@dock.io):

| Secret                  | Purpose                                       | Where used             |
| ----------------------- | --------------------------------------------- | ---------------------- |
| TRUVERA\_EDV\_AUTH\_KEY | Encrypted Data Vault access for cloud wallets | Wallet service backend |

***

## Example

### 1. Wallet SDK - client side

#### Install

```bash
npm install @docknetwork/wallet-sdk-web@^0.0.10
```

#### Initialize a new wallet

```typescript
import TruveraWebWallet from '@docknetwork/wallet-sdk-web';

// Generate a mnemonic (save this -- it's the recovery key)
const { masterKey, mnemonic } = await TruveraWebWallet.generateCloudWalletMasterKey();

// Initialize the cloud wallet
const wallet = await TruveraWebWallet.initialize({
  edvUrl: 'https://edv.dock.io',
  edvAuthKey: '<your-edv-auth-key>',  // fetch from backend, never hardcode
  networkId: 'testnet',               // or 'mainnet'
  mnemonic
});

// Get the wallet's DID
const didDoc = await wallet.getDID();
const did = didDoc.id;  // e.g., "did:dock:5F3s..."
```

> **Tip:** Wallet initialization can intermittently fail with "Vault indices does not exist" errors. Use a retry loop (3 attempts, 1s delay).

#### Restore an existing wallet

```typescript
// Same call, just pass the stored mnemonic
const wallet = await TruveraWebWallet.initialize({
  edvUrl: 'https://edv.dock.io',
  edvAuthKey: '<your-edv-auth-key>',
  networkId: 'testnet',
  mnemonic: '<stored-mnemonic>'
});
```

#### Import a credential (OID4VC)

```typescript
// offerUrl comes from the issuance API (see Section 2)
const credential = await wallet.addCredential(offerUrl);
```

#### List credentials

```typescript
const credentials = await wallet.getCredentials();
// Returns: [{ id: "urn:uuid:...", type: [...], credentialSubject: {...}, ... }]
```

#### Delete a credential

```typescript
// Access the inner wallet object for removeDocument
const innerWallet = (wallet as any).wallet;
await innerWallet.removeDocument(credentialId);
```

#### Submit a zero-knowledge presentation

```typescript
const result = await wallet.submitPresentation({
  credentials: [{
    id: credential.id,
    attributesToReveal: [
      'credentialSubject.age',
      'credentialSubject.bankTenure'
    ]
  }],
  proofRequestUrl: '<qr-url-from-proof-request>'  // the `qr` field from the API
});
```

> **Important:** The attributesToReveal must match the input\_descriptors in your proof template. The proofRequestUrl must be the qr field returned by the API, not a manually constructed URL.

### 2. Truvera REST API - server side

All API calls use dual-header authentication:

```
DOCK-API-TOKEN: <your-api-key>
Authorization: Bearer <your-api-key>
Content-Type: application/json
```

#### 2a. Issue a credential

**Step 1: Create an OpenID Issuer**

```
POST {API_URL}/openid/issuers
```

```json
{
  "claimMap": {
    "age": "age",
    "fullName": "fullName",
    "bankTenure": "bankTenure",
    "dateOfBirth": "dateOfBirth"
  },
  "credentialOptions": {
    "algorithm": "dockbbs",
    "credential": {
      "type": ["VerifiableCredential", "BankIdentity"],
      "subject": {
        "age": 30,
        "fullName": "John Doe",
        "bankTenure": 8,
        "dateOfBirth": "1994-05-15"
      },
      "issuanceDate": "2025-01-01T00:00:00Z",
      "expirationDate": "2026-01-01T00:00:00Z",
      "issuer": "did:dock:<your-issuer-did>"
    }
  }
}
```

Response: { "id": "\<issuer-id>", ... }

> **Critical:** Use algorithm: "dockbbs" for BBS+ signatures. This is required for ZK proof generation.

**Step 2: Generate an OID4VC offer**

```
POST {API_URL}/openid/credential-offers
```

```json
{ "id": "<issuer-id-from-step-1>" }
```

Response: { "url": "openid-credential-offer://...", "id": "..." }

The url is what you pass to wallet.addCredential().

#### 2b. Create a proof request

```
POST {API_URL}/proof-templates/{templateId}/request
```

```json
{ "did": "did:dock:<your-verifier-did>" }
```

Response:

```json
{
  "id": "<proof-request-id>",
  "qr": "https://creds-testnet.dock.io/proof/...",
  ...
}
```

The qr field is the URL you pass to wallet.submitPresentation().

> **Important:** The Issuer DID must be added to the proof template's "trusted issuers" list in the Truvera workspace. Otherwise, proof generation will silently fail.

#### 2c. Poll for verification result

```
GET {API_URL}/proof-requests/{proofRequestId}
```

Response:

```json
{
  "id": "...",
  "verified": true,
  "presentation": { ... },
  "status": "verified"
}
```

Poll this endpoint (e.g., every 3 seconds) until verified === true. Use exponential backoff for network resilience.

***

## Next Steps

Once you understand the above example, you should separate the wallet into a privacy-by-design user-controlled web application. The issuer and verifier should not have direct access to the key for the user's wallet. Instead, we recommend the following flow.

When a user is onboarding,

1. The user will complete identity proofing as required by existing policies,
2. Then the issuer service calls the client wallet service to provision a cloud wallet on behalf of the user,
3. That service [assists the user in defining their key](../credential-wallet/wallet-sdk/cloud-wallet.md#multi-key-authentication) as required for your use case (using a biometric, passkey, or other login method),
4. The wallet service then returns to the issuer the DID of the new wallet,
5. The issuer service can then call the REST API to issue credentials with the attributes that were established during identity proofing. These credentials can be issued directly into the user's wallet using the DIDComm protocol.

When a user later needs to provide those credentials,

1. The verifier service calls the REST API to create a proof request for the needed data,
2. The verifier service directs the user to the client wallet service with the proof request URL,
3. The wallet server helps the user to generate their access key using the same method as during onboarding, or a recovery method,
4. The user can then approve the sharing of the credentials to fulfill the proof request,
5. And the data is returned to the verifier.
