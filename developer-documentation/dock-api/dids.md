# DIDs

DID stands for Decentralized IDentifiers. DIDs are meant to be globally unique identifiers that allow their owner to prove cryptographic control over them. A DID identifies any subject (e.g., a person, organization, thing, data model, abstract entity, etc.) that the controller of the DID decides that it identifies.

DIDs in Dock are created by choosing a 32-byte unique (on Dock chain) identifier along with a public key. You can update and delete a DID as well as list all DIDs. DID is identified by a unique, random key.

For a detailed example of the DIDs workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/didFlow.js).

{% hint style="info" %}
Currently a DID can have only one key at a time as a controller, soon we will support multiple keys per DID.
{% endhint %}

## Endpoints

[POST /dids](dids.md#create-did)\
[GET /dids/{did}](dids.md#get-did)\
[GET /dids](dids.md#list-dids)\
[DELETE /dids/{did}](dids.md#list-dids-parameters-1)\
[POST /dids/{did}/export](dids.md#export-did)

## Create DID

A DID, a public key, and a controller are required to create a new DID. The controller is both the owner of the public key and a DID. The DID can be created using an auto-generated keypair, and the controller will be the same as the DID unless otherwise specified. The DID and public key have no cryptographic relation.

It is important to have a public key of one of its three supported types. Dock supports 3 types of public keys: `sr25519`, `ed25519`, and `secp256k1`.

<details>

<summary>POST /dids REQUEST PAYLOAD</summary>

```json
{
  "type": "dock",
  "keyType": "ed25519"
}
```

</details>

<details>

<summary>POST /dids REQUEST CURL</summary>

```bash
curl --location --request POST 'https://api.dock.io/dids' \
--header 'DOCK-API-TOKEN: API_KEY' \
--data-raw '{
  "type": "dock",
  "keyType": "ed25519"
}'
```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "id": "926",
  "data": {
    "did": "did:dock:5DTGPqE2qYncxoDjrEWKhcTnn6hfsN24F7YZWSjGVUxgBgHA",
    "hexDid": "0x3d7129a4d915e8f864c4bf4f4bcbdb67cde87e9bbcec06cb3baefd5b31812c03",
    "controller": "did:dock:5DTGPqE2qYncxoDjrEWKhcTnn6hfsN24F7YZWSjGVUxgBgHA"
  }
}
```

</details>

### Parameters <a href="#create-did-parameters" id="create-did-parameters"></a>

<table data-full-width="true"><thead><tr><th width="118">Name</th><th width="79">In</th><th width="98">Type</th><th width="92">Required</th><th>Description</th></tr></thead><tbody><tr><td>did</td><td>body</td><td><a href="index.html.md#schemadiddock">DIDDock</a></td><td>false</td><td>DID as fully qualified, e.g., <code>did:dock:</code>. Default value will is a randomly generated DID.</td></tr><tr><td>type</td><td>body</td><td>string</td><td>false</td><td>Specifies the DID method to for the generated DID. Supported options are <code>key</code>, <code>polygonid</code> and <code>dock</code> (default).</td></tr><tr><td>controller</td><td>body</td><td><a href="index.html.md#schemadiddock">DIDDock</a></td><td>false</td><td>DID as fully qualified, e.g., <code>did:dock:</code>. The default value of the controller is the <code>did</code> property.</td></tr><tr><td>keyType</td><td>body</td><td><a href="index.html.md#schemakeytype">KeyType</a></td><td>false</td><td>Type of public key for DID. The default value of the keyType is <code>sr25519</code>.</td></tr></tbody></table>

### Enumerated Values

<table data-full-width="true"><thead><tr><th width="131">Parameter</th><th>Value</th><th>Desctiprion</th></tr></thead><tbody><tr><td>keyType</td><td>sr25519 <strong>or</strong> ed25519 <strong>or</strong> secp256k1 <strong>or</strong> bjj</td><td>keyType signature variants.</td></tr><tr><td>type</td><td>dock <strong>or</strong> key <strong>or</strong> polyginid</td><td>which DID method to generate</td></tr></tbody></table>

{% hint style="info" %}
When creating a Polygon ID DID, be sure to set the \`keyType\` field to \`bjj\`.
{% endhint %}

### Responses <a href="#create-did-responses" id="create-did-responses"></a>

<table data-full-width="true"><thead><tr><th width="106">Status</th><th width="129">Meaning</th><th width="511">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will try to create DID. NOTE: DID does not exist on network until the job identified in the response is complete.</td><td><a href="index.html.md#schemajobstartedresult">JobStartedResult</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid params.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

## Get DID

When a DID is provided in the path, the API will attempt to resolve that DID into a [DID document](https://www.w3.org/TR/did-core/#dfn-did-documents). This document contains the public keys and more information relating to that DID, check [the identity foundation did configuration](https://identity.foundation/.well-known/resources/did-configuration/) document to learn more.

The API supports resolving many DID methods, some examples are:

* `did:dock:5CEdyZkZnALDdCAp7crTRiaCq6KViprTM6kHUQCD8X6VqGPW` - resolves through the Dock blockchain
* `did:key:z6MkjRagNiMu91DduvCvgEsqLZDVzrJzFrwahc4tXLt9DoHd` - the public key is embedded in the DID

<details>

<summary>GET /dids/{did} REQUEST CURL</summary>

```bash
curl --location --request GET 'https://api.dock.io/dids/did:dock:xyz' \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''
```

</details>

<details>

<summary>200 Response</summary>

<pre class="language-json"><code class="lang-json"><strong>{
</strong>  "@context": "https://www.w3.org/ns/did/v1",
  "id": "did:dock:5EEepQGeAeWnYgV8DWj5pH7pjHqrP2ZN2oBiE6ND2ZHA1dyN",
  "authentication": [
    "did:dock:5EEepQGeAeWnYgV8DWj5pH7pjHqrP2ZN2oBiE6ND2ZHA1dyN#keys-1"
  ],
  "assertionMethod": [
    "did:dock:5EEepQGeAeWnYgV8DWj5pH7pjHqrP2ZN2oBiE6ND2ZHA1dyN#keys-1"
  ],
  "publicKey": [
    {
      "id": "did:dock:5EEepQGeAeWnYgV8DWj5pH7pjHqrP2ZN2oBiE6ND2ZHA1dyN#keys-1",
      "type": "Sr25519VerificationKey2020",
      "controller": "did:dock:5EEepQGeAeWnYgV8DWj5pH7pjHqrP2ZN2oBiE6ND2ZHA1dyN",
      "publicKeyBase58": "ZY7vx2Jg1NSpEyrfGpDm7mRxNZyoYtbjjCjhHbhPtzM"
    }
  ]
}
</code></pre>

</details>

### Parameters <a href="#get-did-parameters" id="get-did-parameters"></a>

<table data-full-width="true"><thead><tr><th width="94">Name</th><th width="82">In</th><th width="100">Type</th><th width="108">Required</th><th>Description</th></tr></thead><tbody><tr><td>did</td><td>path</td><td><a href="index.html.md#schemadiddock">DIDDock</a></td><td>true</td><td>Represents a specific DID that uniquely identifies the key resource.</td></tr></tbody></table>

### Responses <a href="#get-did-responses" id="get-did-responses"></a>

<table data-full-width="true"><thead><tr><th width="100">Status</th><th width="190">Meaning</th><th width="457">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return the DID doc.</td><td></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The requested DID was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

## List DIDs

Return a list of all DIDs that your user account controls as fully resolved DID documents.

### Parameters <a href="#list-dids-parameters" id="list-dids-parameters"></a>

<table><thead><tr><th width="92">Name</th><th width="81">In</th><th width="88">Type</th><th width="107">Required</th><th>Description</th></tr></thead><tbody><tr><td>offset</td><td>query</td><td>integer</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

### Responses <a href="#list-dids-responses" id="list-dids-responses"></a>

<table><thead><tr><th width="99">Status</th><th width="134">Meaning</th><th width="350">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>All of a user's DIDs fully resolved into DID documents.</td><td><a href="index.html.md#schemadiddoc">DIDDock</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

> GET /dids REQUEST

```shell
curl --location --request GET 'https://api.dock.io/dids' \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

> 200 Response

```json
[
  {
    "@context": "https://www.w3.org/ns/did/v1",
    "id": "did:dock:5DTGPqE2qYncxoDjrEWKhcTnn6hfsN24F7YZWSjGVUxgBgHA",
    "authentication": [
      "did:dock:5DTGPqE2qYncxoDjrEWKhcTnn6hfsN24F7YZWSjGVUxgBgHA#keys-1"
    ],
    "assertionMethod": [
      "did:dock:5DTGPqE2qYncxoDjrEWKhcTnn6hfsN24F7YZWSjGVUxgBgHA#keys-1"
    ],
    "publicKey": [
      {
        "id": "did:dock:5DTGPqE2qYncxoDjrEWKhcTnn6hfsN24F7YZWSjGVUxgBgHA#keys-1",
        "type": "Sr25519VerificationKey2020",
        "controller": "did:dock:5DTGPqE2qYncxoDjrEWKhcTnn6hfsN24F7YZWSjGVUxgBgHA",
        "publicKeyBase58": "4vm85LvBvhro1N9u4dfKWEyTayXojrTJbJCmzSJixK6L"
      }
    ]
  }
]
```

## Delete DID <a href="#list-dids-parameters" id="list-dids-parameters"></a>

Deletes a DID and its metadata from the blockchain and our platform. This will also delete the associated keypair from the key management system meaning that you cannot sign messages or credentials with it after this operation. The DID will no longer be able to be resolved. This operation is not reversible.

### Parameters <a href="#delete-did-parameters" id="delete-did-parameters"></a>

<table><thead><tr><th width="100">Name</th><th width="73">In</th><th width="85">Type</th><th width="97">Required</th><th>Description</th></tr></thead><tbody><tr><td>did</td><td>path</td><td><a href="index.html.md#schemadiddock">DID</a></td><td>true</td><td>Represents a specific DID that uniquely identifies the key resource.</td></tr></tbody></table>

### Responses <a href="#delete-did-responses" id="delete-did-responses"></a>

<table><thead><tr><th width="99">Status</th><th width="141">Meaning</th><th width="345">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will remove the DID.</td><td><a href="index.html.md#schemajobid">JobId</a></td></tr><tr><td>401</td><td><a href="https://tools.ietf.org/html/rfc7235#section-3.1">Unauthorized</a></td><td>The request was unsuccessful, because you don't own the DID.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The DID does not exist.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>405</td><td><a href="https://datatracker.ietf.org/doc/html/rfc7231#section-6.5.5">Method not Allowed</a></td><td>The {did} value is blank/empty. Please ensure that the {did} value does exist.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

> DELETE /dids/{did} REQUEST

```shell
curl --location --request DELETE https://api.dock.io/dids/{did} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
    }'

```

> 200 Response

```json
{
  "id": "928",
  "data": {
    "deleted": true
  }
}
```

## Export DID

Exports the DID document and keys as an encrypted Universal Wallet JSON-LD document

### Parameters <a href="#export-did-parameters" id="export-did-parameters"></a>

<table><thead><tr><th width="125">Name</th><th width="84">In</th><th width="92">Type</th><th width="115">Required</th><th>Description</th></tr></thead><tbody><tr><td>did</td><td>path</td><td><a href="index.html.md#schemadiddock">DID</a></td><td>true</td><td>Represents a specific DID that uniquely identifies the key resource.</td></tr><tr><td>password</td><td>body</td><td>string</td><td>true</td><td>A password to encrypt the JSON-LD payload with</td></tr></tbody></table>

### Responses <a href="#export-did-responses" id="export-did-responses"></a>

<table><thead><tr><th width="101">Status</th><th width="158">Meaning</th><th width="333">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and the DID has been exported.</td><td></td></tr><tr><td>401</td><td><a href="https://tools.ietf.org/html/rfc7235#section-3.1">Unauthorized</a></td><td>The request was unsuccessful, because you don't own the DID.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The DID does not exist.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

> POST /dids/{did}/export REQUEST

```shell
curl --location --request POST https://api.dock.io/dids/{did}/export \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
      "password": "aStr0ngP@ssw0rd"
    }'

```

> 200 Response

```json
{
}
```
