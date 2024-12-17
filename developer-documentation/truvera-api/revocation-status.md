# Revocation Status

Credentials can be revoked or unrevoked, and as such they contain a revocation status so that verifiers/issuers can check if the credential is still valid. Once a revocation registry has been created and credentials issued with it, you can check the revocation status. Verifiers will do this automatically.

## Get Revocation Status

To check if an id is revoked or not, you can check its status with the registry id (`regId`) and revocation id (`revId`).

### Parameters <a href="#get-revocation-status-parameters" id="get-revocation-status-parameters"></a>

<table data-full-width="false"><thead><tr><th width="118">Name</th><th width="106">In</th><th width="117">Type</th><th width="130">Required</th><th>Description</th></tr></thead><tbody><tr><td>regId</td><td>path</td><td><a href="../dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Revocation registry id.</td></tr><tr><td>revId</td><td>path</td><td><a href="../dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Credential revocation id.</td></tr></tbody></table>

### Responses <a href="#get-revocation-status-responses" id="get-revocation-status-responses"></a>

<table><thead><tr><th width="131">Status</th><th width="144">Meaning</th><th width="304">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return <strong>true</strong>, if the credential is revoked, <strong>false</strong> otherwise.</td><td>Inline</td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The request was unsuccessful, because the registry was not found.</td><td><a href="../dock-api/index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="../dock-api/index.html.md#schemaerror">Error</a></td></tr><tr><td>400</td><td><a href="https://datatracker.ietf.org/doc/html/rfc7231#section-6.6.1">Server Error</a></td><td>The request was unsuccessful, because you have not revoked or unrevoked the registered credential yet. Please try to revoke/unrevoke the registered credential and try again.</td><td><a href="../dock-api/index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /revocationStatus/{regId}/{revId} REQUEST CURL</summary>

```bash
curl --location --request GET https://api.dock.io/revocationStatus/{regId}/{revId} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "type": true
}
```

</details>

## Get Revocation Status Witness

The accumulator witness is utilized by the holder to generate a proof, which combines the witness with their revocation id associated with the credential id (`revId`) and the accumulator associated with the registry id (`regId`), allowing the verifier to validate the credential's status without directly accessing the revocation id on the blockchain.

### Parameters <a href="#get-revocation-status-parameters" id="get-revocation-status-parameters"></a>

<table><thead><tr><th width="113">Name</th><th width="93">In</th><th width="117">Type</th><th width="123">Required</th><th>Description</th></tr></thead><tbody><tr><td>regId</td><td>path</td><td><a href="../dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Revocation registry id.</td></tr><tr><td>revId</td><td>path</td><td><a href="../dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Credential revocation id.</td></tr></tbody></table>

### Responses <a href="#get-revocation-status-responses" id="get-revocation-status-responses"></a>

<table><thead><tr><th width="129">Status</th><th width="173">Meaning</th><th width="283">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return the membership witness.</td><td>Inline</td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The request was unsuccessful, because the registry was not found.</td><td><a href="../dock-api/index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="../dock-api/index.html.md#schemaerror">Error</a></td></tr><tr><td>400</td><td><a href="https://datatracker.ietf.org/doc/html/rfc7231#section-6.6.1">Server Error</a></td><td>The request was unsuccessful, because you have not revoked or unrevoked the registered credential yet. Please try to revoke/unrevoke the registered credential and try again.</td><td><a href="../dock-api/index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /revocationStatus/{regId}/{revId}/witness REQUEST CURL</summary>

```bash

curl --location --request GET https://api.dock.io/revocationStatus/{regId}/{revId} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''
```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "value": "0x81aa308882b663491e2b42803ad0855b030d92a586bc378bc844e1e003c8098a23f0d7d75b4fdbfb4b42cfc42aca8ad3"
}
```

</details>
