# Revocation status

Credentials can be revoked or unrevoked, and as such they contain a revocation status so that verifiers/issuers can check if the credential is still valid. Once a revocation registry has been created and credentials issued with it, you can check the revocation status. Verifiers will do this automatically.

## Get revocation status

To check if an id is revoked or not, you can check its status with the registry id (`regId`) and revocation id (`revId`).

### Parameters <a href="#get-revocation-status-parameters" id="get-revocation-status-parameters"></a>

<table data-full-width="false"><thead><tr><th width="118">Name</th><th width="106">In</th><th width="117">Type</th><th width="130">Required</th><th>Description</th></tr></thead><tbody><tr><td>regId</td><td>path</td><td><a href="../developer-documentation/dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Revocation registry id.</td></tr><tr><td>revId</td><td>path</td><td><a href="../developer-documentation/dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Credential revocation id.</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/revocationStatus/{regId}/{revId}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Get revocation status witness

The accumulator witness is utilized by the holder to generate a proof, which combines the witness with their revocation id associated with the credential id (`revId`) and the accumulator associated with the registry id (`regId`), allowing the verifier to validate the credential's status without directly accessing the revocation id on the blockchain.

### Parameters <a href="#get-revocation-status-parameters" id="get-revocation-status-parameters"></a>

<table><thead><tr><th width="113">Name</th><th width="93">In</th><th width="117">Type</th><th width="123">Required</th><th>Description</th></tr></thead><tbody><tr><td>regId</td><td>path</td><td><a href="../developer-documentation/dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Revocation registry id.</td></tr><tr><td>revId</td><td>path</td><td><a href="../developer-documentation/dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Credential revocation id.</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/revocationStatus/{regId}/{revId}/witness" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

