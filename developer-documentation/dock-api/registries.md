# Registries

Revocation means deleting or updating a credential. On Dock, credential revocation is managed with a revocation registry.

There can be multiple registries on the chain, and each registry has a unique id. It is recommended that the revocation authority create a new registry for each credential type. Dock Certs allows you to create, delete, and revoke/unrevoke the credential. You can retrieve a specified registry as well as a list of all registries created by the user.

For a detailed example of the registry workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/registryFlow.js).

{% hint style="info" %}
If you want to revoke BBS+ credentials, you must create a registry with type \`DockVBAccumulator2022\`. For revoking other credentials, you can use \`StatusList2021Entry\` or \`CredentialStatusList2017\`.
{% endhint %}

## Endpoints

[POST /registries](registries.md#create-registry)\
[GET /registries](registries.md#list-registries)\
[GET /registries/{id}](registries.md#get-registry)\
[POST /registries/{id}](registries.md#revoke-unrevoke-credential)\
[DELETE /registries/{id}](registries.md#delete-registry)

## Create Registry

To create a registry, you have to create a `policy` object for which a DID is needed. It is advised that the DID is registered on the chain first. Otherwise, someone can look at the registry and register the DID, thus gaining control of the registry.

Choosing the right revocation registry is essential. Here's a simplified overview of the available options:

* CredentialStatusList2017
  * Only supports non-BBS+ credentials.
  * Individual Tracking: Each entry is tracked separately, which means more ledger space is used for multiple entries.
  * This registry is cost-effective for a single entry. However, managing several entries can be more expensive.
  * Implements add-only policies.
* StatusList2021Entry
  * Only supports non-BBS+ credentials.
  * Recommended for most users.
  * Collective Tracking: Manages all revocation entries together, making it less costly to revoke multiple credentials simultaneously.
  * W3C Compliant.
* DockVBAccumulator2022
  * Only supports BBS+ credentials.
  * Utilizes an on-ledger accumulator for enhanced privacy.
  * Offers more privacy than the W3C Status List 2021.

### Parameters <a href="#create-registry-parameters" id="create-registry-parameters"></a>

<table data-full-width="true"><thead><tr><th width="119">Name</th><th width="82">In</th><th width="118">Type</th><th width="117">Required</th><th>Description</th></tr></thead><tbody><tr><td>addOnly</td><td>body</td><td>boolean</td><td>false</td><td>True/false options. The default value is "false".</td></tr><tr><td>policy</td><td>body</td><td>[<a href="index.html.md#schemadiddock">DIDDock</a>]</td><td>true</td><td>The DIDs which control this registry. You must own a DID listed here to use the registry. Only one policy supported as of now: <code>OneOf</code> DID in list.</td></tr><tr><td>type</td><td>body</td><td>string</td><td>false</td><td>Specifies which type of registry to create. Defaults to <code>StatusList2021Entry</code>.</td></tr></tbody></table>

### Enumerated Values

<table data-full-width="true"><thead><tr><th width="160">Parameter</th><th width="294">Value</th><th>Description</th></tr></thead><tbody><tr><td>type</td><td>StatusList2021Entry <strong>or</strong> CredentialStatusList2017 <strong>or</strong> DockVBAccumulator2022</td><td>The type used in registry creation.</td></tr></tbody></table>

### Responses <a href="#create-registry-responses" id="create-registry-responses"></a>

<table data-full-width="true"><thead><tr><th width="107">Status</th><th width="156">Meaning</th><th width="308">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will try to create the registry.</td><td><a href="index.html.md#schemajobstartedresult">JobStartedResult</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid params, e.g., policy not supported.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /registries REQUEST PAYLOAD</summary>

```json
{
  "addOnly": true,
  "policy": [
    "did:dock:xyz"
  ],
  "type": "CredentialStatusList2017"
}
```

</details>

<details>

<summary>POST /registries REQUEST CURL</summary>

```bash
curl --location --request POST https://api.dock.io/registries/ \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
  "addOnly": true,
  "policy": [
    "did:dock:xyz"
  ],
  "type": "CredentialStatusList2017"
}'


```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "id": "930",
  "data": {
    "id": "6151e62d7e03bc4012fde0595cfdb0d140e463a2f0ad5a431ff47243374bc612",
    "policy": {
      "type": "OneOf",
      "policy": [
        "did:dock:5GKeTJ7iMU4hEUwhK9a6ogh1bsWAv8Z1TMKnUf1vCNgdoiEM"
      ],
      "addOnly": false
    },
    "type": "CredentialStatusList2017",
  }
}
```

</details>

## List Registries

Return a list of all registries created by the user. The list is returned with the registry id and policy of the revocation registry.

{% hint style="info" %}
For now, only one policy is supported, and each registry is owned by a single DID.
{% endhint %}

### Parameters <a href="#list-dids-parameters" id="list-dids-parameters"></a>

<table data-full-width="true"><thead><tr><th width="116">Name</th><th width="94">In</th><th width="95">Type</th><th width="119">Required</th><th>Description</th></tr></thead><tbody><tr><td>offset</td><td>query</td><td>integer</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

### Responses <a href="#list-registries-responses" id="list-registries-responses"></a>

<table data-full-width="true"><thead><tr><th width="120">Status</th><th width="163">Meaning</th><th width="311">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return all registries created by the user.</td><td>Inline</td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /registries REQUEST CURL</summary>

```bash
curl --location --request GET https://api.dock.io/registries/ \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw'{

  }'

```

</details>

<details>

<summary>200 Response</summary>

