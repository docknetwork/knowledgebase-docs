# Schemas

Data Schemas are useful when enforcing a specific structure on a collection of data like a Verifiable Credential. Other than that, Data Verification schema and Data Encoding Schemas are used to verify and map the structure and contents of a Verifiable Credential.

These are the schemas used in all API operations mentioned before, such as Error, Credential, Jobs, Anchor, Registry, and so on.

For a detailed example of the schema workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/schemaFlow.js).

> Object Schemas

## Error <a href="#tocs_error" id="tocs_error"></a>

This is a schema for an API Error.

#### Properties

<table><thead><tr><th width="138">Name</th><th width="131">Type</th><th width="176">Required</th><th>Description</th></tr></thead><tbody><tr><td>status</td><td>integer</td><td>false</td><td>Status of the error.</td></tr><tr><td>type</td><td>string</td><td>false</td><td>Type of the error.</td></tr><tr><td>message</td><td>string</td><td>false</td><td>Message of the error.</td></tr></tbody></table>

```json
{
  "status": 0,
  "type": "string",
  "message": "string"
}

```

## Hex32 <a href="#tocs_hex32" id="tocs_hex32"></a>

32 byte hex string. Ignoring higher base (base64) for simplicity.

### Properties

<table><thead><tr><th width="100">Name</th><th width="99">Type</th><th width="114">Required</th><th>Description</th></tr></thead><tbody><tr><td>Hex32</td><td>string</td><td>false</td><td>32 byte hex string. Ignoring higher base (base64) for simplicity.</td></tr></tbody></table>

```json
"string"

```

## JobStartedResult <a href="#tocs_jobstartedresult" id="tocs_jobstartedresult"></a>

Object containing unique id of the background task and associated data. This id can be used to query the job status.

### Properties

<table><thead><tr><th width="110">Name</th><th width="130">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td><a href="index.html.md#schemajobid">JobId</a></td><td>Unique id of the background task. This id can be used to query the job status.</td></tr><tr><td>data</td><td>object</td><td>Data of the object.</td></tr></tbody></table>

```json
{
  "id": "string",
  "data": {
    "did": "did:dock:xyz",
    "hexDid": "0x00",
  }
}

```

## JobId <a href="#tocs_jobid" id="tocs_jobid"></a>

Unique id of the background task. This id can be used to query the job status

```json
"string"

```

## JobStatus <a href="#tocs_jobstatus" id="tocs_jobstatus"></a>

This is a schema used in Job operation to get a status of the job.

#### Enumerated Values

<table><thead><tr><th width="158">Property</th><th width="323">Value</th><th>Description</th></tr></thead><tbody><tr><td>JobStatus</td><td>todo <strong>or</strong> finalized <strong>or</strong> in_progress <strong>or</strong> error.</td><td>Job Status variants.</td></tr></tbody></table>

```json
"in_progress"

```

## JobDesc <a href="#tocs_jobdesc" id="tocs_jobdesc"></a>

This is a schema used in Job operation to get description of the job including the result if it is available.

### Properties

<table><thead><tr><th width="121">Name</th><th width="142">Type</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td><a href="index.html.md#schemajobid">JobId</a></td><td>Unique id of the background task. This id can be used to query the job status.</td></tr><tr><td>status</td><td><a href="index.html.md#schemajobstatus">JobStatus</a></td><td>Status of the job.</td></tr><tr><td>result</td><td>object</td><td>false</td></tr></tbody></table>

```json
{
  "id": "string",
  "result": {},
  "status": "todo",

}

```

## DIDDock <a href="#tocs_diddock" id="tocs_diddock"></a>

DID as fully qualified, e.g., `did:dock:`.

### Properties

<table><thead><tr><th width="93">Name</th><th width="99">Type</th><th width="119">Required</th><th>Description</th></tr></thead><tbody><tr><td>DID</td><td>string</td><td>false</td><td>DID as fully qualified, e.g., <code>did:dock:</code>. You cannot specify your own DID, the DID value will be randomly generated.</td></tr></tbody></table>

```json
"did:dock:xyz"

```

## KeyType <a href="#tocs_keytype" id="tocs_keytype"></a>

This is a schema type of public key for DID.

### Enumerated Values

<table><thead><tr><th width="142">Property</th><th width="318">Value</th><th>Description</th></tr></thead><tbody><tr><td>KeyType</td><td>sr25519 <strong>or</strong> ed25519 <strong>or</strong> secp256k1</td><td>keyType DID variants.</td></tr></tbody></table>

```json
"sr25519"

```

## SigType <a href="#tocs_sigtype" id="tocs_sigtype"></a>

This is a schema used in Presentation operation that represents a type of signature.

### Enumerated Values

<table><thead><tr><th width="135">Property</th><th width="364">Value</th><th>Description</th></tr></thead><tbody><tr><td>SigType</td><td>Sr25519Signature2020 <strong>or</strong> Ed25519Signature2018 <strong>or</strong> EcdsaSecp256k1Signature2019</td><td>SigType signature variants.</td></tr></tbody></table>

