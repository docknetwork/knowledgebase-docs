# Registries

Revocation means deleting or updating a credential. Truvera's credential revocation is managed with a revocation registry.

There can be multiple registries on the chain, and each registry has a unique id. It is recommended that the revocation authority create a new registry for each credential type. Truvera Workspace allows you to create, delete, and revoke/unrevoke the credential. You can retrieve a specified registry as well as a list of all registries created by the user.

For a detailed example of the registry workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/registryFlow.js).

{% hint style="info" %}
If you want to revoke ZKP credentials, you must create a registry with type \`DockVBAccumulator2022\`. For revoking other credentials, you can use \`StatusList2021Entry\`.
{% endhint %}

## Create registry

To create a registry, you have to create a `policy` object for which a DID is needed. It is advised that the DID is registered on the chain first. Otherwise, someone can look at the registry and register the DID, thus gaining control of the registry.

Choosing the right revocation registry is essential. Here's a simplified overview of the available options:

* StatusList2021Entry
  * Only supports non-ZKP credentials.
  * Recommended for most users.
  * Collective Tracking: Manages all revocation entries together, making it less costly to revoke multiple credentials simultaneously.
  * W3C Compliant.
* DockVBAccumulator2022
  * Only supports ZKP credentials.
  * Utilizes an on-ledger accumulator for enhanced privacy.
  * Offers more privacy than the W3C Status List 2021.

CredentialStatusList2017 (Deprecated)

* Only supports non-ZKP credentials.
* Individual Tracking: Each entry is tracked separately, which means more ledger space is used for multiple entries.
* This registry is cost-effective for a single entry. However, managing several entries can be more expensive.
* Implements add-only policies.

### Parameters <a href="#create-registry-parameters" id="create-registry-parameters"></a>

<table data-full-width="false"><thead><tr><th width="119">Name</th><th width="82">In</th><th width="118">Type</th><th width="117">Required</th><th>Description</th></tr></thead><tbody><tr><td>addOnly</td><td>body</td><td>boolean</td><td>false</td><td>True/false options. The default value is "false".</td></tr><tr><td>policy</td><td>body</td><td>[<a href="../developer-documentation/dock-api/index.html.md#schemadiddock">DIDDock</a>]</td><td>true</td><td>The DIDs which control this registry. You must own a DID listed here to use the registry. Only one policy supported as of now: <code>OneOf</code> DID in list.</td></tr><tr><td>type</td><td>body</td><td>string</td><td>false</td><td>Specifies which type of registry to create. Defaults to <code>StatusList2021Entry</code>.</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/registries" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



## List registries

Return a list of all registries created by the user. The list is returned with the registry id and policy of the revocation registry.

{% hint style="info" %}
For now, only one policy is supported, and each registry is owned by a single DID.
{% endhint %}

### Parameters <a href="#list-dids-parameters" id="list-dids-parameters"></a>

<table data-full-width="false"><thead><tr><th width="116">Name</th><th width="94">In</th><th width="95">Type</th><th width="119">Required</th><th>Description</th></tr></thead><tbody><tr><td>offset</td><td>query</td><td>integer</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/registries" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



## Get registry

Get the details of an existing registry, such as policy, add-only status, when it was last updated, and controller(s). You need only supply the revocation registry id that was returned upon revocation registry creation.

### Parameters <a href="#get-registry-parameters" id="get-registry-parameters"></a>

<table data-full-width="false"><thead><tr><th width="100">Name</th><th width="88">In</th><th width="104">Type</th><th width="160">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td><a href="../developer-documentation/dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Revocation registry id.</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/registries/{id}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Revoke or unrevoke a credential

Credential revocation is managed with on-chain revocation registries. To revoke a credential, its id (or hash of its id) must be added to the credential. It is advised to have one revocation registry per credential type. Revoking an already revoked credential has no effect.

Similar to the replay protection mechanism for DIDs, the last modified block number is kept for each registry, which is updated each time a credential is revoked or unrevoked. Unrevoking an unrevoked credential has no effect.

In this API, simply add Revoke/Unrevoke into the `action` parameter and input the desired credential ids.

### Parameters <a href="#revoke-unrevoke-credential-parameters" id="revoke-unrevoke-credential-parameters"></a>

<table data-full-width="false"><thead><tr><th width="147">Name</th><th width="89">In</th><th width="96">Type</th><th width="106">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td><a href="../developer-documentation/dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Revocation registry id.</td></tr><tr><td>action</td><td>body</td><td>string</td><td>false</td><td>The action taken, either revoke or unrevoke. The default value is "revoke"</td></tr><tr><td>credentialIds</td><td>body</td><td>array</td><td>true</td><td>The list of credential ids to act upon.</td></tr></tbody></table>

### Enumerated values

<table data-full-width="false"><thead><tr><th width="141">Parameter</th><th width="205">Value</th><th>Description</th></tr></thead><tbody><tr><td>action</td><td>revoke <strong>or</strong> unrevoke</td><td>Action to take on the registry.</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/registries/{id}" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Delete registry

A registry can be deleted, leading to all the corresponding revocation ids being deleted as well. This requires the signature from the owner, similar to the other updates.

### Parameters <a href="#delete-registry-parameters" id="delete-registry-parameters"></a>

<table data-full-width="false"><thead><tr><th width="105">Name</th><th width="85">In</th><th width="126">Type</th><th width="137">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td><a href="../developer-documentation/dock-api/index.html.md#schemahex32">Hex32</a></td><td>true</td><td>Revocation registry id.</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/registries/{id}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

