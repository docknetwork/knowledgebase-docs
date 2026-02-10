# Integrating the Cloud Wallet

### Overview

This guide walks through a simple example of using the Truvera Cloud Wallet for credential storage and integrating it to build a privacy-first identity verification flow using:

* **Truvera Web Wallet SDK** ([@docknetwork/wallet-sdk-web](https://www.npmjs.com/package/@docknetwork/wallet-sdk-web)) - client-side cloud wallet
* **Truvera REST API** - server-side credential issuance and proof verification

The flow has three actors: **Issuer** (e.g., a bank), **Holder** (user's cloud wallet), and **Verifier** (e.g., an exchange).

***

### Prerequisites

You'll need these from the [Truvera Dashboard](https://truvera.io/):

| Secret                  | Purpose                                                                 |
| ----------------------- | ----------------------------------------------------------------------- |
| TRUVERA\_API\_KEY       | REST API authentication                                                 |
| TRUVERA\_API\_URL       | API base URL (e.g., https://api-testnet.dock.io)                        |
| TRUVERA\_EDV\_AUTH\_KEY | Encrypted Data Vault access for cloud wallets (contact support@dock.io) |
| TRUVERA\_ISSUER\_DID    | DID for credential issuance                                             |
| TRUVERA\_VERIFIER\_DID  | DID for proof verification                                              |

You also need a [**Schema**](../../../truvera-api/api-docs.md) and a  [**Proof Template**](../../../truvera-api/presentations/proof-templates.md) configured in the Truvera workspace with your [Issuer DID](../../../truvera-api/dids.md) added as a trusted issuer.

***

### 1. Wallet SDK -- Client-Side

#### Install

```bash
npm install @docknetwork/wallet-sdk-web@^0.0.10
```

#### Initialize a New Wallet

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

#### Restore an Existing Wallet

```typescript
// Same call, just pass the stored mnemonic
const wallet = await TruveraWebWallet.initialize({
  edvUrl: 'https://edv.dock.io',
  edvAuthKey: '<your-edv-auth-key>',
  networkId: 'testnet',
  mnemonic: '<stored-mnemonic>'
});
```

#### Import a Credential (OID4VC)

```typescript
// offerUrl comes from the issuance API (see Section 2)
const credential = await wallet.addCredential(offerUrl);
```

#### List Credentials

```typescript
const credentials = await wallet.getCredentials();
// Returns: [{ id: "urn:uuid:...", type: [...], credentialSubject: {...}, ... }]
```

#### Delete a Credential

```typescript
// Access the inner wallet object for removeDocument
const innerWallet = (wallet as any).wallet;
await innerWallet.removeDocument(credentialId);
```

#### Submit a Zero-Knowledge Presentation

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

***

### 2. Truvera REST API -- Server-Side

All API calls use dual-header authentication:

```
DOCK-API-TOKEN: <your-api-key>
Authorization: Bearer <your-api-key>
Content-Type: application/json
```

#### 2a. Issue a Credential

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

**Step 2: Generate an OID4VC Offer**

```
POST {API_URL}/openid/credential-offers
```

```json
{ "id": "<issuer-id-from-step-1>" }
```

Response: { "url": "openid-credential-offer://...", "id": "..." }

The url is what you pass to wallet.addCredential().

***

#### 2b. Create a Proof Request

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

***

#### 2c. Poll for Verification Result

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

### 3. End-to-End Flow Summary

```
1. SETUP   - Create Issuer DID and Verifier DID in Truvera workspace   - Create a Proof Template with ZK predicates (e.g., age >= 18)   - Add Issuer DID to template's trusted issuers2. ISSUANCE (Bank/Issuer side)   POST /openid/issuers          --> get issuerId   POST /openid/credential-offers --> get offerUrl   wallet.addCredential(offerUrl) --> credential stored in EDV3. VERIFICATION (Exchange/Verifier side)   POST /proof-templates/{id}/request --> get proofRequestId + qr URL   wallet.submitPresentation({ proofRequestUrl: qr }) --> ZKP submitted   GET /proof-requests/{id}  (poll) --> verified: true
```

### 4. Key Gotchas

| Issue                                    | Solution                                                   |
| ---------------------------------------- | ---------------------------------------------------------- |
| Vault indices does not exist on init     | Retry up to 3 times with 1s delay                          |
| Proof submission returns undefined error | Ensure Issuer DID is in template's trusted issuers         |
| removeCredential not found               | Use wallet.wallet.removeDocument(id) (inner wallet object) |
| Proof never verifies                     |                                                            |
|                                          |                                                            |

***

### 5. Environment Variables Reference

| Variable                | Where Used                    | Purpose                   |
| ----------------------- | ----------------------------- | ------------------------- |
| TRUVERA\_API\_KEY       | Server only                   | API authentication        |
| TRUVERA\_API\_URL       | Server only                   | Base URL for REST API     |
| TRUVERA\_EDV\_AUTH\_KEY | Fetched by client via backend | Cloud wallet vault access |
| TRUVERA\_ISSUER\_DID    | Server only                   | Signs credentials         |
| TRUVERA\_VERIFIER\_DID  | Server only                   | Creates proof requests    |