```json
"Sr25519Signature2020"

```

## ProofPurpose <a href="#tocs_proofpurpose" id="tocs_proofpurpose"></a>

This is a schema that represents a purpose of credential.

### Enumerated Values

<table><thead><tr><th width="170">Property</th><th width="309">Value</th><th>Description</th></tr></thead><tbody><tr><td>ProofPurpose</td><td>assertionMethod <strong>or</strong> authentication</td><td>Purpose of credential.</td></tr></tbody></table>

```json
"assertionMethod"

```

## Context <a href="#tocs_context" id="tocs_context"></a>

This is a schema that represents a JSON-LD context used in DID and Presentation.

```json
[
  "string"
]

```

## DIDDoc <a href="#tocs_diddoc" id="tocs_diddoc"></a>

This is a schema that represents a DID document. The current set of properties is incomplete

### Properties

<table><thead><tr><th width="161">Name</th><th width="120">Type</th><th width="117">Required</th><th>Description</th></tr></thead><tbody><tr><td>@context</td><td><a href="index.html.md#schemacontext">Context</a></td><td>false</td><td>JSON-LD context.</td></tr><tr><td>id</td><td><a href="index.html.md#schemadiddock">DIDDock</a></td><td>false</td><td>DID as fully qualified, e.g., <code>did:dock:</code>.</td></tr><tr><td>authentication</td><td>array</td><td>false</td><td>DID authentication.</td></tr></tbody></table>

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

## Credential <a href="#tocs_credential" id="tocs_credential"></a>

This is a schema that represents a credential format expected by API caller when issuing a credential.

### Properties

<table><thead><tr><th width="121">Name</th><th width="153">Type</th><th width="102">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>string(uri)</td><td>false</td><td>Credential ID. The default value is a creds.dock.io uri with random ID.</td></tr><tr><td>context</td><td>[string or object]</td><td>false</td><td>Credential context array of string URIs and/or embedded JSON-LD context objects. If no context parameter is supplied, we will auto generate contexts for you. If you do supply this parameter, you must ensure that all JSON-LD terms are defined. This is for advanced users.</td></tr><tr><td>type</td><td>[string]</td><td>false</td><td>Credential type. The default value is ['VerifiableCredential']</td></tr><tr><td>subject</td><td>object or [object]</td><td>true</td><td>Credential subject or subjects array.</td></tr><tr><td>schema</td><td>string</td><td>false</td><td>Schema ID returned by create schema route or a valid URI</td></tr><tr><td>issuer</td><td><a href="index.html.md#schemadiddock">DIDDock</a></td><td>false</td><td>Credential issuer. DID as fully qualified, e.g., <code>did:dock:</code>. If not supplied the credential will not be signed.</td></tr><tr><td>issuanceDate</td><td>string(date-time[RFC3339])</td><td>false</td><td>The date and time in GMT that the credential was issued specified in RFC 3339 format. The issuanceDate will be automatically set if not provided.</td></tr><tr><td>expirationDate</td><td>string(date-time[RFC3339])</td><td>false</td><td>The date and time in GMT that the credential expired is specified in RFC 3339 format. The default value of the expirationDate will be empty if the user does not provide it.</td></tr><tr><td>status</td><td>object or string</td><td>false</td><td>Revocation registry id or user supplied status object containg a Dock revocation registry identifier.</td></tr></tbody></table>

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

## VerifiablePresentation <a href="#tocs_verifiablepresentation" id="tocs_verifiablepresentation"></a>

This is a schema that represents a Verifiable (signed) Presentation returned by API. The current set of properties is almost complete

### Properties

<table><thead><tr><th width="144">Name</th><th width="163">Type</th><th width="121">Required</th><th>Description</th></tr></thead><tbody><tr><td>@context</td><td><a href="index.html.md#schemacontext">Context</a></td><td>true</td><td>JSON-LD context.</td></tr><tr><td>id</td><td>string(uri)</td><td>true</td><td>Verifiable (signed) presentation id.</td></tr><tr><td>type</td><td>string</td><td>true</td><td>Verifiable (signed) presentation type.</td></tr><tr><td>verifiableCredential</td><td><a href="index.html.md#schemaverifiablecredential">VerifiableCredential</a></td><td>true</td><td>Verifiable (signed) Credential returned by API. The current set of properties is almost complete.</td></tr><tr><td>proof</td><td>object</td><td>true</td><td>Proof of credential.</td></tr></tbody></table>

### Child Properties of Proof <a href="#proofchildpropertiespresentation" id="proofchildpropertiespresentation"></a>

