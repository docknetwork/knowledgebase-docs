# API Documentation



###

Schemas

> Object Schemas

Data Schemas are useful when enforcing a specific structure on a collection of data like a Verifiable Credential. Other than that, Data Verification schema and Data Encoding Schemas are used to verify and map the structure and contents of a Verifiable Credential.

These are the schemas used in all API operations mentioned before, such as Error, Credential, Jobs, Anchor, Registry, and so on.

For a detailed example of the schema workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/schemaFlow.js).

### Error <a href="#tocs_error" id="tocs_error"></a>

```json
{
  "status": 0,
  "type": "string",
  "message": "string"
}

```

This is a schema for an API Error.

#### Properties

| Name    | Type    | Required | Description           |
| ------- | ------- | -------- | --------------------- |
| status  | integer | false    | Status of the error.  |
| type    | string  | false    | Type of the error.    |
| message | string  | false    | Message of the error. |

### Hex32 <a href="#tocs_hex32" id="tocs_hex32"></a>

```json
"string"

```

32 byte hex string. Ignoring higher base (base64) for simplicity.

#### Properties

| Name  | Type   | Required | Description                                                       |
| ----- | ------ | -------- | ----------------------------------------------------------------- |
| Hex32 | string | false    | 32 byte hex string. Ignoring higher base (base64) for simplicity. |

### JobStartedResult <a href="#tocs_jobstartedresult" id="tocs_jobstartedresult"></a>

```json
{
  "id": "string",
  "data": {
    "did": "did:dock:xyz",
    "hexDid": "0x00",
  }
}

```

Object containing unique id of the background task and associated data. This id can be used to query the job status.

#### Properties

