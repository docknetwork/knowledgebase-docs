# Credentials

You can create and sign Verifiable Credentials on Dock Certs and its API. By default, Dock does not store the credential - only its metadata. You can choose to persist a credential, in which case we will encrypt and store the credential for later retrieval using a password. Verifiable Credentials are cryptographically secure and tamper-proof. Once issued, they cannot be edited.

The Dock API supports issuing two types of credentials. The native Dock Verifiable Credentials and Polygon ID Verifiable Credentials.

{% hint style="info" %}
For Polygon ID credentials:

* In order to issue Polygon ID credentials, the issuer **must** be a `did:polygonid` issuer.
* Polygon ID credentials **do not** support designs at this point so `template` field should be omitted.
{% endhint %}

## Endpoints

[POST /credentials](credentials.md#issue-credentials)\
[GET /credentials/{id}](credentials.md#get-credential)\
[DELETE /credentials/{id}](credentials.md#delete-credential)

## Issue Credential <a href="#issue-credentials" id="issue-credentials"></a>

Creates and issues a JSON-LD Verifiable Credential that conforms to the [W3C VCDM specification](https://www.w3.org/TR/vc-data-model/). The `type` values and subject properties must be represented by a schema URI in the `context` property. If you do not specify a `context` property, the API will automatically generate an embedded JSON-LD context based on the properties within your credential. You can read more about JSON-LD and contexts [here](https://json-ld.org/spec/latest/json-ld/#the-context).

{% hint style="info" %}
The `https://www.w3.org/2018/credentials/v1` context URI is always required and will be supplied by default at all times as mandated by the spec. If you pass a custom context, you must ensure that you define all the required JSON-LD terms. Please also note that the request format here is not the same as an issued verifiable credential. You can issue to multiple subjects per credential by passing an array of objects.
{% endhint %}

To sign a credential, an `issuer` must be supplied as either a fully qualified DID string or an object with at least an `id` property which is a fully qualified DID. (e.g: `did:dock:xyz`)

{% hint style="warning" %}
The `issuer` property **must** be a DID that you control with Dock Certs.
{% endhint %}

By default, Dock does not store the credential contents at all - only minimal credential metadata. You can choose to set the `persist` value to `true` and provide a `password` string which will store the credential contents encrypted on our platform. The following metadata is stored on each issuance:

* Credential ID property
* Credential size in bytes
* Issuer DID
* Issuance date

For a detailed example of the credential workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/credentialsFlow.js).

### Zero Knowledge Proofs (ZKP) <a href="#zero-knowledge-proofs" id="zero-knowledge-proofs"></a>

Dock credentials support [anonymous credentials](https://blog.dock.io/anonymous-credentials/) using Zero Knowledge Proofs and [Selective Disclosure](https://www.dock.io/post/selective-disclosure) by using the BBS+ signing algorithm when issuing the credential. To enable this functionality, simply set the `algorithm` field in the request to `dockbbs+`.

### Credential Distribution <a href="#credential-distribution" id="credential-distribution"></a>

Dock's API has built in credential distribution on issuance, allowing you to send credentials directly to a holder's email and/or Dock-compatible wallet. You can achieve this by supplying the `recipientEmail` field and `distribute: true` in your request. For DID distribution, simply set the `credentialSubject.id` property to the holder's DID.

### Revocation <a href="#credential-issuance-revocation" id="credential-issuance-revocation"></a>

In order to support revocation the credential must be linked to a revocation [registry](index.html.md#registry\_create) at the time of issuance. To link the revocation registry to the credential set the `status` field in the [Credential](index.html.md#schemacredential) body to the `registry.id` value.

{% hint style="warning" %}
This operation counts towards your monthly transaction/credential issuance limit for each successful call
{% endhint %}

### Parameters <a href="#issue-a-credential-parameters" id="issue-a-credential-parameters"></a>

<table data-full-width="false"><thead><tr><th width="122">Name</th><th width="84">In</th><th width="100">Type</th><th width="85">Required</th><th>Description</th></tr></thead><tbody><tr><td>anchor</td><td>body</td><td>boolean</td><td>false</td><td>Whether to anchor the credential on the blockchain as soon as it is issued. Defaults to false.</td></tr><tr><td>persist</td><td>body</td><td>boolean</td><td>false</td><td>Whether to store an encrypted version of this credential with us. Defaults to false, if true you must supply password.</td></tr><tr><td>password</td><td>body</td><td>string</td><td>false</td><td>Password used to encrypt the credential if you choose to store it. The same password must be used to retrieve the credential contents. Dock does not store this password.</td></tr><tr><td>template</td><td>body</td><td>UUID string</td><td>false</td><td>The ID of the intended template/design, optional</td></tr><tr><td>format</td><td>body</td><td>string</td><td>false</td><td>Specifies the output format of the credential, either <code>jsonld</code> or <code>jwt</code>. Defaults to <code>jsonld</code>.</td></tr><tr><td>algorithm</td><td>body</td><td>string</td><td>false</td><td>Specifies which signing algorithm to use to sign the issued credential. Defaults to <code>ed25519</code>.</td></tr><tr><td>distribute</td><td>body</td><td>boolean</td><td>false</td><td>Whether to use credential distribution to DID/email, optional</td></tr><tr><td>recipientEmail</td><td>body</td><td>string</td><td>false</td><td>The holder's email for email distribution</td></tr><tr><td>credential</td><td>body</td><td><a href="index.html.md#schemacredential">Credential</a></td><td>true</td><td>Credential object as described in the <a href="index.html.md#schemacredential">schema</a>.</td></tr></tbody></table>

### Enumerated Values

<table data-full-width="false"><thead><tr><th width="161">Parameter</th><th width="232">Value</th><th>Description</th></tr></thead><tbody><tr><td>algorithm</td><td>ed25519 <strong>or</strong> secp256k1 <strong>or</strong> sr25519 <strong>or</strong> dockbbs+</td><td>The algorithm used to sign the credential.</td></tr></tbody></table>

### Responses <a href="#issue-a-credential-responses" id="issue-a-credential-responses"></a>

<table data-full-width="false"><thead><tr><th width="90">Status</th><th width="134">Meaning</th><th width="310">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and returns the created Verifiable Credential.</td><td><a href="index.html.md#schemaverifiablecredential">VerifiableCredential</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid/insufficient credential params.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>401</td><td><a href="https://tools.ietf.org/html/rfc7235#section-3.1">Unauthorized</a></td><td>The request was unsuccessful, either because the authorization token was missing/invalid or you don't own the DID.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /credentials REQUEST PAYLOAD</summary>

```json

{
  "anchor": true,
  "persist": false,
  "distribute": true,
  "recipientEmail": "myemail@dock.io",
  "schema": "https://schema.dock.io/TestSchema-V1-1695817897561.json",
  "template": "b8dd5768-0777-42c2-ae73-859e1079369b",
  "credential": {
    "type": ["UniversityDegreeCredential"],
    "subject": {
      "id": "did:dock:5CDsD8HZa6TeSfgmMcxAkbSXYWeob4jFQmtU6sxr4XWTZzUA",
      "degree": {
        "type": "BachelorDegree",
        "name": "Bachelor of Science and Arts"
      }
    },
    "issuer": "did:dock:xyz",
    "issuanceDate": "2020-08-24T14:15:22Z"
  }
}
```

</details>

<details>

<summary>POST /credentials REQUEST CURL</summary>

```bash
curl --location --request POST https://api.dock.io/credentials/ \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
  "persist": false,
  "anchor": true,
  "template": "b8dd5768-0777-42c2-ae73-859e1079369b",
  "credential": {
    "type": ["UniversityDegreeCredential"],
    "subject": {
      "id": "did:dock:5CDsD8HZa6TeSfgmMcxAkbSXYWeob4jFQmtU6sxr4XWTZzUA",
      "degree": {
        "type": "BachelorDegree",
        "name": "Bachelor of Science and Arts"
      }
    },
    "issuer": "did:dock:xyz",
    "issuanceDate": "2020-08-24T14:15:22Z"
  }
}'


```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb",
  "type": [
    "VerifiableCredential",
    "UniversityDegreeCredential"
  ],
  "credentialSubject": {
    "id": "did:dock:5CDsD8HZa6TeSfgmMcxAkbSXYWeob4jFQmtU6sxr4XWTZzUA",
    "degree": {
      "type": "BachelorDegree",
      "name": "Bachelor of Science and Arts"
    }
  },
  "issuanceDate": "2020-08-24T14:15:22Z",
  "proof": {
    "type": "EcdsaSecp256k1Signature2019",
    "created": "2021-11-22T22:51:08Z",
    "verificationMethod": "did:dock:5FfmGmkY1BqEqRQhRLCLDLHPBFvhSbEBK3DJhEk9mbkpfAXT#keys-1",
    "proofPurpose": "assertionMethod",
    "proofValue": "zAN1rKrjNqYSr6mjbNEohqhCAnEoLWFgJutBmYMkXZYG8RatBuCv7ymFHEchufa1vjiM4JkHCkasswjukYVVJT3rBmTaRaUDHT"
  },
  "issuer": "did:dock:xyz"
}
```

</details>

## Request Claims <a href="#request-claims" id="request-claims"></a>

Creates a request to gather certain claims and then issues the holder a credential after submission. The claims are user provided and type is based on the schema provided. This can be useful to catch a subject's DID without knowing it beforehand, name or other field. It should only be used when you do not already know this data or cannot find it by other means. There is a risk that a user may enter false data - so use it sparingly and not for fields that are important.

Typically, once the request has been created, you would show the holder the QR URL as an image or deep link for them to scan with a wallet and enter claims.

{% hint style="warning" %}
This operation counts towards your monthly transaction/credential issuance limit for each successful call.
{% endhint %}

### Parameters <a href="#request-claims-parameters" id="request-claims-parameters"></a>

<table data-full-width="false"><thead><tr><th width="134">Name</th><th width="76">In</th><th width="144">Type</th><th width="108">Required</th><th>Description</th></tr></thead><tbody><tr><td>schema</td><td>body</td><td>string</td><td>false</td><td>Schema URL for the issued credential</td></tr><tr><td>claims</td><td>body</td><td>array</td><td>false</td><td>The list of claims for the subject</td></tr><tr><td>credentialOptions</td><td>body</td><td><a href="index.html.md#issue-a-credential-parameters">CredentialIssueParameters</a></td><td>true</td><td>Credential issue parameters.</td></tr></tbody></table>

### Responses <a href="#request-claims-responses" id="request-claims-responses"></a>

<table data-full-width="false"><thead><tr><th width="107">Status</th><th width="192">Meaning</th><th width="399">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and returns the claims request properties.</td><td><a href="index.html.md#schemaoidcissuer">OIDCIssuer</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid/insufficient credential params.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>401</td><td><a href="https://tools.ietf.org/html/rfc7235#section-3.1">Unauthorized</a></td><td>The request was unsuccessful, either because the authorization token was missing/invalid or you don't own the DID.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /credentials/request-claims REQUEST PAYLOAD</summary>

```json

{
  "schema": "https://docknetwork.github.io/vc-schemas/basic-credential.json",
  "claims": [
    "id"
  ],
  "credentialOptions": {
    "anchor": false,
    "persist": false,
    "credential": {
      "schema": "https://docknetwork.github.io/vc-schemas/basic-credential.json",
      "name": "Basic Credential",
      "type": [
        "VerifiableCredential",
        "BasicCredential"
      ],
      "issuer": "did:dock:5GZn9zQTggPWijzgnoV8sZ5a74rFqC8qrz2ncp7GggeGCtKd",
      "issuanceDate": "2023-12-20T00:33:15.803Z",
      "subject": {
        "name": "Predefined Claim"
      }
    },
    "distribute": false
  }
}
```

</details>

<details>

<summary>POST /credentials/request-claims REQUEST CURL</summary>

```bash
curl --location --request POST https://api.dock.io/credentials/ \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
  "schema": "https://docknetwork.github.io/vc-schemas/basic-credential.json",
  "claims": [
    "id"
  ],
  "credentialOptions": {
    "anchor": false,
    "persist": false,
    "credential": {
      "schema": "https://docknetwork.github.io/vc-schemas/basic-credential.json",
      "name": "Basic Credential",
      "type": [
        "VerifiableCredential",
        "BasicCredential"
      ],
      "issuer": "did:dock:5GZn9zQTggPWijzgnoV8sZ5a74rFqC8qrz2ncp7GggeGCtKd",
      "issuanceDate": "2023-12-20T00:33:15.803Z",
      "subject": {
        "name": "Predefined Claim"
      }
    },
    "distribute": false
  }
}'
```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "id": "f1831768-853f-4ac1-ae99-adf61a92724f",
  "qrUrl": "openid://discovery?issuer=https://api.dock.io/openid/connect/issuers/f1831768-853f-4ac1-ae99-adf61a92724f",
  "created": "2023-12-20T00:33:35.720Z",
  "updated": "2023-12-20T00:33:35.720Z",
  "singleUse": true,
  "claimMap": {
    "id": "id"
  },
  "issuer": "did:dock:5GZn9zQTggPWijzgnoV8sZ5a74rFqC8qrz2ncp7GggeGCtKd",
  "protocol": "openid",
  "credentialOptions": {
    "anchor": false,
    "persist": false,
    "credential": {
      "name": "Basic Credential",
      "type": [
        "VerifiableCredential",
        "BasicCredential"
      ],
      "issuer": "did:dock:5GZn9zQTggPWijzgnoV8sZ5a74rFqC8qrz2ncp7GggeGCtKd",
      "schema": "https://docknetwork.github.io/vc-schemas/basic-credential.json",
      "subject": {
        "name": "Predefined Claim"
      },
      "issuanceDate": "2023-12-20T00:33:15.803Z"
    },
    "distribute": false
  }
}
```

</details>

## Get Credential

When a credential has been persisted on our systems, you can fetch the credential data by supplying a credential ID and the password used at issuance to encrypt the credential.

### Parameters <a href="#get-credential-parameters" id="get-credential-parameters"></a>

<table data-full-width="false"><thead><tr><th width="130">Name</th><th width="99">In</th><th width="90">Type</th><th width="107">Required</th><th>Description</th></tr></thead><tbody><tr><td>did</td><td>path</td><td>string</td><td>true</td><td>The ID of the credential (as a full URI).</td></tr><tr><td>password</td><td>query</td><td>string</td><td>true</td><td>The password given at issuance to encrypt the credential in storage</td></tr></tbody></table>

### Responses <a href="#get-credential-responses" id="get-credential-responses"></a>

<table data-full-width="false"><thead><tr><th width="118">Status</th><th width="177">Meaning</th><th width="294">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return the credential metadata and its JSON contents.</td><td></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The requested credential was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /credentials/{id} REQUEST CURL</summary>

```bash
curl --location --request GET 'https://api.dock.io/credentials/credential_id?password=test' \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "id": "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb",
  "byteSize": 1074,
  "issuerKey": "did:dock:5CU97DhQ3mnbxPAiYw3GoRqFcnvCLGuHj3MS8evD8sARmg3e#KWAtkADdAy1rCiysr4cPZre4Lj7GFWGqyN5mP5X8xuzAnGzAb                     ",
  "createdAt": "2021-12-21T01:36:23.062Z",
  "credential": { ... }
}
```

</details>

## Delete Credential

A credential can have its metadata deleted, and if persisted the contents will also be deleted. Deleting a credential will remove any reference to it and its contents from our systems. This action cannot be undone. This action will not revoke or invalidate the credential in any way.

### Parameters <a href="#delete-credential-parameters" id="delete-credential-parameters"></a>

<table data-full-width="false"><thead><tr><th width="99">Name</th><th width="76">In</th><th width="102">Type</th><th width="119">Required</th><th>Description</th></tr></thead><tbody><tr><td>did</td><td>path</td><td>string</td><td>true</td><td>The ID of the credential (as a full URL-encoded URI).</td></tr></tbody></table>

### Responses <a href="#delete-credential-responses" id="delete-credential-responses"></a>

<table data-full-width="false"><thead><tr><th width="108">Status</th><th width="171">Meaning</th><th width="304">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and credential will be deleted.</td><td></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The request was unsuccessful, because the credential was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>DELETE /credentials/{id} REQUEST CURL</summary>

```bash
curl --location --request DELETE https://api.dock.io/credentials/{id} \
  --header 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>200 Response</summary>

```
{ }
```

</details>

## Get Credentials Metadata

When you issue a credential with us, persistent or not, we will store certain metadata about the credential to make it easier for you to reference. You can pull a list of credential metadata using this route. To return the content of a persisted credential, you should use the `GET /credentials/{id}` route

### Parameters <a href="#get-credential-parameters" id="get-credential-parameters"></a>

<table data-full-width="false"><thead><tr><th width="116">Name</th><th width="96">In</th><th width="117">Type</th><th width="119">Required</th><th>Description</th></tr></thead><tbody><tr><td>offset</td><td>query</td><td>integer</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

### Responses <a href="#get-credential-responses" id="get-credential-responses"></a>

<table data-full-width="false"><thead><tr><th width="105">Status</th><th width="107">Meaning</th><th width="380">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return the credential metadata and its JSON contents.</td><td></td></tr></tbody></table>

<details>

<summary>GET /credentials REQUEST</summary>

```bash
curl --location --request GET 'https://api.dock.io/credentials' \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''
```

</details>

<details>

<summary>200 Response</summary>

```json
[
  {
    "id": "https://creds.dock.io/6d601b80d56f4bb2f35b4fbe2406cc186a25b615a66fc405283ad5967f28c143",
    "issuerKey": "did:dock:xyz#xyz",
    "type": "BasicCredential",
    "revoked": false,
    "revocationRegistry": "rev-reg:dock:0x357c104d14e81d66ef43debee91eb62aac9af27c34a1e1a2194ee443989c4d44",
    "createdAt": "2022-04-18T18:28:09.914Z",
    "expirationDate": null,
    "byteSize": 917,
    "persist": false
  }
]
```

</details>