```json
[
  {
    "id": "6151e62d7e03bc4012fde0595cfdb0d140e463a2f0ad5a431ff47243374bc612",
    "policy_and_type": {
      "type": "OneOf",
      "policy": [
        "did:dock:5GKeTJ7iMU4hEUwhK9a6ogh1bsWAv8Z1TMKnUf1vCNgdoiEM"
      ],
      "addOnly": false
    },
    "registry_type": "CredentialStatusList2017",
    "created_at": "2021-11-25T12:20:51.773Z"
  }
]
```

</details>

## Get Registry

Get the details of an existing registry, such as policy, add-only status, when it was last updated, and controller(s). You need only supply the revocation registry id that was returned upon revocation registry creation.

### Parameters <a href="#get-registry-parameters" id="get-registry-parameters"></a>

<table data-full-width="true"><thead><tr><th width="100">Name</th><th width="88">In</th><th width="104">Type</th><th width="160">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td><a href="index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Revocation registry id.</td></tr></tbody></table>

### Responses <a href="#get-registry-responses" id="get-registry-responses"></a>

<table data-full-width="true"><thead><tr><th width="116">Status</th><th width="159">Meaning</th><th width="316">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return the revocation registry metadata.</td><td><a href="index.html.md#schemaregistry">Registry</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The request was unsuccessful, because the registry was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /registries/{id} REQUEST CURL</summary>

```bash
curl --location --request GET https://api.dock.io/registries/{id} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''


```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "id": "6151e62d7e03bc4012fde0595cfdb0d140e463a2f0ad5a431ff47243374bc612",
  "policy_and_type": {
    "type": "OneOf",
    "policy": [
      "did:dock:5GKeTJ7iMU4hEUwhK9a6ogh1bsWAv8Z1TMKnUf1vCNgdoiEM"
    ],
    "addOnly": false
  },
  "registry_type": "CredentialStatusList2017",
  "created_at": "2021-11-25T12:20:51.773Z",
  "job_id": "930"
}
```

</details>

## Revoke/Unrevoke Credential

Credential revocation is managed with on-chain revocation registries. To revoke a credential, its id (or hash of its id) must be added to the credential. It is advised to have one revocation registry per credential type. Revoking an already revoked credential has no effect.

Similar to the replay protection mechanism for DIDs, the last modified block number is kept for each registry, which is updated each time a credential is revoked or unrevoked. Unrevoking an unrevoked credential has no effect.

In this API, simply add Revoke/Unrevoke into the `action` parameter and input the desired credential ids.

### Parameters <a href="#revoke-unrevoke-credential-parameters" id="revoke-unrevoke-credential-parameters"></a>

<table data-full-width="true"><thead><tr><th width="147">Name</th><th width="89">In</th><th width="96">Type</th><th width="106">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td><a href="index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Revocation registry id.</td></tr><tr><td>action</td><td>body</td><td>string</td><td>false</td><td>The action taken, either revoke or unrevoke. The default value is "revoke"</td></tr><tr><td>credentialIds</td><td>body</td><td>array</td><td>true</td><td>The list of credential ids to act upon.</td></tr></tbody></table>

### Enumerated Values

<table data-full-width="true"><thead><tr><th width="141">Parameter</th><th width="205">Value</th><th>Description</th></tr></thead><tbody><tr><td>action</td><td>revoke <strong>or</strong> unrevoke</td><td>Action to take on the registry.</td></tr></tbody></table>

<table data-full-width="true"><thead><tr><th width="122">Status</th><th width="152">Meaning</th><th width="264">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will try to revoke/unrevoke the credential.</td><td><a href="index.html.md#schemajobstartedresult">JobStartedResult</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid params.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The request was unsuccessful, because the registry was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /registries/{id} REQUEST PAYLOAD</summary>

```json

{
  "action": "revoke",
  "credentialIds": [
    "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb"
  ]
}
```

</details>

<details>

<summary>POST /registries/{id} REQUEST CURL</summary>

```bash
curl --location --request POST https://api.dock.io/registries/{id} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
  "action": "revoke",
  "credentialIds": [
    "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb"
  ]
}'

```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "id": "931",
  "data": {
    "revokeIds": [
      "0xaff1aa6770d43d684690c0ad679a8608d5b7576feb3fdc1d6712decf73ca44ef"
    ]
  }
}
```

</details>

## Delete Registry

A registry can be deleted, leading to all the corresponding revocation ids being deleted as well. This requires the signature from the owner, similar to the other updates.

### Parameters <a href="#delete-registry-parameters" id="delete-registry-parameters"></a>

<table data-full-width="true"><thead><tr><th width="105">Name</th><th width="85">In</th><th width="126">Type</th><th width="137">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td><a href="index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Revocation registry id.</td></tr></tbody></table>

### Responses <a href="#delete-registry-responses" id="delete-registry-responses"></a>

<table data-full-width="true"><thead><tr><th width="115">Status</th><th width="175">Meaning</th><th width="256">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and revocation registry will be deleted.</td><td><a href="index.html.md#schemajobstartedresult">JobStartedResult</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The request was unsuccessful, because the registry was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>DELETE /registries/{id} REQUEST CURL</summary>

```bash
curl --location --request POST https://api.dock.io/registries/{id} \
  --header 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "id": "932",
  "data": {
  "id": "6151e62d7e03bc4012fde0595cfdb0d140e463a2f0ad5a431ff47243374bc612",
  "hexId": "6151e62d7e03bc4012fde0595cfdb0d140e463a2f0ad5a431ff47243374bc612",
  "lastModified": 4226296
  }
}
```

</details>
