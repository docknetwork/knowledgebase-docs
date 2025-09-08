# Messaging API calls

## Encrypt Message

In most cases you'll want to ensure the privacy of the message by encrypting it before sending.

### Parameters <a href="#post__messaging_encrypt-parameters" id="post__messaging_encrypt-parameters"></a>

<table data-full-width="false"><thead><tr><th width="162">Name</th><th width="85">In</th><th width="103">Type</th><th width="115">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>The recipients, sender and message</td></tr><tr><td>» type</td><td>body</td><td>string</td><td>false</td><td>none</td></tr><tr><td>» payload</td><td>body</td><td>object</td><td>true</td><td>none</td></tr><tr><td>» senderDid</td><td>body</td><td>string</td><td>true</td><td>none</td></tr><tr><td>» algorithm</td><td>body</td><td>string</td><td>false</td><td>none</td></tr><tr><td>» recipientDids</td><td>body</td><td>[oneOf]</td><td>true</td><td>none</td></tr></tbody></table>

### **Enumerated Values**

<table data-full-width="false"><thead><tr><th>Parameter</th><th>Value</th></tr></thead><tbody><tr><td>» algorithm</td><td>ECDH-1PU+A256KW</td></tr><tr><td>» algorithm</td><td>ECDH-ES+A256KW</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/messaging/encrypt" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Decrypt Message

### Parameters <a href="#post__messaging_decrypt-parameters" id="post__messaging_decrypt-parameters"></a>

<table data-full-width="false"><thead><tr><th>Name</th><th>In</th><th>Type</th><th>Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>The JWM</td></tr><tr><td>» jwe</td><td>body</td><td>object</td><td>true</td><td>none</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/messaging/decrypt" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Signing Messages

Signing a message helps to prove to the recipient that the message is valid and unaltered. The message will be signed as a Base64 encoded JWT.

### Parameters <a href="#post__messaging_sign-parameters" id="post__messaging_sign-parameters"></a>

<table data-full-width="false"><thead><tr><th width="169">Name</th><th width="79">In</th><th width="89">Type</th><th width="108">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>The message payload</td></tr><tr><td>» payload</td><td>body</td><td>object</td><td>true</td><td>none</td></tr><tr><td>» senderDid</td><td>body</td><td>string</td><td>true</td><td>none</td></tr><tr><td>» type</td><td>body</td><td>string</td><td>false</td><td>none</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/messaging/sign" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Verifying a Message

Verify that the message is valid.

### Parameters <a href="#post__messaging_verify-parameters" id="post__messaging_verify-parameters"></a>

<table data-full-width="false"><thead><tr><th width="112">Name</th><th width="88">In</th><th width="110">Type</th><th width="135">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>The message payload</td></tr><tr><td>» jws</td><td>body</td><td>string</td><td>true</td><td>none</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/messaging/verify" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Send Message

Sends a DIDComm message using our relay service and DID service endpoints, it also returns a URL for QR code scanning. Supports encrypted, plaintext and signed DIDComm messages. You can generate an encrypted DIDComm message by calling the `/messaging/encrypt` route.

The `typ` attribute must be a DIDComm type (i.e. starts with "application/didcomm").

### Parameters <a href="#post__messaging_send-parameters" id="post__messaging_send-parameters"></a>

<table data-full-width="false"><thead><tr><th width="134">Name</th><th width="83">In</th><th width="107">Type</th><th width="116">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>The message payload</td></tr><tr><td>» to</td><td>body</td><td>string</td><td>true</td><td>none</td></tr><tr><td>» message</td><td>body</td><td>Message</td><td>true</td><td>none</td></tr></tbody></table>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/messaging/send" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}