<table><thead><tr><th width="162">Name</th><th width="155">Type</th><th width="112">Required</th><th>Description</th></tr></thead><tbody><tr><td>type</td><td><a href="index.html.md#schemasigtype">SigType</a></td><td>true</td><td>Type of signature.</td></tr><tr><td>proofPurpose</td><td><a href="index.html.md#schemaproofpurpose">ProofPurpose</a></td><td>true</td><td>Purpose of credential.</td></tr><tr><td>verificationMethod</td><td>string</td><td>true</td><td>Verification method.</td></tr><tr><td>created</td><td>string(date-time[RFC3339])</td><td>true</td><td>The date and time in GMT that the credential was created specified in RFC 3339 format.</td></tr><tr><td>proofValue</td><td>string</td><td>true</td><td>none</td></tr></tbody></table>

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

## VerifiableCredential

This is a schema that represents a verifiable (signed) Credential returned by API. The current set of properties is almost complete.

### Properties

<table><thead><tr><th width="155">Name</th><th width="127">Type</th><th width="107">Required</th><th>Description</th></tr></thead><tbody><tr><td>@context</td><td><a href="index.html.md#schemacontext">Context</a></td><td>false</td><td>JSON-LD context.</td></tr><tr><td>id</td><td>string(uri)</td><td>false</td><td>Credential id.</td></tr><tr><td>type</td><td>[string]</td><td>false</td><td>Credential type.</td></tr><tr><td>credentialSubject</td><td>any</td><td>false</td><td>Credential subject.</td></tr><tr><td>issuer</td><td><a href="index.html.md#schemadiddock">DIDDock</a></td><td>false</td><td>Credential issuer or DID as fully qualified, e.g., <code>did:dock:</code>.</td></tr><tr><td>issuanceDate</td><td>string(date-time[RFC3339])</td><td>false</td><td>The date and time in GMT that the credential was issued specified in RFC 3339 format. The issuanceDate will be automatically set if not provided.</td></tr><tr><td>expirationDate</td><td>string(date-time[RFC3339])</td><td>false</td><td>The date and time in GMT that the credential expired is specified in RFC 3339 format. The default value of the expirationDate will be empty if the user does not provide it.</td></tr><tr><td>credentialStatus</td><td>any</td><td>false</td><td>Revocation registry id or user supplied status object.</td></tr><tr><td>proof</td><td>object</td><td>false</td><td>Proof of credential.</td></tr></tbody></table>

### Child Properties of Proof <a href="#proofchildpropertiescredentials" id="proofchildpropertiescredentials"></a>

<table><thead><tr><th width="164">Name</th><th width="151">Type</th><th width="129">Required</th><th>Description</th></tr></thead><tbody><tr><td>type</td><td><a href="index.html.md#schemasigtype">SigType</a></td><td>false</td><td>Type of signature.</td></tr><tr><td>proofPurpose</td><td><a href="index.html.md#schemaproofpurpose">ProofPurpose</a></td><td>false</td><td>Purpose of credential.</td></tr><tr><td>verificationMethod</td><td>string</td><td>false</td><td>Verification method.</td></tr><tr><td>created</td><td>string(date-time[RFC3339])</td><td>false</td><td>The date and time in GMT that the credential was created specified in RFC 3339 format.</td></tr><tr><td>proofValue</td><td>string</td><td>false</td><td>Value of credential.</td></tr></tbody></table>

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

## Anchor

An anchor, either a batched or single is the information that constitutes the credentials' proof of existence. The schema includes anchor, type (single, batch), block hash, block number and accompanying data (root, proofs) if any. It depends if the anchor was created using API or not.

```json
{
  "type": "single/batch",
  "proofs": [],
  "blockHash": "string",
  "root": "string",
  "created_at": "YYYY-"
}

```

## Registry <a href="#tocs_registry" id="tocs_registry"></a>

This is a schema that represents a Revocation registry used in Revocation or Unrevocation.

### Properties

<table><thead><tr><th width="128">Name</th><th width="115">Type</th><th width="112">Required</th><th>Description</th></tr></thead><tbody><tr><td>addOnly</td><td>boolean</td><td>false</td><td>If the <code>addOnly</code> value is true, they cannot unrevoke and delete the registry. The default value for this is <code>false</code>.</td></tr><tr><td>policy</td><td>[<a href="index.html.md#schemadiddock">DIDDock</a>]</td><td>false</td><td>Only one policy supported as of now called <code>OneOf</code>.</td></tr></tbody></table>

```json
{
  "addOnly": true,
  "policy": [
    "did:dock:xyz"
  ]
}

```

## VerificationResponse <a href="#tocs_verificationresponse" id="tocs_verificationresponse"></a>

This is a schema that is used to define whether a credential/presentation is verified or not

```json
{
  "verified": true,
  "results": [...]
}

```

## Response <a href="#tocs_response" id="tocs_response"></a>

This is a schema that represents a default response for a request made.

```json
{
  "code": 0
}

```

## Message <a href="#tocs_message" id="tocs_message"></a>

This is a schema that represents a message send request. If the message is signed or encrypted use the `ciphertext` field. The `typ` field must be a valid DIDComm message type.

```json
{
  "to": ["did:example:bob"],
  "ciphertext": "eyJhsad...AQ",
  "typ":"application/didcomm..."
}

```

