# API Documentation



###

Sub-Accounts

Sub-accounts are a feature of the Dock Certs API that allows Dock enterprise customers to segregate their data within Dock's platform based on their own customers. Each sub-account can have its own keys, organization profiles, credential designs and verification templates conviently organized to help with tracking and auditing of the activity performed by each.

When using a sub-account the root account can set up separate API keys for each sub-account. By using the sub-account specific API key it will ensure all the transactions are attributed to that sub-account.

![Sub-accounts diagram](../.gitbook/assets/sub-accounts.png)

### Create Sub-Account

> POST /subaccounts REQUEST

```shell

curl -X POST https://api-testnet.dock.io/subaccounts \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

```json
{
  "name": "string",
  "image": "string"
}
```

#### Parameters <a href="#post__subaccounts-parameters" id="post__subaccounts-parameters"></a>

| Name    | In   | Type   | Required | Description           |
| ------- | ---- | ------ | -------- | --------------------- |
| body    | body | object | true     | Subaccount object     |
| » name  | body | string | true     | The sub account name  |
| » image | body | string | false    | The sub account image |

> Example responses

> 200 Response

```json
{
  "id": 0,
  "name": "string",
  "email": "string",
  "image": "string"
}
```

#### Responses <a href="#post__subaccounts-responses" id="post__subaccounts-responses"></a>

| Status | Meaning                                                               | Description                                              | Schema                                       |
| ------ | --------------------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Subaccount has been created                              | [Subaccount](index.html.md#schemasubaccount) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)      | Error creating subaccount                                | [Error](index.html.md#schemaerror)           |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed | [Error](index.html.md#schemaerror)           |

### List Sub-Accounts

> GET /subaccounts REQUEST

> Code samples

```shell

curl -X GET https://api-testnet.dock.io/subaccounts \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

#### Parameters <a href="#get__subaccounts-parameters" id="get__subaccounts-parameters"></a>

| Name   | In    | Type           | Required | Description                                   |
| ------ | ----- | -------------- | -------- | --------------------------------------------- |
| offset | query | integer(int32) | false    | How many items to offset by for pagination    |
| limit  | query | integer(int32) | false    | How many items to return at one time (max 64) |

> Example responses

> 200 Response

```json
[
  {
    "id": 0,
    "name": "string",
    "email": "string",
    "image": "string"
  }
]
```

#### Responses <a href="#get__subaccounts-responses" id="get__subaccounts-responses"></a>

