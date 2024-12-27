# Issuing Paid Credentials (KVAC Algorithm Integration)

This guide provides step-by-step instructions for implementing the KVAC algorithm to issue and verify paid credentials using a series of API endpoints. Follow these instructions to integrate KVAC into your system effectively.

Download a sample Postman collection [here](../Postman_collections/Issuing%20KVAC%20credentials).

## Prerequisites

Before starting, ensure you have:

* DIDs for issuer (`did:dock:issuer`) and verifier (`did:dock:verifier`)
* A trust registry (`trust_registry_id`)
* A schema (`http://example.org/schema/kvac`)

## Step-by-Step Guide

### 1. Invite Participants to Trust Registry (issuer and verifier)

Invite issuers and verifiers to the trust registry and assign them the schema that will be used in the `KVAC` credential.

**POST /trust-registries/{trust\_registry\_id}/participants** This endpoint invites a participant to the trust registry with specified schemas they are allowed to issue or verify. Will be called by the trust registry convenor.

**Body:**

```json
{
  "issuerSchemas": ["http://example.org/schema/kvac"]
}
```

**POST /trust-registries/invitations/accept** This endpoint accepts an invitation to join a trust registry using a provided token. Will be called by a trust registry future member.

**Body:**

```json
{
  "did": "did:dock:issuer",
  "infoUrl": "https://info.org/issuer",
  "token": "inviteTokenIssuer"
}
```

**POST /trust-registries/{trust\_registry\_id}/participants** This endpoint invites a participant to the trust registry with specified schemas they are allowed to issue or verify. Will be called by the trust registry convenor.

**Body:**

```json
{
  "verifierSchemas": ["http://example.org/schema/kvac"]
}
```

**POST /trust-registries/invitations/accept** This endpoint accepts an invitation to join a trust registry using a provided token. Will be called by a trust registry future member.

**Body:**

```json
{
  "did": "did:dock:verifier",
  "infoUrl": "https://info.org/verifier",
  "token": "inviteTokenVerifier"
}
```

### 2. Assign Prices to Schemas

Assign a price to the schema in the trust registry. Prices are specified in "digits" to support fractional cents, where 1 cent is represented as 1,000,000 digits. This ensures precision in transactions and avoids issues related to floating-point arithmetic.

**POST /trust-registries/{trust\_registry\_id}/schemas/{schema\_id}/price** This endpoint assigns a price to a schema within the trust registry, enabling it to be used for paid credentials.

**Body:**

```json
{
  "currency": "USD",
  "digits": 1000000  // Represents 1 cent
}
```

### 3. List Schemas with Prices

Retrieve and verify the list of schemas with their assigned prices.

**GET /trust-registries/{trust\_registry\_id}/schemas** This endpoint retrieves all schemas within a trust registry, including the prices assigned to each schema.

**Response:**

```json
[
  {
    "schema": "http://example.org/schema/kvac",
    "prices": [
      {
        "digits": 1000000,
        "currency": "USD",
        "trustRegistryId": "trust_registry_id",
        "trustRegistryMetadata": {
          ...
        }
      }
    ]
  }
]
```

### 4. Issue Credentials

Issue credentials using the schemas. The credential must be a KVAC credential to enable paid credentials. The use of the `bbdt16` algorithm is required to enable KVAC and paid credentials.

**POST /credentials** This endpoint issues a KVAC credential based on the specified schema and issuer details.

**Body:**

```json
{
  "algorithm": "bbdt16",
  "credential": {
    "schema": "http://example.org/schema/kvac",
    "issuer": "did:dock:issuer",
    "name": "KVAC Credential",
    "issuanceDate": "2019-12-03T12:19:52Z",
    "expirationDate": "2029-12-03T12:19:52Z",
    "subject": {
      "id": "did:dock:subject",
      "name": "Subject Name",
      "favouriteDrink": "Coffee"
    }
  }
}
```

### 5. Create Proof Template

Create a proof template using the schema with a price associated and request for verification.

**POST /proof-templates** This endpoint creates a proof template specifying the requirements for verifying a credential.

**Body:**

```json
{
  "name": "KVAC Proof Template",
  "nonce": "1234567890",
  "request": {
    "name": "KVAC Request",
    "purpose": "KVAC Purpose",
    "input_descriptors": [
      {
        "id": "Credential 1",
        "name": "KVAC Request",
        "purpose": "KVAC Purpose",
        "constraints": {
          "fields": [
            { "path": ["$.credentialSchema.id"], "filter": { "const": "http://example.org/schema/kvac" } }
          ]
        }
      }
    ]
  }
}
```

### 6. Add the Proof Template to the Trust Registry

Add the proof template to the trust registry to enable it being used by other participants.

**POST /trust-registries/{trust\_registry\_id}/proof-templates** This endpoint adds a proof template to the trust registry, enabling it to be used for verification.

**Body:**

```json
{
  "id": "proof_template_id",
}
```

### 7. Create Proof Request

Create a proof request based on the proof template to verify the credential.

**POST /proof-templates/{template\_id}/request** This endpoint creates a proof request based on the specified proof template, which can then be used to verify a credential.

**Body:**

```json
{
  "did": "did:dock:verifier"
}
```

**Note:** Verifier DID is required when using paid schemas.

**Errors:**

* If using a did that is part of the trust registry but is not assigned as a verifier for that schema the verification process on step 6 will fail with the following error message: `Presentation could not be verified: Error: Verifier DID does not have permission to verify this credential`
* If using a did that is not part of the trust registry the verification process on step 6 will fail with the following message: `Presentation could not be verified: Error: This credential can only be verified by participants in the ${trust_registry_name} ecosystem. You can learn about the ecosystem by visiting this website: ${trust_registry_url}`

### 8. Verify Presentation

Using the [Truvera Wallet](../credential-wallet/download-truvera-wallet.md), scan the QR code received and follow the process to submit the verification.

### 9. Retrieve Trust Registry Reports

Fetch and verify trust registry reports to ensure proper billing and tracking.

**GET /trust-registries/{trust\_registry\_id}/reports** This endpoint retrieves reports from the trust registry, detailing verifications, fees, and other relevant information for auditing purposes.

**Response:**

```json
[
  {
    "trustRegistryId": "trust_registry_id",
    "verificationId": "572350a8-673a-490a-bed3-c001aa3f58a0",
    "verifierDID": "did:dock:verifier",
    "issuerDID": "did:dock:issuer",
    "schemaId": "http://example.org/schema/kvac",
    "currency": "USD",
    "verifierFee": "123456",
    "vendorFee": "6172",
    "created": "2024-08-08T08:53:50.524Z"
  }
]
```

### 10. Assigning additional schemas to participants

Add new schemas  to the Ecosystem by assigning them to each participant.

**PATCH/trust-registries/{registryId}/participants/{participantId}** This endpoint allows updating the Trust Registry participant.

```json
{
  "name": "string",
  "logoUrl": "string",
  "infoUrl": "string",
  "status": "string",
  "suspendedAt": "string",
  "issuerSchemas": [
    "http://example.org/schema/kvac2",
    "http://example.org/schema/kvac3"
  ],
  "verifierSchemas": [
    "http://example.org/schema/kvac2",
    "http://example.org/schema/kvac3"
  ]
}
```
