# Trust Registry Integration Guide

This guide provides step-by-step instructions for integrating a trust registry into any application using a series of API endpoints. This guide assumes a basic understanding of essential elements such as DIDs, JWTs, and specific configurations.

Download a sample Postman collection [here](../../../Postman\_collections/Ecosystem%20Tools%20\(Trust%20Registry\)).

## Prerequisites

Before starting, ensure you have:

* A DID for the convener (`did:dock:convener`) with associated profile
* A DID for the participant (`did:dock:pariticpant`) with associated profile

## Step-by-Step Guide

### 1. Create a Trust Registry

Create a trust registry using the convener's DID and relevant metadata.

**POST /trust-registries** This endpoint creates a new trust registry with the provided metadata and convener DID.

**Body:**

```json
{
  "name": "Dock Trust Registry",
  "description": "Qui labore ad consequat exercitation excepteur nulla deserunt qui sunt deserunt laboris quis dolore voluptate!",
  "logoUrl": "https://logo.com/registry",
  "ecosystemUrl": "https://myecosystem.com",
  "governanceFramework": "Consectetur non anim incididunt duis ullamco est in irure labore quis.",
  "governanceFrameworkVersion": "1.0.0",
  "convener": "did:dock:convener"
}
```

**Response:**

```json
{
  "id": "0x30eb6adc982f60e11d77044e7dec02c89e24af32f05be6a17ea204d155a36fcb",
  "slug": "my-trust-registry-1",
  "nonce": "0xc54b08e7f82d4689",
  "convener": "did:dock:convener",
  "convenerName": "My Convener",
  "convenerLogoUrl": "https://dock.io/convener.png",
  "created": "2024-08-16T12:39:32.060Z",
  "name": "Dock Trust Registry",
  "description": "Qui labore ad consequat exercitation excepteur nulla deserunt qui sunt deserunt laboris quis dolore voluptate!",
  "logoUrl": "https://logo.com/registry",
  "ecosystemUrl": "https://myecosystem.com",
  "governanceFramework": "Consectetur non anim incididunt duis ullamco est in irure labore quis.",
  "governanceFrameworkVersion": "1.0.0"
}
```

### 2. Add Participants to the Trust Registry

Invite participants (e.g., issuers, verifiers) to the trust registry and assign schemas.

**Note:** Roles are automatically assigned based on the schemas allocated to a participant:

* If a participant can only issue credentials using the assigned schemas, they are designated as an `issuer`.
* If a participant can only verify credentials using the assigned schemas, they are designated as a `verifier`.
* If a participant can both issue and verify, they are designated as a `verifier+issuer`. A participant without any assigned schemas will have a `verifier` role but will only be able to verify public schemas within the ecosystem.

**POST /trust-registries/{trust\_registry\_id}/participants** This endpoint invites a participant to the trust registry with specified schemas they are allowed to issue or verify. Will be called by the trust registry convener.

**Body:**

```json
{}
```

**Note:** An empty body will result in a `verifier` role for the participant, allowing them only to verify `public` schemas. Issuer and verifier schemas can be assigned in the invitation by adding the schema IDs to the request body.

```json
{
  "issuerSchemas": ["https://schema.com/invitation/issuer"],
  "verifierSchemas": ["https://schema.com/invitation/verifier"]
}
```

**Response:**

```json
{
  "link": "http://127.0.0.1:3000/ecosystems?token=inviteToken"
}
```

**Accept the invitation:**

**POST /trust-registries/invitations/accept** This endpoint accepts an invitation to join a trust registry using a provided token. Will be called by a trust registry participant to join the registry.

**Body:**

```json
{
  "did": "did:dock:participant",
  "infoUrl": "https://participant.com",
  "token": "inviteToken"
}
```

**Response:**

```json
{
  "id": "64c257f0-2920-408b-adef-8fd3f40c1b3c",
  "userId": 1,
  "name": "My Participant",
  "description": "Proident proident enim cupidatat ad culpa anim ullamco qui aliquip.",
  "did": "did:dock:participant",
  "logoUrl": "https://dock.io/participant.png",
  "infoUrl": "https://participant.com",
  "status": "active",
  "role": "verifier",
  "created": "2024-08-16T12:42:56.682Z",
  "suspendedAt": ""
}
```

**Note:**

* The DID's profile name, description, and logo will be applied to the participant. The name and logo are required for DIDs that will be used as participants.
* Invitations can be snoozed using `POST /trust-registries/invitations/snooze`
* Invitations can be declined using `POST /trust-registries/invitations/decline`

**Error Handling:**

* Attempting to reuse an invite token will result in an error.
* Inviting a participant that already exists in the registry may also cause an error.

### 3. Retrieve Trust Registry Details

Retrieve details of the trust registry, including participants and schemas.

**GET /trust-registries/{trust\_registry\_id}** This endpoint retrieves detailed information about a specific trust registry. Useful for both the convener and participants to get an overview of the registry.

