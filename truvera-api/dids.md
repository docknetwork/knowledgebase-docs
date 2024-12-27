# DIDs

DID stands for Decentralized IDentifiers. DIDs are meant to be globally unique identifiers that allow their owner to prove cryptographic control over them. A DID identifies any subject (e.g., a person, organization, thing, data model, abstract entity, etc.) that the controller of the DID decides that it identifies.

DIDs in Truvera are created by choosing a 32-byte unique identifier along with a public key. You can update and delete a DID as well as list all DIDs. DID is identified by a unique, random key.

For a detailed example of the DIDs workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/didFlow.js).

## Create DID

A DID, a public key, and a controller are required to create a new DID. The controller is both the owner of the public key and a DID. The DID can be created using an auto-generated keypair, and the controller will be the same as the DID unless otherwise specified. The DID and public key have no cryptographic relation.

It is important to have a public key types that is supported by Truvera, the supported type of public key is `ed25519.`

{% hint style="info" %}
When creating a Polygon ID DID, be sure to set the \`keyType\` field to \`bjj\`.
{% endhint %}

{% swagger src="https://swagger-api.truvera.io/openapi.yaml" path="/dids" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endswagger %}

## List DIDs

Return a list of all DIDs that your user account controls as fully resolved DID documents.

{% swagger src="https://swagger-api.truvera.io/openapi.yaml" path="/dids" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endswagger %}





## Return ecosystems that DID participates in <a href="#list-dids-parameters" id="list-dids-parameters"></a>

{% swagger src="https://swagger-api.truvera.io/openapi.yaml" path="/dids/{did}/ecosystems" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endswagger %}



## Export DID

Exports the DID document and keys as an encrypted Universal Wallet JSON-LD document

{% swagger src="https://swagger-api.truvera.io/openapi.yaml" path="/dids/{did}/export" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endswagger %}



## Get DID

When a DID is provided in the path, the API will attempt to resolve that DID into a [DID document](https://www.w3.org/TR/did-core/#dfn-did-documents). This document contains the public keys and more information relating to that DID, check [the identity foundation did configuration](https://identity.foundation/.well-known/resources/did-configuration/) document to learn more.

The API supports resolving many DID methods, some examples are:

* `did:dock:5CEdyZkZnALDdCAp7crTRiaCq6KViprTM6kHUQCD8X6VqGPW` - resolves through the Dock blockchain
* `did:key:z6MkjRagNiMu91DduvCvgEsqLZDVzrJzFrwahc4tXLt9DoHd` - the public key is embedded in the DID

{% swagger src="https://swagger-api.truvera.io/openapi.yaml" path="/dids/{did}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endswagger %}

{% swagger src="https://swagger-api.truvera.io/openapi.yaml" path="/dids/{did}/metadata" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endswagger %}

## Delete DID <a href="#list-dids-parameters" id="list-dids-parameters"></a>

Deletes a DID and its metadata from the blockchain and our platform. This will also delete the associated keypair from the key management system meaning that you cannot sign messages or credentials with it after this operation. The DID will no longer be able to be resolved. This operation is not reversible.

{% swagger src="https://swagger-api.truvera.io/openapi.yaml" path="/dids/{did}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endswagger %}



