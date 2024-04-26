# Anchors

Anchoring allows users to store a digest of one or more credentials (or any document) on our blockchain, tying them to immutable timestamps and proving that they were generated at a certain moment in time. By enabling this feature, users will have more options for auditing credentials given and timestamping any documents.

The Dock Blockchain includes a module explicitly intended for proof of existence. You post the hash of a document on-chain at a specific block. Later you can use that hash to prove the document existed at or before that block.

The API allows you to create, get, and retrieve anchors as well as a list of all anchors created by the user.

For a detailed example of the anchor workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/anchorsFlow.js).

## Endpoints

[POST /anchors](anchors.md#create-anchor)\
[GET /anchors](anchors.md#list-anchors)\
[GET /anchors/{anchor}](anchors.md#get-anchor)

## Create Anchor

Creating an anchor will state on the blockchain that one or more document hashes were created at a specific time. In the context of verifiable credentials, anchors are used to attest that the credential document was not altered and was created at a specific time. Batching multiple documents/credentials into a single anchor is done through a Merkle tree and can save on cost/time as only the Merkle root has to be anchored.

The API will store the `blake2b256` hash of a document or string that you provide. Dock provides a [fully functioning reference client](https://fe.dock.io/#/anchor/batch) and [SDK example](https://github.com/docknetwork/sdk/blob/master/example/anchor.js) for anchoring.

### Parameters <a href="#create-anchor-parameters" id="create-anchor-parameters"></a>

<table data-full-width="false"><thead><tr><th width="92">Name</th><th width="82">In</th><th width="126">Type</th><th width="94">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>array of strings or JSON</td><td>true</td><td>Supply an array of strings or JSON documents to be hashed and anchored to the blockchain. For credentials, send the Verifiable Credential document(s) or anchor when issuing.</td></tr></tbody></table>

### Responses <a href="#create-anchor-responses" id="create-anchor-responses"></a>

<table data-header-hidden data-full-width="false"><thead><tr><th width="119">Status</th><th width="169">Meaning</th><th width="307">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will try to create an anchor on the blockchain.</td><td><a href="index.html.md#schemajobid">JobId</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid params.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /anchors REQUEST PAYLOAD</summary>

```json

[
  "can be a string",
  {
    "or": "a JSON document"
  }
]
```

</details>

<details>

<summary>POST /anchors REQUEST CURL</summary>

```bash
curl --location --request POST https://api.dock.io/anchors \

  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '[
  "can be a string",
  {
    "or": "a JSON document"
  }
]'
```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "id": "829",
  "data": {
    "root": "0xdfc3cd9ff7836143746c292d4099e62277fac4c2b6a1c004d784adcbc0319634",
    "proofs": []
  }
}
```

</details>

## List Anchors

Return a list of all anchors created by the authenticated user, regardless of whether they have contributed to the batching or not.

### Parameters <a href="#list-anchors-parameters" id="list-anchors-parameters"></a>

<table data-full-width="false"><thead><tr><th width="112">Name</th><th width="93">In</th><th width="121">Type</th><th width="118">Required</th><th>Description</th></tr></thead><tbody><tr><td>offset</td><td>query</td><td>integer</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

### Responses <a href="#list-anchors-responses" id="list-anchors-responses"></a>

<table data-full-width="false"><thead><tr><th width="120">Status</th><th width="182">Meaning</th><th width="283">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return all anchors created by the user.</td><td>Inline</td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /anchors REQUEST CURL</summary>

```bash
curl --location --request GET https://api.dock.io/anchors \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

</details>

<details>

<summary>200 Response</summary>

<pre class="language-json"><code class="lang-json">[
  {
    "anchor":"54bdd55207c4d41d2b8a7780e967bb5a06bdfb793fc4055baf244e60cd0d839c",
<strong>    "type": "single",
</strong>    "data": {
      "proofs": [],
      "root":"0x54bdd55207c4d41d2b8a7780e967bb5a06bdfb793fc4055baf244e60cd0d839c",
      "documentIds": [
        "https://creds.dock.io/credential/b1ed680d3d2d8167dc31bc4913e9c511"
      ]
     },
     "created_at": "2021-11-12T13:53:51.640Z",
     "job_id": "827"
  }
]
</code></pre>

</details>

## Get Anchor

Get a specific anchor with the given ID.

### Parameters <a href="#get-anchor-parameters" id="get-anchor-parameters"></a>

<table data-full-width="false"><thead><tr><th>Name</th><th>In</th><th>Type</th><th>Required</th><th>Description</th></tr></thead><tbody><tr><td>anchor</td><td>path</td><td><a href="index.html.md#schemahex32">Hex32</a></td><td>true</td><td>An anchor id.</td></tr></tbody></table>

### Responses <a href="#get-anchor-responses" id="get-anchor-responses"></a>

<table data-full-width="false"><thead><tr><th width="119">Status</th><th width="159">Meaning</th><th width="303">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and returns the anchor's details, e.g., <code>blockHash</code> and <code>root</code>.</td><td><a href="index.html.md#schemaanchor">Anchor</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The request was unsuccessful, because the anchor was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /anchors/{anchor} REQUEST CURL</summary>

```bash
curl --location --request GET https://api.dock.io/anchors/{anchor} \
  --header 'DOCK-API-TOKEN: API_KEY'
  --data-raw ''
```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "type": "single",
  "proofs": [],
  "root": "0x00",
  "created_at": "2021-11-30T15:47:24.667Z"
}
```

</details>

## Verify Anchor

Verify an anchor's merkle root and proof by supplying the source documents (array of strings of JSON objects, same as in anchor creation).

### Parameters <a href="#get-anchor-parameters" id="get-anchor-parameters"></a>

<table data-full-width="false"><thead><tr><th width="133">Name</th><th width="101">In</th><th width="148">Type</th><th width="102">Required</th><th>Description</th></tr></thead><tbody><tr><td>documents</td><td>body</td><td>array of strings or JSON</td><td>true</td><td>An array of strings or JSON objects to represent documents to be hashed</td></tr><tr><td>proofs</td><td>body</td><td>JSON object array</td><td>true</td><td>An array of proofs given on anchor creation</td></tr><tr><td>root</td><td>body</td><td><a href="index.html.md#schemahex32">Hex32</a></td><td>true</td><td>The anchor merkle root/ID.</td></tr></tbody></table>

### Responses <a href="#get-anchor-responses" id="get-anchor-responses"></a>

<table data-full-width="false"><thead><tr><th width="110">Status</th><th>Meaning</th><th width="325">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and returns the anchor's details, e.g., <code>blockHash</code> and <code>root</code>.</td><td><a href="index.html.md#schemaanchor">Anchor</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /verify REQUEST PAYLOAD</summary>

```
{
  "documents": [],
  "proofs": [],
  "root": "0x00"
}
```

</details>

<details>

<summary>POST /verify REQUEST CURL</summary>

```bash
curl --location --request POST https://api.dock.io/anchors \

  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '[
  "can be a string",
  {
    "or": "a JSON document"
  }
]'
```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "verified": true,
  "results": [
    {}
  ]
}
```

</details>
