# Credentials

Credential issuance is the process of creating and signing a verifiable credential using the Truvera API. Verifiable Credentials are cryptographically secure and tamper-proof. They cannot be edited once issued, but [they can be revoked](credentials.md#credential-issuance-revocation) and replaced with a new credential.

By default, the Truvera API issues a credential to a holder wallet without storing a copy—only credential metadata is stored. If the holder does not yet have a wallet, we recommend [provisioning a cloud wallet](../credential-wallet/wallet-sdk/cloud-wallet/#step-4-create-a-new-wallet) for that holder and issuing the credential into it. If that is not appropriate for your use case, you can choose to persist the credential, in which case we will encrypt and store the credential for later retrieval using a password.

The following metadata is stored on each issuance:

* Credential ID property
* Credential size in bytes
* Issuer DID
* Issuance date

## Issue credential <a href="#issue-credentials" id="issue-credentials"></a>

Creates and issues a JSON-LD verifiable credential that conforms to the [W3C VCDM specification](https://www.w3.org/TR/vc-data-model/). The `type` values and subject properties must be represented by a schema URI in the `context` property. If you do not specify a `context` property, the API will automatically generate an embedded JSON-LD context based on the properties within your credential. You can read more about JSON-LD and contexts [here](https://json-ld.org/spec/latest/json-ld/#the-context).

{% hint style="info" %}
The `https://www.w3.org/2018/credentials/v1` context URI is always required and will be supplied by default at all times as mandated by the spec. If you pass a custom context, you must ensure that you define all the required JSON-LD terms. Please also note that the request format here is not the same as an issued verifiable credential. You can issue to multiple subjects per credential by passing an array of objects.
{% endhint %}

To sign a credential, an `issuer` must be supplied as either a fully qualified DID string or an object with at least an `id` property which is a fully qualified DID. (e.g: `did:dock:xyz`)

{% hint style="warning" %}
The `issuer` property **must** be a DID that you control with your Truvera account.
{% endhint %}

#### Creating an Example Payload <a href="#zero-knowledge-proofs" id="zero-knowledge-proofs"></a>

As mentioned in the [development tips](getting-started.md#development-tips), you can create an example payload in Truvera Workspace by:

* Open the browser's dev tools
* Look at the network requests
* Manually issue a credential with the desired schema from the desired issuer profile
* In the section that shows HTTP headers, you can copy the Request URL ("Headers" in Google Chrome)
* In the section that shows the request preview, you can copy the text of the request (in Google Chrome, click on "Preview", then right-click on the top-level element "{,...}" and select "Copy object")

#### Zero Knowledge Proofs (ZKP) <a href="#zero-knowledge-proofs" id="zero-knowledge-proofs"></a>

Truvera credentials support [anonymous credentials](https://blog.dock.io/anonymous-credentials/) using Zero Knowledge Proofs and [Selective Disclosure](https://www.dock.io/post/selective-disclosure) by using the BBS2023 signing algorithm when issuing the credential. To enable this functionality, simply set the `algorithm` field in the request to `dockbbs`.

#### Credential distribution <a href="#credential-distribution" id="credential-distribution"></a>

As mentioned above, issued credentials are not stored and so should be issue directly into a holder wallet. Truvera's API has built in credential distribution on issuance, allowing you to send credentials directly to a holder's email and/or Truvera-compatible wallet. You can achieve this by supplying the `recipientEmail` field and `distribute: true` in your request. For DID distribution, simply set the `credentialSubject.id` property to the holder's DID.

In some use cases, you might choose to set the `persist` value to `true` and provide a `password` string which will store the credential contents encrypted on our platform.

#### Revocation <a href="#credential-issuance-revocation" id="credential-issuance-revocation"></a>

In order to support revocation the credential must be linked to a [revocation registry](registries.md) at the time of issuance. To link the revocation registry to the credential set the `status` field in the [Credential](../developer-documentation/dock-api/index.html.md#schemacredential) body to the `registry.id` value.

{% hint style="info" %}
One time use credentials can be created, but automating the revocation based on tracking the verification of the credential ID and revoking the credential associated with it.
{% endhint %}

#### Expiration

An expiration date can be set when issuing a credential making the credential invalid after the assigned time. To check the expiration date for Zero Knowledge Proof credentials (using the dockbbs algorythm) the expiration date needs to be requested in the verification template otherwise due to the nature of zero knowledge proof it will not be disclosed automatically.

#### Attaching files

At the moment it is not possible to add a file to the credential itself. If a credential has to have a file associated with it, the file will need to be placed in public storage and the link to that location and a hash of the content should be added to the attributes of the credential.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/credentials" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## List credentials

When you issue a credential with us, persistent or not, we will store certain metadata about the credential to make it easier for you to reference. You can pull a list of credential metadata using this route. To return the content of a persisted credential, you should use the `GET /credentials/{id}` route.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/credentials" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Get credentials metadata and contents

When a credential has been persisted on our systems, you can fetch the credential data by supplying a credential ID and the password used at issuance to encrypt the credential.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/credentials/{id}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Create request claims <a href="#request-claims" id="request-claims"></a>

Creates a request to gather certain claims and then issues the holder a credential after submission. The claims are user provided and type is based on the schema provided. This can be useful to catch a subject's DID without knowing it beforehand, name or other field. It should only be used when you do not already know this data or cannot find it by other means. There is a risk that a user may enter false data - so use it sparingly and not for fields that are important.

Typically, once the request has been created, you would show the holder the QR URL as an image or deep link for them to scan with a wallet and enter claims. After the holder submits the requested information the credential is automatically issued.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/credentials/request-claims" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Get request claims

Lists all created request claims that are open (the holders have not submitted the requested information).

{% openapi src="../.gitbook/assets/openapi (1).yaml" path="/credentials/request-claims" method="get" %}
[openapi (1).yaml](<../.gitbook/assets/openapi (1).yaml>)
{% endopenapi %}

## Delete credential

A credential can have its metadata deleted, and if persisted the contents will also be deleted. Deleting a credential will remove any reference to it and its contents from our systems. This action cannot be undone. This action will not revoke or invalidate the credential in any way.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/credentials/{id}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}
