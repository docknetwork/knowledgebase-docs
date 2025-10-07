# DIDs

DID stands for Decentralized IDentifiers. DIDs are meant to be globally unique identifiers that allow their owner to prove cryptographic control over them. A DID identifies any subject (e.g., a person, organization, thing, data model, abstract entity, etc.) that the controller of the DID decides that it identifies.

In Truvera, Decentralized Identifiers (DIDs) are created using the UUID v4 standard. This involves selecting a unique 128-bit identifier, typically represented as a 36-character hexadecimal string, along with an initial public key. Users have the flexibility to add and remove public keys associated with their DID document as needed. Additionally, the system supports various operations such as updating, deactivating, and listing all existing DIDs.

For a detailed example of the DIDs workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/didFlow.js).

## Create DID

A DID, a public key, and a controller are required to create a new DID. The controller is both the owner of the public key and a DID. The DID can be created using an auto-generated keypair, and the controller will be the same as the DID unless otherwise specified. The DID and public key have no cryptographic relation.

It is important to have a public key types that is supported by Truvera, the supported type of public key is `ed25519.`

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/dids" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Import DIDs

Import an already existing DID, possibly created in another platform, to take advantage of Truvera's advanced functions like ecosystems and monetized credentials.

{% openapi-operation spec="dock-labs-api" path="/dids/import" method="post" %}
[OpenAPI dock-labs-api](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi-operation %}

## List DIDs

Return a list of all DIDs that your user account controls as fully resolved DID documents.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/dids" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}





## Return ecosystems that DID participates in <a href="#list-dids-parameters" id="list-dids-parameters"></a>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/dids/{did}/ecosystems" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



## Export DID

Exports the DID document and keys as an encrypted Universal Wallet JSON-LD document

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/dids/{did}/export" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



## Get DID

When a DID is provided in the path, the API will attempt to resolve that DID into a [DID document](https://www.w3.org/TR/did-core/#dfn-did-documents). This document contains the public keys and more information relating to that DID, check [the identity foundation did configuration](https://identity.foundation/.well-known/resources/did-configuration/) document to learn more.

The API supports resolving many DID methods, some examples are:

* did:cheqd:f48d2ace-4947-4cb7-8550-1cef3d63e651 - resolves through the cheqd blockchain
* did:key:z6MkjRagNiMu91DduvCvgEsqLZDVzrJzFrwahc4tXLt9DoHd- the public key is embedded in the DID

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/dids/{did}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/dids/{did}/metadata" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Delete DID <a href="#list-dids-parameters" id="list-dids-parameters"></a>

Deletes a DID and its metadata from the blockchain and our platform. This will also delete the associated keypair from the key management system meaning that you cannot sign messages or credentials with it after this operation. The DID will no longer be able to be resolved. This operation is not reversible.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/dids/{did}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



