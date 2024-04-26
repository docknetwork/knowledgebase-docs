# Messaging

Operations about DIDComm messaging. DIDComm messages are addressed by DID using Dock's relay service.

The current most common use case for the messaging service is to send credentials and presentation requests to the Dock Wallet, but other clients can use it too.

## Encrypt Message

In most cases you'll want to ensure the privacy of the message by encrypting it before sending.

### Parameters <a href="#post__messaging_encrypt-parameters" id="post__messaging_encrypt-parameters"></a>

<table data-full-width="false"><thead><tr><th width="162">Name</th><th width="85">In</th><th width="103">Type</th><th width="115">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>The recipients, sender and message</td></tr><tr><td>» type</td><td>body</td><td>string</td><td>false</td><td>none</td></tr><tr><td>» payload</td><td>body</td><td>object</td><td>true</td><td>none</td></tr><tr><td>» senderDid</td><td>body</td><td>string</td><td>true</td><td>none</td></tr><tr><td>» algorithm</td><td>body</td><td>string</td><td>false</td><td>none</td></tr><tr><td>» recipientDids</td><td>body</td><td>[oneOf]</td><td>true</td><td>none</td></tr></tbody></table>

### **Enumerated Values**

<table data-full-width="false"><thead><tr><th>Parameter</th><th>Value</th></tr></thead><tbody><tr><td>» algorithm</td><td>ECDH-1PU+A256KW</td></tr><tr><td>» algorithm</td><td>ECDH-ES+A256KW</td></tr></tbody></table>

### Responses <a href="#post__messaging_encrypt-responses" id="post__messaging_encrypt-responses"></a>

<table data-full-width="false"><thead><tr><th width="107">Status</th><th width="173">Meaning</th><th width="299">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Message has been encrypted, returning an encrypted DIDComm Message</td><td><a href="index.html.md#schemaresponse">Response</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>Message failed to encrypt</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.2">Payment Required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>DID was not found</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /messaging/encrypt REQUEST CURL</summary>

```bash
# You can also use wget
curl -X POST https://api-testnet.dock.io/messaging/encrypt \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>Body parameter</summary>

```json
{
  "type": "https://didcomm.org/issue-credential/2.0/issue-credential",
  "payload": {
    "domain": "api.dock.io",
    "credentials": [{ ...vcJSON }]
  },
  "senderDid": "did:dock:xyz",
  "algorithm": "ECDH-1PU+A256KW",
  "recipientDids": [
    "did:dock:xyz"
  ]
}
```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "code": 0
}
```

</details>

## Decrypt Message

### Parameters <a href="#post__messaging_decrypt-parameters" id="post__messaging_decrypt-parameters"></a>

<table data-full-width="false"><thead><tr><th>Name</th><th>In</th><th>Type</th><th>Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>The JWM</td></tr><tr><td>» jwe</td><td>body</td><td>object</td><td>true</td><td>none</td></tr></tbody></table>

### Responses <a href="#post__messaging_decrypt-responses" id="post__messaging_decrypt-responses"></a>

<table data-full-width="false"><thead><tr><th width="121">Status</th><th width="175">Meaning</th><th width="284">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Message has been decrypted, returning a DIDComm message</td><td><a href="index.html.md#schemaresponse">Response</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>Message failed to decrypt</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.2">Payment Required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>DID was not found</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /messaging/decrypt REQUEST CURL</summary>

```bash
# You can also use wget
curl -X POST https://api-testnet.dock.io/messaging/decrypt \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>Body parameter</summary>

```json
{
  "jwe": {}
}
```

</details>

<details>

<summary>200 Response</summary>

```json
{
  "code": 0
}
```

</details>

## Signing Messages

Signing a message helps to prove to the recipient that the message is valid and unaltered. The message will be signed as a Base64 encoded JWT.

### Parameters <a href="#post__messaging_sign-parameters" id="post__messaging_sign-parameters"></a>

<table data-full-width="false"><thead><tr><th width="169">Name</th><th width="79">In</th><th width="89">Type</th><th width="108">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>The message payload</td></tr><tr><td>» payload</td><td>body</td><td>object</td><td>true</td><td>none</td></tr><tr><td>» senderDid</td><td>body</td><td>string</td><td>true</td><td>none</td></tr><tr><td>» type</td><td>body</td><td>string</td><td>false</td><td>none</td></tr></tbody></table>

### Responses <a href="#post__messaging_sign-responses" id="post__messaging_sign-responses"></a>

<table data-full-width="false"><thead><tr><th width="123">Status</th><th width="172">Meaning</th><th width="457">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Message has been signed</td><td><a href="index.html.md#schemaresponse">Response</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>Message failed to sign</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.2">Payment Required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>DID was not found</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /messaging/sign REQUEST CURL</summary>

```bash
# You can also use wget
curl -X POST https://api-testnet.dock.io/messaging/sign \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>Body parameter</summary>

