# Credentials

You can create and sign Verifiable Credentials using Truvera API. By default, Dock does not store the credential - only its metadata. You can choose to persist a credential, in which case we will encrypt and store the credential for later retrieval using a password. Verifiable Credentials are cryptographically secure and tamper-proof. Once issued, they cannot be edited.

## Issue Credential <a href="#issue-credentials" id="issue-credentials"></a>

Creates and issues a JSON-LD Verifiable Credential that conforms to the [W3C VCDM specification](https://www.w3.org/TR/vc-data-model/). The `type` values and subject properties must be represented by a schema URI in the `context` property. If you do not specify a `context` property, the API will automatically generate an embedded JSON-LD context based on the properties within your credential. You can read more about JSON-LD and contexts [here](https://json-ld.org/spec/latest/json-ld/#the-context).

{% hint style="info" %}
The `https://www.w3.org/2018/credentials/v1` context URI is always required and will be supplied by default at all times as mandated by the spec. If you pass a custom context, you must ensure that you define all the required JSON-LD terms. Please also note that the request format here is not the same as an issued verifiable credential. You can issue to multiple subjects per credential by passing an array of objects.
{% endhint %}

To sign a credential, an `issuer` must be supplied as either a fully qualified DID string or an object with at least an `id` property which is a fully qualified DID. (e.g: `did:dock:xyz`)

{% hint style="warning" %}
The `issuer` property **must** be a DID that you control with Dock Certs.
{% endhint %}

{% hint style="info" %}
For Polygon ID credentials:

* In order to issue Polygon ID credentials, the issuer **must** be a `did:polygonid` issuer.
* Polygon ID credentials **do not** support designs at this point so `template` field should be omitted.
{% endhint %}

By default, Dock does not store the credential contents at all - only minimal credential metadata. You can choose to set the `persist` value to `true` and provide a `password` string which will store the credential contents encrypted on our platform. The following metadata is stored on each issuance:

* Credential ID property
* Credential size in bytes
* Issuer DID
* Issuance date

For a detailed example of the credential workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/credentialsFlow.js).

#### Zero Knowledge Proofs (ZKP) <a href="#zero-knowledge-proofs" id="zero-knowledge-proofs"></a>

Dock credentials support [anonymous credentials](https://blog.dock.io/anonymous-credentials/) using Zero Knowledge Proofs and [Selective Disclosure](https://www.dock.io/post/selective-disclosure) by using the BBS2023 signing algorithm when issuing the credential. To enable this functionality, simply set the `algorithm` field in the request to `dockbbs`.

#### Credential Distribution <a href="#credential-distribution" id="credential-distribution"></a>

Dock's API has built in credential distribution on issuance, allowing you to send credentials directly to a holder's email and/or Dock-compatible wallet. You can achieve this by supplying the `recipientEmail` field and `distribute: true` in your request. For DID distribution, simply set the `credentialSubject.id` property to the holder's DID.

#### Revocation <a href="#credential-issuance-revocation" id="credential-issuance-revocation"></a>

In order to support revocation the credential must be linked to a [revocation registry](registries.md) at the time of issuance. To link the revocation registry to the credential set the `status` field in the [Credential](../dock-api/index.html.md#schemacredential) body to the `registry.id` value.

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/credentials" method="post" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## List Credentials

When you issue a credential with us, persistent or not, we will store certain metadata about the credential to make it easier for you to reference. You can pull a list of credential metadata using this route. To return the content of a persisted credential, you should use the `GET /credentials/{id}` route.

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/credentials" method="get" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## Get credentials metadata and contents

When a credential has been persisted on our systems, you can fetch the credential data by supplying a credential ID and the password used at issuance to encrypt the credential.

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/credentials/{id}" method="get" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## Create request claims <a href="#request-claims" id="request-claims"></a>

Creates a request to gather certain claims and then issues the holder a credential after submission. The claims are user provided and type is based on the schema provided. This can be useful to catch a subject's DID without knowing it beforehand, name or other field. It should only be used when you do not already know this data or cannot find it by other means. There is a risk that a user may enter false data - so use it sparingly and not for fields that are important.

Typically, once the request has been created, you would show the holder the QR URL as an image or deep link for them to scan with a wallet and enter claims. After the holder submits the requested information the credential is automatically issued.

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/credentials/request-claims" method="post" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}



## Get request claims

Lists all created request claims that are open (the holders have not submited the requested information).

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/credentials/request-claims" method="get" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}



{% swagger src="../../.gitbook/assets/openapi (1).yaml" path="/credentials/request-claims" method="get" %}
[openapi (1).yaml](<../../.gitbook/assets/openapi (1).yaml>)
{% endswagger %}



## Delete Credential

A credential can have its metadata deleted, and if persisted the contents will also be deleted. Deleting a credential will remove any reference to it and its contents from our systems. This action cannot be undone. This action will not revoke or invalidate the credential in any way.

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/credentials/{id}" method="delete" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}