| Name | Type                               | Description                                                                    |
| ---- | ---------------------------------- | ------------------------------------------------------------------------------ |
| id   | [JobId](index.html.md#schemajobid) | Unique id of the background task. This id can be used to query the job status. |
| data | object                             | Data of the object.                                                            |

### JobId <a href="#tocs_jobid" id="tocs_jobid"></a>

```json
"string"

```

Unique id of the background task. This id can be used to query the job status

### JobStatus <a href="#tocs_jobstatus" id="tocs_jobstatus"></a>

```json
"in_progress"

```

This is a schema used in Job operation to get a status of the job.

#### Enumerated Values

| Property  | Value                                                   | Description          |
| --------- | ------------------------------------------------------- | -------------------- |
| JobStatus | todo **or** finalized **or** in\_progress **or** error. | Job Status variants. |

### JobDesc <a href="#tocs_jobdesc" id="tocs_jobdesc"></a>

```json
{
  "id": "string",
  "result": {},
  "status": "todo",

}

```

This is a schema used in Job operation to get description of the job including the result if it is available.

#### Properties

| Name   | Type                                       | Description                                                                    |
| ------ | ------------------------------------------ | ------------------------------------------------------------------------------ |
| id     | [JobId](index.html.md#schemajobid)         | Unique id of the background task. This id can be used to query the job status. |
| status | [JobStatus](index.html.md#schemajobstatus) | Status of the job.                                                             |
| result | object                                     | false                                                                          |

### DIDDock <a href="#tocs_diddock" id="tocs_diddock"></a>

```json
"did:dock:xyz"

```

DID as fully qualified, e.g., `did:dock:`.

#### Properties

| Name | Type   | Required | Description                                                                                                           |
| ---- | ------ | -------- | --------------------------------------------------------------------------------------------------------------------- |
| DID  | string | false    | DID as fully qualified, e.g., `did:dock:`. You cannot specify your own DID, the DID value will be randomly generated. |

### KeyType <a href="#tocs_keytype" id="tocs_keytype"></a>

```json
"sr25519"

```

This is a schema type of public key for DID.

#### Enumerated Values

| Property | Value                                   | Description           |
| -------- | --------------------------------------- | --------------------- |
| KeyType  | sr25519 **or** ed25519 **or** secp256k1 | keyType DID variants. |

### SigType <a href="#tocs_sigtype" id="tocs_sigtype"></a>

```json
"Sr25519Signature2020"

```

This is a schema used in Presentation operation that represents a type of signature.

#### Enumerated Values

| Property | Value                                                                               | Description                 |
| -------- | ----------------------------------------------------------------------------------- | --------------------------- |
| SigType  | Sr25519Signature2020 **or** Ed25519Signature2018 **or** EcdsaSecp256k1Signature2019 | SigType signature variants. |

### ProofPurpose <a href="#tocs_proofpurpose" id="tocs_proofpurpose"></a>

```json
"assertionMethod"

```

This is a schema that represents a purpose of credential.

#### Enumerated Values

| Property     | Value                                 | Description            |
| ------------ | ------------------------------------- | ---------------------- |
| ProofPurpose | assertionMethod **or** authentication | Purpose of credential. |

### Context <a href="#tocs_context" id="tocs_context"></a>

```json
[
  "string"
]

```

This is a schema that represents a JSON-LD context used in DID and Presentation.

### DIDDoc <a href="#tocs_diddoc" id="tocs_diddoc"></a>

```json
{
  "@context": [
    "string"
  ],
  "id": "did:dock:xyz",
  "authentication": [
    {}
  ]
}

```

This is a schema that represents a DID document. The current set of properties is incomplete

#### Properties

| Name           | Type                                   | Required | Description                                |
| -------------- | -------------------------------------- | -------- | ------------------------------------------ |
| @context       | [Context](index.html.md#schemacontext) | false    | JSON-LD context.                           |
| id             | [DIDDock](index.html.md#schemadiddock) | false    | DID as fully qualified, e.g., `did:dock:`. |
| authentication | array                                  | false    | DID authentication.                        |

### Credential <a href="#tocs_credential" id="tocs_credential"></a>

```json
{
  "context": [
    "string"
  ],
  "type": [
    "string"
  ],
  "subject": {},
  "issuer": "did:dock:xyz",
  "issuanceDate": "2019-08-24T14:15:22Z",
  "expirationDate": "2019-08-24T14:15:22Z",
  "status": "90b7dc6e8642bf1425c5a5ef2c3ff62bb689770843fdc0e2d79b97beb6c73311"
}

```

This is a schema that represents a credential format expected by API caller when issuing a credential.

#### Properties

| Name           | Type                                   | Required | Description                                                                                                                                                                                                                                                                    |
| -------------- | -------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| id             | string(uri)                            | false    | Credential ID. The default value is a creds.dock.io uri with random ID.                                                                                                                                                                                                        |
| context        | \[string or object]                    | false    | Credential context array of string URIs and/or embedded JSON-LD context objects. If no context parameter is supplied, we will auto generate contexts for you. If you do supply this parameter, you must ensure that all JSON-LD terms are defined. This is for advanced users. |
| type           | \[string]                              | false    | Credential type. The default value is \['VerifiableCredential']                                                                                                                                                                                                                |
| subject        | object or \[object]                    | true     | Credential subject or subjects array.                                                                                                                                                                                                                                          |
| schema         | string                                 | false    | Schema ID returned by create schema route or a valid URI                                                                                                                                                                                                                       |
| issuer         | [DIDDock](index.html.md#schemadiddock) | false    | Credential issuer. DID as fully qualified, e.g., `did:dock:`. If not supplied the credential will not be signed.                                                                                                                                                               |
| issuanceDate   | string(date-time\[RFC3339])            | false    | The date and time in GMT that the credential was issued specified in RFC 3339 format. The issuanceDate will be automatically set if not provided.                                                                                                                              |
| expirationDate | string(date-time\[RFC3339])            | false    | The date and time in GMT that the credential expired is specified in RFC 3339 format. The default value of the expirationDate will be empty if the user does not provide it.                                                                                                   |
| status         | object or string                       | false    | Revocation registry id or user supplied status object containg a Dock revocation registry identifier.                                                                                                                                                                          |

### VerifiablePresentation <a href="#tocs_verifiablepresentation" id="tocs_verifiablepresentation"></a>

```json
{
  "@context": [
    "string"
  ],
  "id": "http://example.com",
  "type": [
    "string"
  ],
  "verifiableCredential": {
    "@context": [
      "string"
    ],
    "id": "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb",
    "type": [
      "string"
    ],
    "credentialSubject": {},
    "issuer": "did:dock:xyz",
    "issuanceDate": "2019-08-24T14:15:22Z",
    "expirationDate": "2019-08-24T14:15:22Z",
    "credentialStatus": {},
    "proof": {
      "type": "Sr25519Signature2020",
      "proofPurpose": "assertionMethod",
      "verificationMethod": "string",
      "created": "2019-08-24T14:15:22Z",
      "proofValue": "string"
    }
  },
  "proof": {
    "type": "Sr25519Signature2020",
    "proofPurpose": "assertionMethod",
    "verificationMethod": "string",
    "created": "2019-08-24T14:15:22Z",
    "proofValue": "string"
  }
}

```

This is a schema that represents a Verifiable (signed) Presentation returned by API. The current set of properties is almost complete

#### Properties

| Name                 | Type                                                             | Required | Description                                                                                       |
| -------------------- | ---------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------- |
| @context             | [Context](index.html.md#schemacontext)                           | true     | JSON-LD context.                                                                                  |
| id                   | string(uri)                                                      | true     | Verifiable (signed) presentation id.                                                              |
| type                 | string                                                           | true     | Verifiable (signed) presentation type.                                                            |
| verifiableCredential | [VerifiableCredential](index.html.md#schemaverifiablecredential) | true     | Verifiable (signed) Credential returned by API. The current set of properties is almost complete. |
| proof                | object                                                           | true     | Proof of credential.                                                                              |

#### Child Properties of Proof <a href="#proofchildpropertiespresentation" id="proofchildpropertiespresentation"></a>

| Name               | Type                                             | Required | Description                                                                            |
| ------------------ | ------------------------------------------------ | -------- | -------------------------------------------------------------------------------------- |
| type               | [SigType](index.html.md#schemasigtype)           | true     | Type of signature.                                                                     |
| proofPurpose       | [ProofPurpose](index.html.md#schemaproofpurpose) | true     | Purpose of credential.                                                                 |
| verificationMethod | string                                           | true     | Verification method.                                                                   |
| created            | string(date-time\[RFC3339])                      | true     | The date and time in GMT that the credential was created specified in RFC 3339 format. |
| proofValue         | string                                           | true     | none                                                                                   |

### VerifiableCredential <a href="#tocs_verifiablecredential" id="tocs_verifiablecredential"></a>

```json
{
  "@context": [
    "string"
  ],
  "id": "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb",
  "type": [
    "string"
  ],
  "credentialSubject": {},
  "issuer": "did:dock:xyz",
  "issuanceDate": "2019-08-24T14:15:22Z",
  "expirationDate": "2019-08-24T14:15:22Z",
  "credentialStatus": {},
  "proof": {
    "type": "Sr25519Signature2020",
    "proofPurpose": "assertionMethod",
    "verificationMethod": "string",
    "created": "2019-08-24T14:15:22Z",
    "proofValue": "string"
  }
}

```

This is a schema that represents a verifiable (signed) Credential returned by API. The current set of properties is almost complete.

#### Properties

| Name              | Type                                   | Required | Description                                                                                                                                                                  |
| ----------------- | -------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| @context          | [Context](index.html.md#schemacontext) | false    | JSON-LD context.                                                                                                                                                             |
| id                | string(uri)                            | false    | Credential id.                                                                                                                                                               |
| type              | \[string]                              | false    | Credential type.                                                                                                                                                             |
| credentialSubject | any                                    | false    | Credential subject.                                                                                                                                                          |
| issuer            | [DIDDock](index.html.md#schemadiddock) | false    | Credential issuer or DID as fully qualified, e.g., `did:dock:`.                                                                                                              |
| issuanceDate      | string(date-time\[RFC3339])            | false    | The date and time in GMT that the credential was issued specified in RFC 3339 format. The issuanceDate will be automatically set if not provided.                            |
| expirationDate    | string(date-time\[RFC3339])            | false    | The date and time in GMT that the credential expired is specified in RFC 3339 format. The default value of the expirationDate will be empty if the user does not provide it. |
| credentialStatus  | any                                    | false    | Revocation registry id or user supplied status object.                                                                                                                       |
| proof             | object                                 | false    | Proof of credential.                                                                                                                                                         |

#### Child Properties of Proof <a href="#proofchildpropertiescredentials" id="proofchildpropertiescredentials"></a>

| Name               | Type                                             | Required | Description                                                                            |
| ------------------ | ------------------------------------------------ | -------- | -------------------------------------------------------------------------------------- |
| type               | [SigType](index.html.md#schemasigtype)           | false    | Type of signature.                                                                     |
| proofPurpose       | [ProofPurpose](index.html.md#schemaproofpurpose) | false    | Purpose of credential.                                                                 |
| verificationMethod | string                                           | false    | Verification method.                                                                   |
| created            | string(date-time\[RFC3339])                      | false    | The date and time in GMT that the credential was created specified in RFC 3339 format. |
| proofValue         | string                                           | false    | Value of credential.                                                                   |

### Anchor <a href="#tocs_anchor" id="tocs_anchor"></a>

```json
{
  "type": "single/batch",
  "proofs": [],
  "blockHash": "string",
  "root": "string",
  "created_at": "YYYY-"
}

```

An anchor, either a batched or single is the information that constitutes the credentials' proof of existence. The schema includes anchor, type (single, batch), block hash, block number and accompanying data (root, proofs) if any. It depends if the anchor was created using API or not.

### Registry <a href="#tocs_registry" id="tocs_registry"></a>

```json
{
  "addOnly": true,
  "policy": [
    "did:dock:xyz"
  ]
}

```

This is a schema that represents a Revocation registry used in Revocation or Unrevocation.

#### Properties

| Name    | Type                                      | Required | Description                                                                                                          |
| ------- | ----------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------- |
| addOnly | boolean                                   | false    | If the `addOnly` value is true, they cannot unrevoke and delete the registry. The default value for this is `false`. |
| policy  | \[[DIDDock](index.html.md#schemadiddock)] | false    | Only one policy supported as of now called `OneOf`.                                                                  |

### VerificationResponse <a href="#tocs_verificationresponse" id="tocs_verificationresponse"></a>

```json
{
  "verified": true,
  "results": [...]
}

```

This is a schema that is used to define whether a credential/presentation is verified or not

### Response <a href="#tocs_response" id="tocs_response"></a>

```json
{
  "code": 0
}

```

This is a schema that represents a default response for a request made.

### Message <a href="#tocs_message" id="tocs_message"></a>

```json
{
  "to": ["did:example:bob"],
  "ciphertext": "eyJhsad...AQ",
  "typ":"application/didcomm..."
}

```

This is a schema that represents a message send request. If the message is signed or encrypted use the `ciphertext` field. The `typ` field must be a valid DIDComm message type.

{ "@context": "http://schema.org/", "@type": "WebAPI", "description": "Dock provides a complete solution for creating and managing verifiable credentials on the blockchain. This includes a free trial and simple, monthly pricing. Get started here: https://certs.dock.io/ ", "name": "Dock API" }