```json
{
  "payload": {},
  "senderDid": "string",
  "type": "string"
}
```

</details>

<details>

<summary>200 Response</summary>

```
"eyJhRU...p6byJ9.eyJpZ...em8iXV19.RIHJunaOq0SnQqYjG...BXo4ozHjWAMfqR0czB0rR4emWF0MeWOCXXSJra4ttCFAQ"
```

</details>

## Verifying a Message

Verify that the message is valid.

### Parameters <a href="#post__messaging_verify-parameters" id="post__messaging_verify-parameters"></a>

<table data-full-width="false"><thead><tr><th width="112">Name</th><th width="88">In</th><th width="110">Type</th><th width="135">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>The message payload</td></tr><tr><td>» jws</td><td>body</td><td>string</td><td>true</td><td>none</td></tr></tbody></table>

### Responses <a href="#post__messaging_verify-responses" id="post__messaging_verify-responses"></a>

<table data-full-width="false"><thead><tr><th width="127">Status</th><th width="176">Meaning</th><th width="276">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Message is verified</td><td><a href="index.html.md#schemaresponse">Response</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>Message failed to verify</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.2">Payment Required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>DID was not found</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /messaging/verify REQUEST CURL</summary>

```bash
# You can also use wget
curl -X POST https://api-testnet.dock.io/messaging/verify \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'
```

</details>

<details>

<summary>Body parameter</summary>

```json
{
  "jws": "string"
}
```

</details>

<details>

<summary>200 Response</summary>

```json
{
	"verified": true,
	"payload": {
		"id": "14a31880-e864-11ed-ab4c-3f9fbca4f00d",
		"type": "https://example.com/protocols/lets_do_lunch/1.0/proposal",
		"created_time": 1682975205,
		"from": "did:example:alice",
		"body": {
			"some": "test-value"
		},
		"reply_to": [
			[
				"did:example:alice"
			]
		]
	}
}
```

</details>

## Send Message

Sends a DIDComm message using our relay service and DID service endpoints, it also returns a URL for QR code scanning. Supports encrypted, plaintext and signed DIDComm messages. You can generate an encrypted DIDComm message by calling the `/messaging/encrypt` route.

The `typ` attribute must be a DIDComm type (i.e. starts with "application/didcomm").

### Parameters <a href="#post__messaging_send-parameters" id="post__messaging_send-parameters"></a>

<table data-full-width="false"><thead><tr><th width="134">Name</th><th width="83">In</th><th width="107">Type</th><th width="116">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>The message payload</td></tr><tr><td>» to</td><td>body</td><td>string</td><td>true</td><td>none</td></tr><tr><td>» message</td><td>body</td><td>Message</td><td>true</td><td>none</td></tr></tbody></table>

### Responses <a href="#post__messaging_send-responses" id="post__messaging_send-responses"></a>

<table data-full-width="false"><thead><tr><th width="113">Status</th><th width="174">Meaning</th><th width="286">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Message has been sent</td><td><a href="index.html.md#schemaresponse">Response</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>Message failed to send</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.2">Payment Required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>DID was not found</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /messaging/send REQUEST CURL</summary>

```bash
# You can also use wget
curl -X POST https://api-testnet.dock.io/messaging/send \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>Body parameter</summary>

```json
{
  "to": "string",
  "message": {
    "typ": "string"
  }
}
```

</details>

<details>

<summary>200 Response</summary>

```json
{
	"sent": true,
	"qrUrl": "didcomm://https://relay.dock.io/read/64502e3243455b67f93f95557"
}
```

</details>