**Response:**

```json
{
  "id": "0x30eb6adc982f60e11d77044e7dec02c89e24af32f05be6a17ea204d155a36fcb",
  "slug": "my-trust-registry-1",
  "nonce": "0xc54b08e7f82d4689",
  "convener": "did:dock:convener",
  "convenerName": "My Convener",
  "convenerLogoUrl": "https://dock.io/convener.png",
  "created": "2024-08-16T12:39:32.060Z",
  "name": "Dock Trust Registry",
  "description": "Qui labore ad consequat exercitation excepteur nulla deserunt qui sunt deserunt laboris quis dolore voluptate!",
  "logoUrl": "https://logo.com/registry",
  "ecosystemUrl": "https://myecosystem.com",
  "governanceFramework": "Consectetur non anim incididunt duis ullamco est in irure labore quis.",
  "governanceFrameworkVersion": "1.0.0",
  "created": "2024-08-16T12:50:30.944Z",
  "isOwner": true, //whether the current user is the owner of the ecosystem
  "isUnmaintained": false, // whether the trust registry administrator has no active subscription
  "issuerCount": 0, // the number of issuers in the trust registry
  "verifierCount": 1 // the number of verifier in the trust registry
}
```

**Note:**

* `slug` can be used instead of `trust_registry_id`
* The public info about a trust registry is available at `GET /trust-registries/{trust_registry_id}/public`

### 4. Update Trust Registry Metadata

Update the metadata of an existing trust registry.

**PATCH /trust-registries/{trust\_registry\_id}** This endpoint updates the metadata of an existing trust registry. Will be called by the convener to update details like the name, description, or governance framework.

**Body:**

```json
{
  "name": "Updated Name",
  "description": "Updated description",
  "logoUrl": "https://logo.com/updated",
  "ecosystemUrl": "https://updatedecosystem.com",
  "governanceFramework": "This is a markdown document describing my framework version two!",
  "governanceFrameworkVersion": "2.0.0"
}
```

**Response:**

```json
{
  "id": "0x62459be8cef6cd405cc6838ed3f678bcf0784393fce25f42307f37001255d07c",
  "slug": "updated-name-359",
  "nonce": "0x9f49c2d9e481d5c7",
  "convener": "did:dock:convener",
  "convenerName": "My Convener",
  "convenerLogoUrl": "https://dock.io/convener.png",
  "created": "2024-08-16T13:02:49.456Z",
  "isOwner": true,
  "isUnmaintained": false,
  "name": "Updated Name",
  "description": "Updated the description",
  "logoUrl": "https://logo.com/ecosystemnew",
  "ecosystemUrl": "https://myecosystemnew.com",
  "governanceFramework": "This is a markdown document describing my framework version two!",
  "governanceFrameworkVersion": "2.0.0",
  "issuerCount": 0,
  "verifierCount": 1
}
```

### 5. Manage Trust Registry Participants

#### a. Update Participant Information

Update a participant's information within the registry.

**PATCH /trust-registries/{trust\_registry\_id}/participants/{participant\_id}/info** This endpoint updates a participant’s information within the trust registry. It can be used only by the participant to update his own informations.

**Body:**

```json
{
  "infoUrl": "https://newinfo.com"
}
```

**Response:**

```json
{
  "id": "f6ea7dd8-2a99-4c1a-9985-a41f12b4a7da",
  "userId": 1,
  "name": "My Participant",
  "description": "Proident proident enim cupidatat ad culpa anim ullamco qui aliquip.",
  "did": "did:dock:participant",
  "logoUrl": "https://newlogo.com",
  "infoUrl": "https://newinfo.com",
  "status": "active",
  "role": "verifier",
  "issuerSchemas": [],
  "verifierSchemas": [],
  "created": "2024-08-16T13:22:38.213Z",
  "suspendedAt": ""
}
```

**Note:** The name and logo can be updated by modifying the associated DID profile's information.

#### b. Suspend/Unsuspend Participants

Suspend or unsuspend a participant's status within the registry.

**PATCH /trust-registries/{trust\_registry\_id}/participants/{participant\_id}** This endpoint updates a participant’s information within the trust registry, such as their assigned schemas or their status (e.g., suspended or active).

**Body:**

```json
{
  "status": "suspended" // or "active"
}
```

**Response:**

```json
{
  "id": "f6ea7dd8-2a99-4c1a-9985-a41f12b4a7da",
  "userId": 1,
  "name": "My Participant",
  "description": "Proident proident enim cupidatat ad culpa anim ullamco qui aliquip.",
  "did": "did:dock:participant",
  "logoUrl": "https://dock.io/participant.png",
  "infoUrl": "https://participant.com",
  "status": "suspended",
  "role": "verifier",
  "issuerSchemas": [],
  "verifierSchemas": [],
  "created": "2024-08-16T13:22:38.213Z",
  "suspendedAt": "2024-08-16T14:22:38.213Z"
}
```

#### c. Get all participants