| Status | Meaning                                                 | Description                  | Schema                                         |
| ------ | ------------------------------------------------------- | ---------------------------- | ---------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | A paged array of subaccounts | [Subaccounts](index.html.md#schemasubaccounts) |

### Get Sub-Account by ID

> GET /subaccounts/{id} REQUEST

> Code samples

```shell

curl -X GET https://api-testnet.dock.io/subaccounts/{id} \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

#### Parameters <a href="#get__subaccounts_-id-parameters" id="get__subaccounts_-id-parameters"></a>

| Name | In   | Type   | Required | Description |
| ---- | ---- | ------ | -------- | ----------- |
| id   | path | string | true     | An ID       |

> Example responses

> 200 Response

```json
{
  "id": 0,
  "name": "string",
  "email": "string",
  "image": "string"
}
```

#### Responses <a href="#get__subaccounts_-id-responses" id="get__subaccounts_-id-responses"></a>

| Status | Meaning                                                          | Description                          | Schema                                       |
| ------ | ---------------------------------------------------------------- | ------------------------------------ | -------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)          | Expected response to a valid request | [Subaccount](index.html.md#schemasubaccount) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) | Error getting subaccount             | [Error](index.html.md#schemaerror)           |
| 401    | [Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)  | You do not own this subaccount       | [Error](index.html.md#schemaerror)           |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)   | Subaccount was not found             | [Error](index.html.md#schemaerror)           |

> PATCH /subaccounts/{id} REQUEST

Update the specified sub-account.

> Code samples

```shell

curl -X PATCH https://api-testnet.dock.io/subaccounts/{id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

```json
{
  "name": "string",
  "image": "string"
}
```

#### Parameters <a href="#patch__subaccounts_-id-parameters" id="patch__subaccounts_-id-parameters"></a>

| Name    | In   | Type   | Required | Description           |
| ------- | ---- | ------ | -------- | --------------------- |
| id      | path | string | true     | An ID                 |
| body    | body | object | true     | Subaccount properties |
| » name  | body | string | true     | The sub account name  |
| » image | body | string | false    | The sub account image |

> Example responses

> 200 Response

```json
{
  "id": 0,
  "name": "string",
  "email": "string",
  "image": "string"
}
```

#### Responses <a href="#patch__subaccounts_-id-responses" id="patch__subaccounts_-id-responses"></a>

| Status | Meaning                                                               | Description                                              | Schema                                       |
| ------ | --------------------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Subaccount has been updated                              | [Subaccount](index.html.md#schemasubaccount) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)      | Error creating subaccount                                | [Error](index.html.md#schemaerror)           |
| 401    | [Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)       | You do not own this subaccount                           | [Error](index.html.md#schemaerror)           |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed | [Error](index.html.md#schemaerror)           |

> DELETE /subaccounts/{id} REQUEST

Deletes the specified sub-account.

> Code samples

```shell

curl -X DELETE https://api-testnet.dock.io/subaccounts/{id} \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

#### Parameters <a href="#delete__subaccounts_-id-parameters" id="delete__subaccounts_-id-parameters"></a>

| Name | In   | Type   | Required | Description |
| ---- | ---- | ------ | -------- | ----------- |
| id   | path | string | true     | An ID       |

> Example responses

> 400 Response

```json
{
  "status": 0,
  "type": "string",
  "message": "string"
}
```

#### Responses <a href="#delete__subaccounts_-id-responses" id="delete__subaccounts_-id-responses"></a>

| Status | Meaning                                                          | Description                    | Schema                             |
| ------ | ---------------------------------------------------------------- | ------------------------------ | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)          | Subaccount deleted             | None                               |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) | Error deleting subaccount      | [Error](index.html.md#schemaerror) |
| 401    | [Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)  | You do not own this subaccount | [Error](index.html.md#schemaerror) |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)   | Subaccount was not found       | [Error](index.html.md#schemaerror) |

### Get Sub-Account Usage

> GET /subaccounts/{id}/usage REQUEST

Get details about the activity that this sub-account has performed against the system.

> Code samples

```shell

curl -X GET https://api-testnet.dock.io/subaccounts/{id}/usage \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

#### Parameters <a href="#get__subaccounts_-id-_usage-parameters" id="get__subaccounts_-id-_usage-parameters"></a>

| Name      | In    | Type              | Required | Description                                     |
| --------- | ----- | ----------------- | -------- | ----------------------------------------------- |
| id        | path  | string            | true     | An ID                                           |
| startTime | query | string(date-time) | false    | Timestamp for the start of the range (ISO 8601) |
| endTime   | query | string(date-time) | false    | Timestamp for the end of the range (ISO 8601)   |
| offset    | query | integer(int32)    | false    | How many items to offset by for pagination      |
| limit     | query | integer(int32)    | false    | How many items to return at one time (max 64)   |

> Example responses

> 200 Response

```json
[
  {}
]
```

#### Responses <a href="#get__subaccounts_-id-_usage-responses" id="get__subaccounts_-id-_usage-responses"></a>

| Status | Meaning                                                         | Description                                            | Schema                                             |
| ------ | --------------------------------------------------------------- | ------------------------------------------------------ | -------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)         | A paged array of subaccount transaction usage metadata | [ArrayResponse](index.html.md#schemaarrayresponse) |
| 401    | [Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1) | You do not own this subaccount                         | [Error](index.html.md#schemaerror)                 |

### Create Sub-Account API Key

> POST /subaccounts/{id}/keys REQUEST

Creates an API key for a subaccount. In order for activity to be associated with the given sub-account an API key needs to be created for that sub-account and then that key must be used for all transactions related to that sub-account.

> Code samples

```shell

curl -X POST https://api-testnet.dock.io/subaccounts/{id}/keys \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

```json
{}
```

#### Parameters <a href="#post__subaccounts_-id-_keys-parameters" id="post__subaccounts_-id-_keys-parameters"></a>

| Name | In   | Type   | Required | Description           |
| ---- | ---- | ------ | -------- | --------------------- |
| id   | path | string | true     | An ID                 |
| body | body | object | false    | Subaccount properties |

> Example responses

> 200 Response

```json
{
  "code": 0
}
```

#### Responses <a href="#post__subaccounts_-id-_keys-responses" id="post__subaccounts_-id-_keys-responses"></a>

| Status | Meaning                                                               | Description                                              | Schema                                   |
| ------ | --------------------------------------------------------------------- | -------------------------------------------------------- | ---------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Subaccount API key created                               | [Response](index.html.md#schemaresponse) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)      | Error creating subaccount API key                        | [Error](index.html.md#schemaerror)       |
| 401    | [Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)       | You do not own this subaccount                           | [Error](index.html.md#schemaerror)       |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed | [Error](index.html.md#schemaerror)       |

### List Sub-Account API Keys

> GET /subaccounts/{id}/keys REQUEST

> Code samples

```shell

curl -X GET https://api-testnet.dock.io/subaccounts/{id}/keys \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

#### Parameters <a href="#get__subaccounts_-id-_keys-parameters" id="get__subaccounts_-id-_keys-parameters"></a>

| Name   | In    | Type           | Required | Description                                   |
| ------ | ----- | -------------- | -------- | --------------------------------------------- |
| id     | path  | string         | true     | An ID                                         |
| offset | query | integer(int32) | false    | How many items to offset by for pagination    |
| limit  | query | integer(int32) | false    | How many items to return at one time (max 64) |

> Example responses

> 200 Response

```json
[
  {}
]
```

#### Responses <a href="#get__subaccounts_-id-_keys-responses" id="get__subaccounts_-id-_keys-responses"></a>

| Status | Meaning                                                         | Description                              | Schema                                             |
| ------ | --------------------------------------------------------------- | ---------------------------------------- | -------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)         | A paged array of subaccount key metadata | [ArrayResponse](index.html.md#schemaarrayresponse) |
| 401    | [Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1) | You do not own this subaccount           | [Error](index.html.md#schemaerror)                 |

### Delete a Sub-Account API Key

> DELETE /subaccounts/{id}/keys/{keyId} REQUEST

Delete the specified API key for the given sub-account.

> Code samples

```shell

curl -X DELETE https://api-testnet.dock.io/subaccounts/{id}/keys/{keyId} \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

#### Parameters <a href="#delete__subaccounts_-id-_keys_-keyid-parameters" id="delete__subaccounts_-id-_keys_-keyid-parameters"></a>

| Name  | In   | Type   | Required | Description   |
| ----- | ---- | ------ | -------- | ------------- |
| id    | path | string | true     | An ID         |
| keyId | path | string | true     | An API key ID |

> Example responses

> 400 Response

```json
{
  "status": 0,
  "type": "string",
  "message": "string"
}
```

#### Responses <a href="#delete__subaccounts_-id-_keys_-keyid-responses" id="delete__subaccounts_-id-_keys_-keyid-responses"></a>

| Status | Meaning                                                          | Description                       | Schema                             |
| ------ | ---------------------------------------------------------------- | --------------------------------- | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)          | Subaccount API key deleted        | None                               |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) | Error deleting subaccount API key | [Error](index.html.md#schemaerror) |
| 401    | [Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)  | You do not own this subaccount    | [Error](index.html.md#schemaerror) |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)   | Subaccount API key was not found  | [Error](index.html.md#schemaerror) |

## Messaging <a href="#dock-api-messaging" id="dock-api-messaging"></a>

Operations about DIDComm messaging. DIDComm messages are addressed by DID using Dock's relay service.

The current most common use case for the messaging service is to send credentials and presentation requests to the Dock Wallet, but other clients can use it too.

### Encrypt Message

> POST /messaging/encrypt REQUEST

In most cases you'll want to ensure the privacy of the message by encrypting it before sending.

> Code samples

```shell
# You can also use wget
curl -X POST https://api-testnet.dock.io/messaging/encrypt \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

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

#### Parameters <a href="#post__messaging_encrypt-parameters" id="post__messaging_encrypt-parameters"></a>

| Name            | In   | Type     | Required | Description                        |
| --------------- | ---- | -------- | -------- | ---------------------------------- |
| body            | body | object   | true     | The recipients, sender and message |
| » type          | body | string   | false    | none                               |
| » payload       | body | object   | true     | none                               |
| » senderDid     | body | string   | true     | none                               |
| » algorithm     | body | string   | false    | none                               |
| » recipientDids | body | \[oneOf] | true     | none                               |

**Enumerated Values**

| Parameter   | Value           |
| ----------- | --------------- |
| » algorithm | ECDH-1PU+A256KW |
| » algorithm | ECDH-ES+A256KW  |

> Example responses

> 200 Response

```json
{
  "code": 0
}
```

#### Responses <a href="#post__messaging_encrypt-responses" id="post__messaging_encrypt-responses"></a>

| Status | Meaning                                                               | Description                                                        | Schema                                   |
| ------ | --------------------------------------------------------------------- | ------------------------------------------------------------------ | ---------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Message has been encrypted, returning an encrypted DIDComm Message | [Response](index.html.md#schemaresponse) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)      | Message failed to encrypt                                          | [Error](index.html.md#schemaerror)       |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed           | [Error](index.html.md#schemaerror)       |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)        | DID was not found                                                  | [Error](index.html.md#schemaerror)       |

### Decrypt Message

> POST /messaging/decrypt REQUEST

> Code samples

```shell
# You can also use wget
curl -X POST https://api-testnet.dock.io/messaging/decrypt \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

```json
{
  "jwe": {}
}
```

#### Parameters <a href="#post__messaging_decrypt-parameters" id="post__messaging_decrypt-parameters"></a>

| Name  | In   | Type   | Required | Description |
| ----- | ---- | ------ | -------- | ----------- |
| body  | body | object | true     | The JWM     |
| » jwe | body | object | true     | none        |

> Example responses

> 200 Response

```json
{
  "code": 0
}
```

#### Responses <a href="#post__messaging_decrypt-responses" id="post__messaging_decrypt-responses"></a>

| Status | Meaning                                                               | Description                                              | Schema                                   |
| ------ | --------------------------------------------------------------------- | -------------------------------------------------------- | ---------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Message has been decrypted, returning a DIDComm message  | [Response](index.html.md#schemaresponse) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)      | Message failed to decrypt                                | [Error](index.html.md#schemaerror)       |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed | [Error](index.html.md#schemaerror)       |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)        | DID was not found                                        | [Error](index.html.md#schemaerror)       |

### Signing Messages

> POST /messaging/sign REQUEST

Signing a message helps to prove to the recipient that the message is valid and unaltered. The message will be signed as a Base64 encoded JWT.

> Code samples

```shell
# You can also use wget
curl -X POST https://api-testnet.dock.io/messaging/sign \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

```json
{
  "payload": {},
  "senderDid": "string",
  "type": "string"
}
```

#### Parameters <a href="#post__messaging_sign-parameters" id="post__messaging_sign-parameters"></a>

| Name        | In   | Type   | Required | Description         |
| ----------- | ---- | ------ | -------- | ------------------- |
| body        | body | object | true     | The message payload |
| » payload   | body | object | true     | none                |
| » senderDid | body | string | true     | none                |
| » type      | body | string | false    | none                |

> Example responses

> 200 Response

```
"eyJhRU...p6byJ9.eyJpZ...em8iXV19.RIHJunaOq0SnQqYjG...BXo4ozHjWAMfqR0czB0rR4emWF0MeWOCXXSJra4ttCFAQ"
```

#### Responses <a href="#post__messaging_sign-responses" id="post__messaging_sign-responses"></a>

| Status | Meaning                                                               | Description                                              | Schema                                   |
| ------ | --------------------------------------------------------------------- | -------------------------------------------------------- | ---------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Message has been signed                                  | [Response](index.html.md#schemaresponse) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)      | Message failed to sign                                   | [Error](index.html.md#schemaerror)       |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed | [Error](index.html.md#schemaerror)       |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)        | DID was not found                                        | [Error](index.html.md#schemaerror)       |

### Verifying a Message

> POST /messaging/verify REQUEST

Verify that the message is valid.

> Code samples

```shell
# You can also use wget
curl -X POST https://api-testnet.dock.io/messaging/verify \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

```json
{
  "jws": "string"
}
```

#### Parameters <a href="#post__messaging_verify-parameters" id="post__messaging_verify-parameters"></a>

| Name  | In   | Type   | Required | Description         |
| ----- | ---- | ------ | -------- | ------------------- |
| body  | body | object | true     | The message payload |
| » jws | body | string | true     | none                |

> Example responses

> 200 Response

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

#### Responses <a href="#post__messaging_verify-responses" id="post__messaging_verify-responses"></a>

| Status | Meaning                                                               | Description                                              | Schema                                   |
| ------ | --------------------------------------------------------------------- | -------------------------------------------------------- | ---------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Message is verified                                      | [Response](index.html.md#schemaresponse) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)      | Message failed to verify                                 | [Error](index.html.md#schemaerror)       |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed | [Error](index.html.md#schemaerror)       |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)        | DID was not found                                        | [Error](index.html.md#schemaerror)       |

### Send Message

> POST /messaging/send REQUEST

Sends a DIDComm message using our relay service and DID service endpoints, it also returns a URL for QR code scanning. Supports encrypted, plaintext and signed DIDComm messages. You can generate an encrypted DIDComm message by calling the `/messaging/encrypt` route.

The `typ` attribute must be a DIDComm type (i.e. starts with "application/didcomm").

> Code samples

```shell
# You can also use wget
curl -X POST https://api-testnet.dock.io/messaging/send \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

```json
{
  "to": "string",
  "message": {
    "typ": "string"
  }
}
```

#### Parameters <a href="#post__messaging_send-parameters" id="post__messaging_send-parameters"></a>

| Name      | In   | Type    | Required | Description         |
| --------- | ---- | ------- | -------- | ------------------- |
| body      | body | object  | true     | The message payload |
| » to      | body | string  | true     | none                |
| » message | body | Message | true     | none                |

> Example responses

> 200 Response

```json
{
	"sent": true,
	"qrUrl": "didcomm://https://relay.dock.io/read/64502e3243455b67f93f95557"
}
```

#### Responses <a href="#post__messaging_send-responses" id="post__messaging_send-responses"></a>

| Status | Meaning                                                               | Description                                              | Schema                                   |
| ------ | --------------------------------------------------------------------- | -------------------------------------------------------- | ---------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Message has been sent                                    | [Response](index.html.md#schemaresponse) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)      | Message failed to send                                   | [Error](index.html.md#schemaerror)       |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed | [Error](index.html.md#schemaerror)       |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)        | DID was not found                                        | [Error](index.html.md#schemaerror)       |

## Schemas <a href="#dock-api-schemas" id="dock-api-schemas"></a>

> Object Schemas

Data Schemas are useful when enforcing a specific structure on a collection of data like a Verifiable Credential. Other than that, Data Verification schema and Data Encoding Schemas are used to verify and map the structure and contents of a Verifiable Credential.

These are the schemas used in all API operations mentioned before, such as Error, Credential, Jobs, Anchor, Registry, and so on.

For a detailed example of the schema workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/schemaFlow.js).

### Error <a href="#tocs_error" id="tocs_error"></a>

```json
{
  "status": 0,
  "type": "string",
  "message": "string"
}

```

This is a schema for an API Error.

#### Properties

| Name    | Type    | Required | Description           |
| ------- | ------- | -------- | --------------------- |
| status  | integer | false    | Status of the error.  |
| type    | string  | false    | Type of the error.    |
| message | string  | false    | Message of the error. |

### Hex32 <a href="#tocs_hex32" id="tocs_hex32"></a>

```json
"string"

```

32 byte hex string. Ignoring higher base (base64) for simplicity.

#### Properties

| Name  | Type   | Required | Description                                                       |
| ----- | ------ | -------- | ----------------------------------------------------------------- |
| Hex32 | string | false    | 32 byte hex string. Ignoring higher base (base64) for simplicity. |

### JobStartedResult <a href="#tocs_jobstartedresult" id="tocs_jobstartedresult"></a>

```json
{
  "id": "string",
  "data": {
    "did": "did:dock:xyz",
    "hexDid": "0x00",
  }
}

```

Object containing unique id of the background task and associated data. This id can be used to query the job status.

#### Properties

| Name | Type                               | Description                                                                    |
| ---- | ---------------------------------- | ------------------------------------------------------------------------------ |
| id   | [JobId](index.html.md#schemajobid) | Unique id of the background task. This id can be used to query the job status. |
| data | object                             | Data of the object.                                                            |

### JobId <a href="#tocs_jobid" id="tocs_jobid"></a>

```json
"string"

```

Unique id of the background task. This id can be used to query the job status

### JobStatus <a href="#tocs_jobstatus" id="tocs_jobstatus"></a>

```json
"in_progress"

```

This is a schema used in Job operation to get a status of the job.

#### Enumerated Values

| Property  | Value                                                   | Description          |
| --------- | ------------------------------------------------------- | -------------------- |
| JobStatus | todo **or** finalized **or** in\_progress **or** error. | Job Status variants. |

### JobDesc <a href="#tocs_jobdesc" id="tocs_jobdesc"></a>

```json
{
  "id": "string",
  "result": {},
  "status": "todo",

}

```

This is a schema used in Job operation to get description of the job including the result if it is available.

#### Properties

| Name   | Type                                       | Description                                                                    |
| ------ | ------------------------------------------ | ------------------------------------------------------------------------------ |
| id     | [JobId](index.html.md#schemajobid)         | Unique id of the background task. This id can be used to query the job status. |
| status | [JobStatus](index.html.md#schemajobstatus) | Status of the job.                                                             |
| result | object                                     | false                                                                          |

### DIDDock <a href="#tocs_diddock" id="tocs_diddock"></a>

```json
"did:dock:xyz"

```

DID as fully qualified, e.g., `did:dock:`.

#### Properties

| Name | Type   | Required | Description                                                                                                           |
| ---- | ------ | -------- | --------------------------------------------------------------------------------------------------------------------- |
| DID  | string | false    | DID as fully qualified, e.g., `did:dock:`. You cannot specify your own DID, the DID value will be randomly generated. |

### KeyType <a href="#tocs_keytype" id="tocs_keytype"></a>

```json
"sr25519"

```

This is a schema type of public key for DID.

#### Enumerated Values

| Property | Value                                   | Description           |
| -------- | --------------------------------------- | --------------------- |
| KeyType  | sr25519 **or** ed25519 **or** secp256k1 | keyType DID variants. |

### SigType <a href="#tocs_sigtype" id="tocs_sigtype"></a>

```json
"Sr25519Signature2020"

```

This is a schema used in Presentation operation that represents a type of signature.

#### Enumerated Values

| Property | Value                                                                               | Description                 |
| -------- | ----------------------------------------------------------------------------------- | --------------------------- |
| SigType  | Sr25519Signature2020 **or** Ed25519Signature2018 **or** EcdsaSecp256k1Signature2019 | SigType signature variants. |

### ProofPurpose <a href="#tocs_proofpurpose" id="tocs_proofpurpose"></a>

```json
"assertionMethod"

```

This is a schema that represents a purpose of credential.

#### Enumerated Values

| Property     | Value                                 | Description            |
| ------------ | ------------------------------------- | ---------------------- |
| ProofPurpose | assertionMethod **or** authentication | Purpose of credential. |

### Context <a href="#tocs_context" id="tocs_context"></a>

```json
[
  "string"
]

```

This is a schema that represents a JSON-LD context used in DID and Presentation.

### DIDDoc <a href="#tocs_diddoc" id="tocs_diddoc"></a>

```json
{
  "@context": [
    "string"
  ],
  "id": "did:dock:xyz",
  "authentication": [
    {}
  ]
}

```

This is a schema that represents a DID document. The current set of properties is incomplete

#### Properties

| Name           | Type                                   | Required | Description                                |
| -------------- | -------------------------------------- | -------- | ------------------------------------------ |
| @context       | [Context](index.html.md#schemacontext) | false    | JSON-LD context.                           |
| id             | [DIDDock](index.html.md#schemadiddock) | false    | DID as fully qualified, e.g., `did:dock:`. |
| authentication | array                                  | false    | DID authentication.                        |

### Credential <a href="#tocs_credential" id="tocs_credential"></a>

```json
{
  "context": [
    "string"
  ],
  "type": [
    "string"
  ],
  "subject": {},
  "issuer": "did:dock:xyz",
  "issuanceDate": "2019-08-24T14:15:22Z",
  "expirationDate": "2019-08-24T14:15:22Z",
  "status": "90b7dc6e8642bf1425c5a5ef2c3ff62bb689770843fdc0e2d79b97beb6c73311"
}

```

This is a schema that represents a credential format expected by API caller when issuing a credential.

#### Properties

| Name           | Type                                   | Required | Description                                                                                                                                                                                                                                                                    |
| -------------- | -------------------------------------- | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| id             | string(uri)                            | false    | Credential ID. The default value is a creds.dock.io uri with random ID.                                                                                                                                                                                                        |
| context        | \[string or object]                    | false    | Credential context array of string URIs and/or embedded JSON-LD context objects. If no context parameter is supplied, we will auto generate contexts for you. If you do supply this parameter, you must ensure that all JSON-LD terms are defined. This is for advanced users. |
| type           | \[string]                              | false    | Credential type. The default value is \['VerifiableCredential']                                                                                                                                                                                                                |
| subject        | object or \[object]                    | true     | Credential subject or subjects array.                                                                                                                                                                                                                                          |
| schema         | string                                 | false    | Schema ID returned by create schema route or a valid URI                                                                                                                                                                                                                       |
| issuer         | [DIDDock](index.html.md#schemadiddock) | false    | Credential issuer. DID as fully qualified, e.g., `did:dock:`. If not supplied the credential will not be signed.                                                                                                                                                               |
| issuanceDate   | string(date-time\[RFC3339])            | false    | The date and time in GMT that the credential was issued specified in RFC 3339 format. The issuanceDate will be automatically set if not provided.                                                                                                                              |
| expirationDate | string(date-time\[RFC3339])            | false    | The date and time in GMT that the credential expired is specified in RFC 3339 format. The default value of the expirationDate will be empty if the user does not provide it.                                                                                                   |
| status         | object or string                       | false    | Revocation registry id or user supplied status object containg a Dock revocation registry identifier.                                                                                                                                                                          |

### VerifiablePresentation <a href="#tocs_verifiablepresentation" id="tocs_verifiablepresentation"></a>

```json
{
  "@context": [
    "string"
  ],
  "id": "http://example.com",
  "type": [
    "string"
  ],
  "verifiableCredential": {
    "@context": [
      "string"
    ],
    "id": "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb",
    "type": [
      "string"
    ],
    "credentialSubject": {},
    "issuer": "did:dock:xyz",
    "issuanceDate": "2019-08-24T14:15:22Z",
    "expirationDate": "2019-08-24T14:15:22Z",
    "credentialStatus": {},
    "proof": {
      "type": "Sr25519Signature2020",
      "proofPurpose": "assertionMethod",
      "verificationMethod": "string",
      "created": "2019-08-24T14:15:22Z",
      "proofValue": "string"
    }
  },
  "proof": {
    "type": "Sr25519Signature2020",
    "proofPurpose": "assertionMethod",
    "verificationMethod": "string",
    "created": "2019-08-24T14:15:22Z",
    "proofValue": "string"
  }
}

```

This is a schema that represents a Verifiable (signed) Presentation returned by API. The current set of properties is almost complete

#### Properties

| Name                 | Type                                                             | Required | Description                                                                                       |
| -------------------- | ---------------------------------------------------------------- | -------- | ------------------------------------------------------------------------------------------------- |
| @context             | [Context](index.html.md#schemacontext)                           | true     | JSON-LD context.                                                                                  |
| id                   | string(uri)                                                      | true     | Verifiable (signed) presentation id.                                                              |
| type                 | string                                                           | true     | Verifiable (signed) presentation type.                                                            |
| verifiableCredential | [VerifiableCredential](index.html.md#schemaverifiablecredential) | true     | Verifiable (signed) Credential returned by API. The current set of properties is almost complete. |
| proof                | object                                                           | true     | Proof of credential.                                                                              |

#### Child Properties of Proof <a href="#proofchildpropertiespresentation" id="proofchildpropertiespresentation"></a>

| Name               | Type                                             | Required | Description                                                                            |
| ------------------ | ------------------------------------------------ | -------- | -------------------------------------------------------------------------------------- |
| type               | [SigType](index.html.md#schemasigtype)           | true     | Type of signature.                                                                     |
| proofPurpose       | [ProofPurpose](index.html.md#schemaproofpurpose) | true     | Purpose of credential.                                                                 |
| verificationMethod | string                                           | true     | Verification method.                                                                   |
| created            | string(date-time\[RFC3339])                      | true     | The date and time in GMT that the credential was created specified in RFC 3339 format. |
| proofValue         | string                                           | true     | none                                                                                   |

### VerifiableCredential <a href="#tocs_verifiablecredential" id="tocs_verifiablecredential"></a>

```json
{
  "@context": [
    "string"
  ],
  "id": "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb",
  "type": [
    "string"
  ],
  "credentialSubject": {},
  "issuer": "did:dock:xyz",
  "issuanceDate": "2019-08-24T14:15:22Z",
  "expirationDate": "2019-08-24T14:15:22Z",
  "credentialStatus": {},
  "proof": {
    "type": "Sr25519Signature2020",
    "proofPurpose": "assertionMethod",
    "verificationMethod": "string",
    "created": "2019-08-24T14:15:22Z",
    "proofValue": "string"
  }
}

```

This is a schema that represents a verifiable (signed) Credential returned by API. The current set of properties is almost complete.

#### Properties

| Name              | Type                                   | Required | Description                                                                                                                                                                  |
| ----------------- | -------------------------------------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| @context          | [Context](index.html.md#schemacontext) | false    | JSON-LD context.                                                                                                                                                             |
| id                | string(uri)                            | false    | Credential id.                                                                                                                                                               |
| type              | \[string]                              | false    | Credential type.                                                                                                                                                             |
| credentialSubject | any                                    | false    | Credential subject.                                                                                                                                                          |
| issuer            | [DIDDock](index.html.md#schemadiddock) | false    | Credential issuer or DID as fully qualified, e.g., `did:dock:`.                                                                                                              |
| issuanceDate      | string(date-time\[RFC3339])            | false    | The date and time in GMT that the credential was issued specified in RFC 3339 format. The issuanceDate will be automatically set if not provided.                            |
| expirationDate    | string(date-time\[RFC3339])            | false    | The date and time in GMT that the credential expired is specified in RFC 3339 format. The default value of the expirationDate will be empty if the user does not provide it. |
| credentialStatus  | any                                    | false    | Revocation registry id or user supplied status object.                                                                                                                       |
| proof             | object                                 | false    | Proof of credential.                                                                                                                                                         |

#### Child Properties of Proof <a href="#proofchildpropertiescredentials" id="proofchildpropertiescredentials"></a>

| Name               | Type                                             | Required | Description                                                                            |
| ------------------ | ------------------------------------------------ | -------- | -------------------------------------------------------------------------------------- |
| type               | [SigType](index.html.md#schemasigtype)           | false    | Type of signature.                                                                     |
| proofPurpose       | [ProofPurpose](index.html.md#schemaproofpurpose) | false    | Purpose of credential.                                                                 |
| verificationMethod | string                                           | false    | Verification method.                                                                   |
| created            | string(date-time\[RFC3339])                      | false    | The date and time in GMT that the credential was created specified in RFC 3339 format. |
| proofValue         | string                                           | false    | Value of credential.                                                                   |

### Anchor <a href="#tocs_anchor" id="tocs_anchor"></a>

```json
{
  "type": "single/batch",
  "proofs": [],
  "blockHash": "string",
  "root": "string",
  "created_at": "YYYY-"
}

```

An anchor, either a batched or single is the information that constitutes the credentials' proof of existence. The schema includes anchor, type (single, batch), block hash, block number and accompanying data (root, proofs) if any. It depends if the anchor was created using API or not.

### Registry <a href="#tocs_registry" id="tocs_registry"></a>

```json
{
  "addOnly": true,
  "policy": [
    "did:dock:xyz"
  ]
}

```

This is a schema that represents a Revocation registry used in Revocation or Unrevocation.

#### Properties

| Name    | Type                                      | Required | Description                                                                                                          |
| ------- | ----------------------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------- |
| addOnly | boolean                                   | false    | If the `addOnly` value is true, they cannot unrevoke and delete the registry. The default value for this is `false`. |
| policy  | \[[DIDDock](index.html.md#schemadiddock)] | false    | Only one policy supported as of now called `OneOf`.                                                                  |

### VerificationResponse <a href="#tocs_verificationresponse" id="tocs_verificationresponse"></a>

```json
{
  "verified": true,
  "results": [...]
}

```

This is a schema that is used to define whether a credential/presentation is verified or not

### Response <a href="#tocs_response" id="tocs_response"></a>

```json
{
  "code": 0
}

```

This is a schema that represents a default response for a request made.

### Message <a href="#tocs_message" id="tocs_message"></a>

```json
{
  "to": ["did:example:bob"],
  "ciphertext": "eyJhsad...AQ",
  "typ":"application/didcomm..."
}

```

This is a schema that represents a message send request. If the message is signed or encrypted use the `ciphertext` field. The `typ` field must be a valid DIDComm message type.

{ "@context": "http://schema.org/", "@type": "WebAPI", "description": "Dock provides a complete solution for creating and managing verifiable credentials on the blockchain. This includes a free trial and simple, monthly pricing. Get started here: https://certs.dock.io/ ", "name": "Dock API" }