Get a list of all participants in the trust registry

**GET /trust-registries/{trust\_registry\_id}/participants** This endpoint retrieves detailed information about the participants from the trust registry

**Response:**

```json
{
  "total": 1,
  "list": [
    {
      "id": "f6ea7dd8-2a99-4c1a-9985-a41f12b4a7da",
	  "userId": 1,
	  "name": "My Participant",
	  "description": "Proident proident enim cupidatat ad culpa anim ullamco qui aliquip.",
	  "did": "did:dock:participant",
	  "logoUrl": "https://dock.io/participant.png",
	  "infoUrl": "https://participant.com",
	  "status": "active",
	  "role": "verifier",
	  "issuerSchemas": [],
	  "verifierSchemas": [],
	  "created": "2024-08-16T13:22:38.213Z",
	  "suspendedAt": ""
    }
  ]
}
}
```

### 6. Manage Schemas

#### a. Assign Schemas to Participants

Assign specific schemas to participants based on their roles.

**PATCH /trust-registries/{trust\_registry\_id}/participants/{participant\_id}** This endpoint updates a participant’s information within the trust registry, such as their assigned schemas or their status (e.g., suspended or active). Will be called by the convener to manage participant roles and schemas.

**Body:**

```json
{
  "issuerSchemas": ["https://schema.com/issuer"],
  "verifierSchemas": ["https://schema.com/verifier"]
}
```

**Response:**

```json
{
  "id": "f6ea7dd8-2a99-4c1a-9985-a41f12b4a7da",
  "userId": 1,
  "name": "My Participant",
  "description": "Proident proident enim cupidatat ad culpa anim ullamco qui aliquip.",
  "did": "did:dock:participant",
  "logoUrl": "https://dock.io/participant.png",
  "infoUrl": "https://participant.com",
  "status": "active",
  "role": "verifier",
  "issuerSchemas": ["https://schema.com/issuer"],
  "verifierSchemas": ["https://schema.com/verifier"],
  "created": "2024-08-16T13:22:38.213Z",
  "suspendedAt": ""
}
```

#### b. Get Trust Registry Schemas

Retrieve schemas associated with the trust registry.

**GET /trust-registries/{trust\_registry\_id}/schemas** This endpoint retrieves the list of schemas associated with a specific trust registry, including participant counts and public visibility. Useful for both the convener and participants.

**Response:**

```json
{
  "id": "https://schema.com/verifier",
  "name": "https://schema.com/verifier",
  "public": false, // if a schema has no verifier assigned it is a public schema and can be verifier by anyone in the ecosystem
  "prices": [], // assigned prices for this schema
  "topParticipants": [
    {
      "id": "0e5ed250-382a-496c-a59e-d7b0f9f2f3d3",
      "name": "My Participant",
      "description": "Proident proident enim cupidatat ad culpa anim ullamco qui aliquip.",
      "did": "did:key:participant",
      "logoUrl": "https://dock.io/participant.png",
      "suspendedAt": ""
    }
  ], // top 5 participants using this schema
  "participantCount": 1 // the total number of participants using this schema
}
```

### 7. Manage Proof Templates

#### a. Assign Proof Templates to the Trust Registry

Assign proof templates to the trust registry to enable credential verification. This will allow the verifiers in the trust registry to use the proof-template

**POST /trust-registries/{trust\_registry\_id}/proof-templates** This endpoint assigns a proof template to the trust registry, enabling it for use in credential verification. Will be called by the convener.

**Body:**

```json
{
  "id": "proof_template_id"
}
```

**Response:**

```json
{}
```

#### b. Retrieve Proof Templates

Retrieve proof templates associated with the trust registry.

**GET /trust-registries/{trust\_registry\_id}/proof-templates** This endpoint retrieves the list of proof templates associated with the trust registry. Useful for both the convener and participants.

**Response:**

```json
{
  "total": 1,
  "list": [
    {
      "id": "proof_template_id",
      "created": "2024-08-16T13:36:54.776Z",
      "name": "Proof request"
    }
  ]
}
```

### 8. Delete Trust Registry Entities

#### a. Delete a Trust Registry Participant

Remove a participant from the trust registry.

**DELETE /trust-registries/{trust\_registry\_id}/participants/{participant\_id}** This endpoint removes a participant from the trust registry. Will be called by the convener to manage the registry’s participants.

**Response:**

```json
{}
```

#### b. Delete a Trust Registry Proof Template

Remove a proof template from the trust registry.

**DELETE /trust-registries/{trust\_registry\_id}/proof-templates/{template\_id}** This endpoint removes a proof template from the trust registry. Will be called by the convener to manage the registry’s proof templates.

**Response:**

```json
{}
```

#### c. Delete a Trust Registry

Delete the entire trust registry.

**DELETE /trust-registries/{trust\_registry\_id}** This endpoint deletes the entire trust registry. Will be called by the convener when the trust registry is no longer needed.

**Response:**

```json
{}
```
