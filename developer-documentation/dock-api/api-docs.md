# API Documentation



###

Presentations

The presentation is signed using the holder's private key as it is being created. To validate the presentation, the verifier must also check the issuer's signature and the holder's public key. One way to achieve this is to make the holder have a DID too, so that the verifier can look up the DID on the chain and learn the public key.

The API allows you to create and sign a verifiable presentation out of one or more Verifiable Credentials.

For a detailed example of the presentations workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/presentationsFlow.js).

### Create Presentation <a href="#create-a-presentation" id="create-a-presentation"></a>

> POST /presentations REQUEST

```shell
curl --location --request POST https://api.dock.io/presentations/ \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
  "holder": "did:dock:xyz",
  "challenge": "string",
  "domain": "string",
  "credentials": [
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
  ]
}'

```

```json-doc

{
  "holder": "did:dock:xyz",
  "challenge": "string",
  "domain": "string",
  "credentials": [
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
  ]
}
```

The holder while creating the presentation signs it with his private key. For the verifier to verify the presentation, in addition to verifying the issuer's signature, he/she needs to verify this signature as well, and for that he must know the holder's public key.

This is an operation to create and sign a verifiable presentation out of one or more Verifiable Credentials.

#### Parameters <a href="#create-a-presentation-parameters" id="create-a-presentation-parameters"></a>

| Name        | In   | Type                                                             | Required | Description                                                                                                                                                                                                                                                       |
| ----------- | ---- | ---------------------------------------------------------------- | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| holder      | body | [DIDDock](index.html.md#schemadiddock)                           | true     | DID as fully qualified, e.g., `did:dock:xyz`.                                                                                                                                                                                                                     |
| challenge   | body | string                                                           | false    | Presentation's Challenge in a string format. The default value for this is `random hex string`. NOTE: if this presentation is being created to respond to a `proof-request` the challenge should be set to the value from the `nonce` field in the proof-request. |
| domain      | body | string                                                           | false    | A domain for the proof in a string format. The default value for the domain is `dock.io`.                                                                                                                                                                         |
| credentials | body | [VerifiableCredential](index.html.md#schemaverifiablecredential) | false    | Verifiable (signed) Credential returned by API.                                                                                                                                                                                                                   |

#### Enumerated Values

| Parameter    | Value                                                                               | Description                                  |
| ------------ | ----------------------------------------------------------------------------------- | -------------------------------------------- |
| type         | Sr25519Signature2020 **or** Ed25519Signature2018 **or** EcdsaSecp256k1Signature2019 | Type of Signature.                           |
| proofPurpose | assertionMethod **or** authentication                                               | The purpose the credential will be used for. |

> 200 Response

```json
{

  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "urn:uuid:3978344f-8596-4c3a-a978-8fcaba3903c5",
  "type": ["VerifiablePresentation", "CredentialManagerPresentation"],
  "verifiableCredential": [{  }],
  "proof": [{  }]
}
```

#### Responses <a href="#create-a-presentation-responses" id="create-a-presentation-responses"></a>

| Status | Meaning                                                                          | Description                                                                                             | Schema                                                               |
| ------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and returns a Verifiable Presentation.                                       | [VerifiablePresentation](index.html.md#schemaverifiablepresentation) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)                 | The request was unsuccessful, because of invalid/insufficient parameters.                               | [Error](index.html.md#schemaerror)                                   |
| 401    | [Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)                  | The request was unsuccessful, either because of a missing/invalid auth header or you don't own the DID. | [Error](index.html.md#schemaerror)                                   |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                                                | [Error](index.html.md#schemaerror)                                   |

### Create Proof Request <a href="#create-proof-request" id="create-proof-request"></a>

> POST /proof-requests REQUEST

```shell
curl --location --request POST https://api.dock.io/proof-requests/ \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
	"name": "Proof Request Test",
	"purpose": "Prove income",
	"request": {
		"input_descriptors": [
			{
				"id": "ProofIncome-1",
				"name": "Proof Request Test",
				"purpose": "Prove income",
				"constraints": {
					"fields": [
						{
							"path": [
								"$.credentialSubject.id",
								"$.credentialSubject.income.total"
							]
						}
					]
				}
		  ]
    }
	}'

```

```json-doc
{
	"name": "Proof Request Test",
	"purpose": "Prove income",
	"request": {
		"input_descriptors": [
			{
				"id": "ProofIncome-1",
				"name": "Proof Request Test",
				"purpose": "Prove income",
				"constraints": {
					"fields": [
						{
							"path": [
								"$.credentialSubject.id",
								"$.credentialSubject.income.total"
							]
						}
					]
				}
		  ]
    }
	}
```

It often makes sense for a verifier to request proof of credentials from a holder. For this, we have built a proof requests system into the API that works with the Dock Wallet. When a request is created, you will receive a URL which you should display in a QR code for a wallet application to scan. You can define which attributes should exist in the credential, a name for the holder and yourself to see and a nonce/challenge which prevents replay attacks.

Our system supports the [DIF Presentation Exchange (PEX)](https://identity.foundation/presentation-exchange/) syntax for querying and filtering credentials.

See the https://identity.foundation/presentation-exchange/#input-descriptor-extensions for more examples, but a few common use cases are:

#### Require a numeric attribute to be within a range

For example, a verifier might require that the holder have an income between $100,000 and $200,000 per year. This could be requested using the following `input_descriptor`

```
{
  path: ['$.credentialSubject.income.2022.total'],
  filter: {
    type: 'number',
    minimum: 100000,
    maximum: 200000
  },
}
```

#### Require a date attribute to be within a range

For example, a verifier might require that the credential be issued after a certain date. In this example the verifier is requiring that the credential was issued between January 1, 2020 and December 31, 2020.

```
{
  path: ['$.issuanceDate'],
  filter: {
    "type": "string",
    "format": "date",
    "formatMinimum": "2020-01-01",
    "formatMaximum": "2020-12-31"
  },
}
```

#### Parameters <a href="#create-proof-request-parameters" id="create-proof-request-parameters"></a>

| Name       | In   | Type   | Required | Description                                         |
| ---------- | ---- | ------ | -------- | --------------------------------------------------- |
| attributes | body | object | false    | Requested attribute specifications of proof request |
| name       | body | string | false    | Proof request name, will be shown to the holder     |
| nonce      | body | string | false    | Nonce or challenge for the presentation to match    |

> 200 Response

```json
{
  "id": "aeec1776-84c3-4783-b80b-c6690a652892",
  "name": "Proof Request Test",
  "nonce": "1234567890",
  "verified": false,
  "created": "2022-10-17T22:48:30.619Z",
  "updated": "2022-10-17T22:48:30.619Z",
  "presentation": {},
  "response_url": "https://api.dock.io/proof-requests/aeec1776-84c3-4783-b80b-c6690a652892/send-presentation",
  "type": "proof-request",
	"qr": "https://creds-testnet.dock.io/proof/acaae15e-3c6e-412e-951e-4dc129b9745a",
  "request": {
		"input_descriptors": [
			{
				"id": "ProofIncome-1",
				"constraints": {
					"fields": [
						{
							"path": [
								"$.credentialSubject.income.total"
							],
              "filter": {
                "type": "number",
                "minimum": 100000,
                "maximum": 200000
              }
						}
					]
				}
			}
		]
	}
}
```

#### Responses <a href="#create-proof-request-responses" id="create-proof-request-responses"></a>

| Status | Meaning                                                                          | Description                                                                                             | Schema                                                               |
| ------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and returns a Verifiable Presentation.                                       | [VerifiablePresentation](index.html.md#schemaverifiablepresentation) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)                 | The request was unsuccessful, because of invalid/insufficient parameters.                               | [Error](index.html.md#schemaerror)                                   |
| 401    | [Unauthorized](https://tools.ietf.org/html/rfc7235#section-3.1)                  | The request was unsuccessful, either because of a missing/invalid auth header or you don't own the DID. | [Error](index.html.md#schemaerror)                                   |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                                                | [Error](index.html.md#schemaerror)                                   |

### List Proof Requests

> GET /proof-requests REQUEST

```shell
curl --location --request GET https://api.dock.io/proof-requests/ \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw'{

  }'

```

Return a list of all proof requests and their verification status

> 200 Response

```json
[
  {
		"id": "f2ea3225-ef6b-44d7-a37c-7713c66875b5",
		"name": "Proof of Bachelors of Education",
		"nonce": "6684fb3d878f2c3a25e35e36045bde8d",
		"verified": false,
		"created": "2023-04-05T22:00:25.729Z",
		"updated": "2023-04-05T22:00:25.729Z",
		"presentation": {},
		"response_url": "https://api-testnet.dock.io/proof-requests/f2ea3225-ef6b-44d7-a37c-7713c66875b5/send-presentation",
		"type": "proof-request",
		"qr": "https://creds-testnet.dock.io/proof/f2ea3225-ef6b-44d7-a37c-7713c66875b5",
		"request": {
			"input_descriptors": [
				{
					"id": "Credential 1",
					"name": "Proof of Bachelors of Education",
					"purpose": "Prove that the holder has a Bachelors of Education degree",
					"constraints": {
						"fields": [
							{
								"path": [
									"$.credentialSubject.degreeName",
									"$.credentialSubject.degreeType",
									"$.credentialSubject.dateEarned | date: \"%B %d, %Y\"",
									"$.credentialSubject.fullName"
								]
							},
							{
								"path": [
									"$.name"
								],
								"filter": {
									"type": "string",
									"pattern": "Bachelors of Education"
								}
							}
						]
					}
				}
			]
		}
	}
]
```

#### Parameters <a href="#list-proof-requests-parameters" id="list-proof-requests-parameters"></a>

| Name   | In    | Type    | Required | Description                                   |
| ------ | ----- | ------- | -------- | --------------------------------------------- |
| offset | query | integer | false    | How many items to offset by for pagination    |
| limit  | query | integer | false    | How many items to return at one time (max 64) |

#### Responses <a href="#list-proof-requests-responses" id="list-proof-requests-responses"></a>

| Status | Meaning                                                 | Description                                                                        | Schema |
| ------ | ------------------------------------------------------- | ---------------------------------------------------------------------------------- | ------ |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | The request was successful and will return all proof requests created by the user. | Inline |

### Get Proof Request

> GET /proof-requests/{id} REQUEST

```shell
curl --location --request GET https://api.dock.io/proof-requests/{id} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''


```

Get the details of an existing proof request and its verification status

#### Parameters <a href="#get-proof-request-parameters" id="get-proof-request-parameters"></a>

| Name | In   | Type | Required | Description        |
| ---- | ---- | ---- | -------- | ------------------ |
| id   | path | UUID | true     | Proof request UUID |

> 200 Response

```json
{
	"qr": "https://creds-testnet.dock.io/proof/acaae15e-3c6e-412e-951e-4dc129b9745a",
	"id": "fcaae15e-3c6e-412e-951e-4dc129b9745a",
	"name": "Proof Request Test",
	"nonce": "ffa6d005dfd8ddecf1664079bda1af1e",
	"created": "2023-05-16T15:42:53.925Z",
	"updated": "2023-05-16T15:42:53.925Z",
	"verified": false,
	"response_url": "https://api-testnet.dock.io/proof-requests/acaae15e-3c6e-412e-951e-4dc129b9745a/send-presentation",
	"request": {
		"id": "acaae15e-3c6e-412e-951e-4dc129b9745a",
		"input_descriptors": [
			{
				"id": "ProofIncome-1",
				"constraints": {
					"fields": [
						{
							"path": [
								"$.credentialSubject.id",
								"$.credentialSubject.income.total"
							]
						}
					]
				}
			}
		]
	},
	"type": "proof-request"
}
```

#### Responses <a href="#get-proof-request-responses" id="get-proof-request-responses"></a>

| Status | Meaning                                                        | Description                                                            | Schema                                   |
| ------ | -------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)        | The request was successful and will return the proof request.          | [Registry](index.html.md#schemaregistry) |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) | The request was unsuccessful, because the proof request was not found. | [Error](index.html.md#schemaerror)       |

### List Proof Request Templates

> GET /proof-templates REQUEST

When working with Proof Requests you will often want to request the same information from holders. To make this easier you can create Proof Request Templates to define the contents of the proof requests to be re-used.

> Code samples

```shell
# You can also use wget
curl -X GET https://api-testnet.dock.io/proof-templates \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

#### Parameters <a href="#get__proof-templates-parameters" id="get__proof-templates-parameters"></a>

| Name   | In    | Type           | Required | Description                                   |
| ------ | ----- | -------------- | -------- | --------------------------------------------- |
| offset | query | integer(int32) | false    | How many items to offset by for pagination    |
| limit  | query | integer(int32) | false    | How many items to return at one time (max 64) |

> Example responses

> 200 Response

```json
[
  {
		"id": "dcd6e820-5ea6-4835-8ad5-ddf3de82f3d2",
		"name": "Test Proof Template",
		"created": "2023-05-09T13:18:09.290Z",
		"updated": "2023-05-09T13:18:09.290Z",
		"request": {
			"input_descriptors": [
				{
					"id": "Credential 1",
					"name": "Test Proof Template",
					"purpose": "University Degree with name, issued date requested",
					"constraints": {
						"fields": [
							{
								"path": [
									"$.credentialSubject.name",
									"$.issuanceDate"
								]
							},
							{
								"path": [
									"$.type[*]"
								],
								"filter": {
									"type": "string",
									"pattern": "UniversityDegree"
								}
							}
						]
					}
				}
			]
		}
	}
]
```

#### Responses <a href="#get__proof-templates-responses" id="get__proof-templates-responses"></a>

| Status | Meaning                                                 | Description                      | Schema                                             |
| ------ | ------------------------------------------------------- | -------------------------------- | -------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1) | A paged array of proof templates | [ProofRequests](index.html.md#schemaproofrequests) |

### Create Proof Request Template

> POST /proof-templates REQUEST

> Code samples

```shell
# You can also use wget
curl -X POST https://api-testnet.dock.io/proof-templates \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

```json
{
  "attributes": {
    "property1": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    },
    "property2": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    }
  },
  "name": "Proof request",
  "nonce": "1234567890",
  "qr": "string"
}
```

#### Parameters <a href="#post__proof-templates-parameters" id="post__proof-templates-parameters"></a>

| Name | In   | Type                                             | Required | Description           |
| ---- | ---- | ------------------------------------------------ | -------- | --------------------- |
| body | body | [ProofRequest](index.html.md#schemaproofrequest) | true     | Proof template object |

> Example responses

> 200 Response

```json
{
  "attributes": {
    "property1": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    },
    "property2": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    }
  },
  "name": "Proof request",
  "nonce": "1234567890",
  "qr": "string",
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "error": "string",
  "created": "2019-08-24T14:15:22Z",
  "updated": "2019-08-24T14:15:22Z"
}
```

#### Responses <a href="#post__proof-templates-responses" id="post__proof-templates-responses"></a>

| Status | Meaning                                                               | Description                                              | Schema                                                         |
| ------ | --------------------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Proof request template created                           | [ProofTemplateObject](index.html.md#schemaprooftemplateobject) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)      | Invalid parameters                                       | [Error](index.html.md#schemaerror)                             |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed | [Error](index.html.md#schemaerror)                             |

### Get Proof Template History

> GET /proof-templates/{id}/history REQUEST

Get all of the previously created proof requests based on the specified template.

> Code samples

```shell
# You can also use wget
curl -X GET https://api-testnet.dock.io/proof-templates/{id}/history \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

#### Parameters <a href="#get__proof-templates_-id-_history-parameters" id="get__proof-templates_-id-_history-parameters"></a>

| Name   | In    | Type           | Required | Description                                   |
| ------ | ----- | -------------- | -------- | --------------------------------------------- |
| id     | path  | string(uuid)   | true     | Proof template UUID                           |
| offset | query | integer(int32) | false    | How many items to offset by for pagination    |
| limit  | query | integer(int32) | false    | How many items to return at one time (max 64) |

> Example responses

> 200 Response

```json
[
  {
    "attributes": {
      "property1": {
        "name": "favouriteDrink",
        "names": [
          "age"
        ]
      },
      "property2": {
        "name": "favouriteDrink",
        "names": [
          "age"
        ]
      }
    },
    "name": "Proof request",
    "nonce": "1234567890",
    "qr": "string"
  }
]
```

#### Responses <a href="#get__proof-templates_-id-_history-responses" id="get__proof-templates_-id-_history-responses"></a>

| Status | Meaning                                                        | Description                                             | Schema                                             |
| ------ | -------------------------------------------------------------- | ------------------------------------------------------- | -------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)        | Returns the information about the proof request history | [ProofRequests](index.html.md#schemaproofrequests) |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) | Proof template was not found.                           | [Error](index.html.md#schemaerror)                 |

### Create Proof Request from a Template

> POST /proof-templates/{id}/request REQUEST

Create a proof requtest based on the specified template.

> Code samples

```shell
# You can also use wget
curl -X POST https://api-testnet.dock.io/proof-templates/{id}/request \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

```json
{
  "nonce": "string",
  "domain": "string"
}
```

#### Parameters <a href="#post__proof-templates_-id-_request-parameters" id="post__proof-templates_-id-_request-parameters"></a>

| Name     | In   | Type         | Required | Description                       |
| -------- | ---- | ------------ | -------- | --------------------------------- |
| body     | body | object       | true     | Specify optional nonce and domain |
| » nonce  | body | string       | false    | none                              |
| » domain | body | string       | false    | none                              |
| id       | path | string(uuid) | true     | Proof template UUID               |

> Example responses

> 200 Response

```json
{
  "attributes": {
    "property1": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    },
    "property2": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    }
  },
  "name": "Proof request",
  "nonce": "1234567890",
  "qr": "string",
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "error": "string",
  "response_url": "string",
  "verified": true,
  "presentation": {},
  "created": "2019-08-24T14:15:22Z",
  "updated": "2019-08-24T14:15:22Z"
}
```

#### Responses <a href="#post__proof-templates_-id-_request-responses" id="post__proof-templates_-id-_request-responses"></a>

| Status | Meaning                                                               | Description                                              | Schema                                                       |
| ------ | --------------------------------------------------------------------- | -------------------------------------------------------- | ------------------------------------------------------------ |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Returns the information about the proof request          | [ProofRequestObject](index.html.md#schemaproofrequestobject) |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed | [Error](index.html.md#schemaerror)                           |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)        | Proof template was not found.                            | [Error](index.html.md#schemaerror)                           |

### Get Proof Template

> GET /proof-templates/{id} REQUEST

Get the details about a specific template.

> Code samples

```shell
# You can also use wget
curl -X GET https://api-testnet.dock.io/proof-templates/{id} \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

#### Parameters <a href="#get__proof-templates_-id-parameters" id="get__proof-templates_-id-parameters"></a>

| Name | In   | Type         | Required | Description         |
| ---- | ---- | ------------ | -------- | ------------------- |
| id   | path | string(uuid) | true     | Proof template UUID |

> Example responses

> 200 Response

```json
{
  "attributes": {
    "property1": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    },
    "property2": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    }
  },
  "name": "Proof request",
  "nonce": "1234567890",
  "qr": "string",
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "error": "string",
  "created": "2019-08-24T14:15:22Z",
  "updated": "2019-08-24T14:15:22Z"
}
```

#### Responses <a href="#get__proof-templates_-id-responses" id="get__proof-templates_-id-responses"></a>

| Status | Meaning                                                        | Description                                       | Schema                                                         |
| ------ | -------------------------------------------------------------- | ------------------------------------------------- | -------------------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)        | Returns the information about the proof templates | [ProofTemplateObject](index.html.md#schemaprooftemplateobject) |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4) | Proof templates was not found.                    | [Error](index.html.md#schemaerror)                             |

To perform this operation, you must be authenticated by means of one of the following methods: accessToken, bearerAuth, rapidAPI

### Update Proof Template

> PATCH /proof-templates/{id} REQUEST

> Code samples

```shell
# You can also use wget
curl -X PATCH https://api-testnet.dock.io/proof-templates/{id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

> Body parameter

```json
{
  "attributes": {
    "property1": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    },
    "property2": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    }
  },
  "name": "Proof request",
  "nonce": "1234567890",
  "qr": "string"
}
```

#### Parameters <a href="#patch__proof-templates_-id-parameters" id="patch__proof-templates_-id-parameters"></a>

| Name | In   | Type                                             | Required | Description           |
| ---- | ---- | ------------------------------------------------ | -------- | --------------------- |
| body | body | [ProofRequest](index.html.md#schemaproofrequest) | true     | Proof template object |
| id   | path | string(uuid)                                     | true     | Proof template UUID   |

> Example responses

> 200 Response

```json
{
  "attributes": {
    "property1": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    },
    "property2": {
      "name": "favouriteDrink",
      "names": [
        "age"
      ]
    }
  },
  "name": "Proof request",
  "nonce": "1234567890",
  "qr": "string",
  "id": "497f6eca-6276-4993-bfeb-53cbbbba6f08",
  "error": "string",
  "created": "2019-08-24T14:15:22Z",
  "updated": "2019-08-24T14:15:22Z"
}
```

#### Responses <a href="#patch__proof-templates_-id-responses" id="patch__proof-templates_-id-responses"></a>

| Status | Meaning                                                               | Description                                              | Schema                                                         |
| ------ | --------------------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)               | Profile has been updated                                 | [ProofTemplateObject](index.html.md#schemaprooftemplateobject) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)      | Error creating profile                                   | [Error](index.html.md#schemaerror)                             |
| 402    | [Payment Required](https://tools.ietf.org/html/rfc7231#section-6.5.2) | Transaction limit reached or upgrade required to proceed | [Error](index.html.md#schemaerror)                             |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)        | Proof templates was not found.                           | [Error](index.html.md#schemaerror)                             |

### Delete Proof Template

> DELETE /proof-templates/{id} REQUEST

Deletes the specified template and any associated data.

> Code samples

```shell
# You can also use wget
curl -X DELETE https://api-testnet.dock.io/proof-templates/{id} \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

#### Parameters <a href="#delete__proof-templates_-id-parameters" id="delete__proof-templates_-id-parameters"></a>

| Name | In   | Type         | Required | Description         |
| ---- | ---- | ------------ | -------- | ------------------- |
| id   | path | string(uuid) | true     | Proof template UUID |

> Example responses

> 400 Response

```json
{
  "status": 0,
  "type": "string",
  "message": "string"
}
```

#### Responses <a href="#delete__proof-templates_-id-responses" id="delete__proof-templates_-id-responses"></a>

| Status | Meaning                                                          | Description                     | Schema                             |
| ------ | ---------------------------------------------------------------- | ------------------------------- | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)          | Proof templates will be deleted | None                               |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1) | Something went wrong.           | [Error](index.html.md#schemaerror) |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)   | Proof templates was not found.  | [Error](index.html.md#schemaerror) |

## Registries <a href="#registries" id="registries"></a>

> Endpoints

[POST /registries](index.html.md#create-registry-parameters)\
[GET /registries](index.html.md#list-registries-responses)\
[GET /registries/{id}](index.html.md#get-registry-parameters)\
[POST /registries/{id}](index.html.md#revoke/unrevoke-credential-parameters)\
[DELETE /registries/{id}](index.html.md#delete-registry-responses)\\

Revocation means deleting or updating a credential. On Dock, credential revocation is managed with a revocation registry.

There can be multiple registries on the chain, and each registry has a unique id. It is recommended that the revocation authority create a new registry for each credential type. Dock Certs allows you to create, delete, and revoke/unrevoke the credential. You can retrieve a specified registry as well as a list of all registries created by the user.

For a detailed example of the registry workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/registryFlow.js).

If you want to revoke BBS+ credentials, you must create a registry with type \`DockVBAccumulator2022\`. For revoking other credentials, you can use \`StatusList2021Entry\` or \`CredentialStatusList2017\`.

### Create Registry

> POST /registries REQUEST

```shell
curl --location --request POST https://api.dock.io/registries/ \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
  "addOnly": true,
  "policy": [
    "did:dock:xyz"
  ],
  "type": "CredentialStatusList2017"
}'


```

```json-doc

{
  "addOnly": true,
  "policy": [
    "did:dock:xyz"
  ],
  "type": "CredentialStatusList2017"
}
```

To create a registry, you have to create a `policy` object for which a DID is needed. It is advised that the DID is registered on the chain first. Otherwise, someone can look at the registry and register the DID, thus gaining control of the registry.

Choosing the right revocation registry is essential. Here's a simplified overview of the available options:

* CredentialStatusList2017
  * Only supports non-BBS+ credentials.
  * Individual Tracking: Each entry is tracked separately, which means more ledger space is used for multiple entries.
  * This registry is cost-effective for a single entry. However, managing several entries can be more expensive.
  * Implements add-only policies.
* StatusList2021Entry
  * Only supports non-BBS+ credentials.
  * Recommended for most users.
  * Collective Tracking: Manages all revocation entries together, making it less costly to revoke multiple credentials simultaneously.
  * W3C Compliant.
* DockVBAccumulator2022
  * Only supports BBS+ credentials.
  * Utilizes an on-ledger accumulator for enhanced privacy.
  * Offers more privacy than the W3C Status List 2021.

#### Parameters <a href="#create-registry-parameters" id="create-registry-parameters"></a>

| Name    | In   | Type                                      | Required | Description                                                                                                                                         |
| ------- | ---- | ----------------------------------------- | -------- | --------------------------------------------------------------------------------------------------------------------------------------------------- |
| addOnly | body | boolean                                   | false    | True/false options. The default value is "false".                                                                                                   |
| policy  | body | \[[DIDDock](index.html.md#schemadiddock)] | true     | The DIDs which control this registry. You must own a DID listed here to use the registry. Only one policy supported as of now: `OneOf` DID in list. |
| type    | body | string                                    | false    | Specifies which type of registry to create. Defaults to `StatusList2021Entry`.                                                                      |

#### Enumerated Values

| Parameter | Value                                                                            | Description                         |
| --------- | -------------------------------------------------------------------------------- | ----------------------------------- |
| type      | StatusList2021Entry **or** CredentialStatusList2017 **or** DockVBAccumulator2022 | The type used in registry creation. |

> 200 Response

```json
{
  "id": "930",
  "data": {
    "id": "6151e62d7e03bc4012fde0595cfdb0d140e463a2f0ad5a431ff47243374bc612",
    "policy": {
      "type": "OneOf",
      "policy": [
        "did:dock:5GKeTJ7iMU4hEUwhK9a6ogh1bsWAv8Z1TMKnUf1vCNgdoiEM"
      ],
      "addOnly": false
    },
    "type": "CredentialStatusList2017",
  }
}
```

#### Responses <a href="#create-registry-responses" id="create-registry-responses"></a>

| Status | Meaning                                                                          | Description                                                                          | Schema                                                   |
| ------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------ | -------------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will try to create the registry.                      | [JobStartedResult](index.html.md#schemajobstartedresult) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)                 | The request was unsuccessful, because of invalid params, e.g., policy not supported. | [Error](index.html.md#schemaerror)                       |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                             | [Error](index.html.md#schemaerror)                       |

### List Registries

> GET /registries REQUEST

```shell
curl --location --request GET https://api.dock.io/registries/ \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw'{

  }'

```

Return a list of all registries created by the user. The list is returned with the registry id and policy of the revocation registry.

For now, only one policy is supported, and each registry is owned by a single DID.

> 200 Response

```json
[
  {
    "id": "6151e62d7e03bc4012fde0595cfdb0d140e463a2f0ad5a431ff47243374bc612",
    "policy_and_type": {
      "type": "OneOf",
      "policy": [
        "did:dock:5GKeTJ7iMU4hEUwhK9a6ogh1bsWAv8Z1TMKnUf1vCNgdoiEM"
      ],
      "addOnly": false
    },
    "registry_type": "CredentialStatusList2017",
    "created_at": "2021-11-25T12:20:51.773Z"
  }
]
```

#### Parameters <a href="#list-dids-parameters" id="list-dids-parameters"></a>

| Name   | In    | Type    | Required | Description                                   |
| ------ | ----- | ------- | -------- | --------------------------------------------- |
| offset | query | integer | false    | How many items to offset by for pagination    |
| limit  | query | integer | false    | How many items to return at one time (max 64) |

#### Responses <a href="#list-registries-responses" id="list-registries-responses"></a>

| Status | Meaning                                                                          | Description                                                                    | Schema                             |
| ------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will return all registries created by the user. | Inline                             |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                       | [Error](index.html.md#schemaerror) |

### Get Registry

> GET /registries/{id} REQUEST

```shell
curl --location --request GET https://api.dock.io/registries/{id} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''


```

Get the details of an existing registry, such as policy, add-only status, when it was last updated, and controller(s). You need only supply the revocation registry id that was returned upon revocation registry creation.

#### Parameters <a href="#get-registry-parameters" id="get-registry-parameters"></a>

| Name | In   | Type                               | Required | Description             |
| ---- | ---- | ---------------------------------- | -------- | ----------------------- |
| id   | path | [Hex32](index.html.md#schemahex32) | true     | Revocation registry id. |

> 200 Response

```json
{
  "id": "6151e62d7e03bc4012fde0595cfdb0d140e463a2f0ad5a431ff47243374bc612",
  "policy_and_type": {
    "type": "OneOf",
    "policy": [
      "did:dock:5GKeTJ7iMU4hEUwhK9a6ogh1bsWAv8Z1TMKnUf1vCNgdoiEM"
    ],
    "addOnly": false
  },
  "registry_type": "CredentialStatusList2017",
  "created_at": "2021-11-25T12:20:51.773Z",
  "job_id": "930"
}
```

#### Responses <a href="#get-registry-responses" id="get-registry-responses"></a>

| Status | Meaning                                                                          | Description                                                                  | Schema                                   |
| ------ | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will return the revocation registry metadata. | [Registry](index.html.md#schemaregistry) |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)                   | The request was unsuccessful, because the registry was not found.            | [Error](index.html.md#schemaerror)       |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                     | [Error](index.html.md#schemaerror)       |

### Revoke/Unrevoke Credential

> POST /registries/{id} REQUEST

```shell
curl --location --request POST https://api.dock.io/registries/{id} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
  "action": "revoke",
  "credentialIds": [
    "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb"
  ]
}'

```

```json-doc

{
  "action": "revoke",
  "credentialIds": [
    "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb"
  ]
}
```

Credential revocation is managed with on-chain revocation registries. To revoke a credential, its id (or hash of its id) must be added to the credential. It is advised to have one revocation registry per credential type. Revoking an already revoked credential has no effect.

Similar to the replay protection mechanism for DIDs, the last modified block number is kept for each registry, which is updated each time a credential is revoked or unrevoked. Unrevoking an unrevoked credential has no effect.

In this API, simply add Revoke/Unrevoke into the `action` parameter and input the desired credential ids.

#### Parameters <a href="#revoke-unrevoke-credential-parameters" id="revoke-unrevoke-credential-parameters"></a>

| Name          | In   | Type                               | Required | Description                                                                |
| ------------- | ---- | ---------------------------------- | -------- | -------------------------------------------------------------------------- |
| id            | path | [Hex32](index.html.md#schemahex32) | true     | Revocation registry id.                                                    |
| action        | body | string                             | false    | The action taken, either revoke or unrevoke. The default value is "revoke" |
| credentialIds | body | array                              | true     | The list of credential ids to act upon.                                    |

#### Enumerated Values

| Parameter | Value                  | Description                     |
| --------- | ---------------------- | ------------------------------- |
| action    | revoke **or** unrevoke | Action to take on the registry. |

> 200 Response

```json
{
  "id": "931",
  "data": {
    "revokeIds": [
      "0xaff1aa6770d43d684690c0ad679a8608d5b7576feb3fdc1d6712decf73ca44ef"
    ]
  }
}
```

#### Responses <a href="#revoke-unrevoke-credential-responses" id="revoke-unrevoke-credential-responses"></a>

| Status | Meaning                                                                          | Description                                                                | Schema                                                   |
| ------ | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will try to revoke/unrevoke the credential. | [JobStartedResult](index.html.md#schemajobstartedresult) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)                 | The request was unsuccessful, because of invalid params.                   | [Error](index.html.md#schemaerror)                       |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)                   | The request was unsuccessful, because the registry was not found.          | [Error](index.html.md#schemaerror)                       |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                   | [Error](index.html.md#schemaerror)                       |

### Delete Registry

> DELETE /registries/{id} REQUEST

```shell
curl --location --request POST https://api.dock.io/registries/{id} \
  --header 'DOCK-API-TOKEN: API_KEY'

```

A registry can be deleted, leading to all the corresponding revocation ids being deleted as well. This requires the signature from the owner, similar to the other updates.

#### Parameters <a href="#delete-registry-parameters" id="delete-registry-parameters"></a>

| Name | In   | Type                               | Required | Description             |
| ---- | ---- | ---------------------------------- | -------- | ----------------------- |
| id   | path | [Hex32](index.html.md#schemahex32) | true     | Revocation registry id. |

> 200 Response

```json
{
  "id": "932",
  "data": {
  "id": "6151e62d7e03bc4012fde0595cfdb0d140e463a2f0ad5a431ff47243374bc612",
  "hexId": "6151e62d7e03bc4012fde0595cfdb0d140e463a2f0ad5a431ff47243374bc612",
  "lastModified": 4226296
  }
}
```

#### Responses <a href="#delete-registry-responses" id="delete-registry-responses"></a>

| Status | Meaning                                                                          | Description                                                         | Schema                                                   |
| ------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------- | -------------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and revocation registry will be deleted. | [JobStartedResult](index.html.md#schemajobstartedresult) |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)                   | The request was unsuccessful, because the registry was not found.   | [Error](index.html.md#schemaerror)                       |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed            | [Error](index.html.md#schemaerror)                       |

## Revocation Status <a href="#revocationstatus" id="revocationstatus"></a>

Credentials can be revoked or unrevoked, and as such they contain a revocation status so that verifiers/issuers can check if the credential is still valid. Once a revocation registry has been created and credentials issued with it, you can check the revocation status. Verifiers will do this automatically.

### Get Revocation Status

> GET /revocationStatus/{regId}/{revId} REQUEST

```shell

curl --location --request GET https://api.dock.io/revocationStatus/{regId}/{revId} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

To check if an id is revoked or not, you can check its status with the registry id (`regId`) and revocation id (`revId`).

#### Parameters <a href="#get-revocation-status-parameters" id="get-revocation-status-parameters"></a>

| Name  | In   | Type                               | Required | Description               |
| ----- | ---- | ---------------------------------- | -------- | ------------------------- |
| regId | path | [Hex32](index.html.md#schemahex32) | true     | Revocation registry id.   |
| revId | path | [Hex32](index.html.md#schemahex32) | true     | Credential revocation id. |

> 200 Response

```json
{
  "type": true
}
```

#### Responses <a href="#get-revocation-status-responses" id="get-revocation-status-responses"></a>

| Status | Meaning                                                                          | Description                                                                                                                                                                   | Schema                             |
| ------ | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will return **true**, if the credential is revoked, **false** otherwise.                                                                       | Inline                             |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)                   | The request was unsuccessful, because the registry was not found.                                                                                                             | [Error](index.html.md#schemaerror) |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                                                                                                                      | [Error](index.html.md#schemaerror) |
| 400    | [Server Error](https://datatracker.ietf.org/doc/html/rfc7231#section-6.6.1)      | The request was unsuccessful, because you have not revoked or unrevoked the registered credential yet. Please try to revoke/unrevoke the registered credential and try again. | [Error](index.html.md#schemaerror) |

### Get Revocation Status Witness

> GET /revocationStatus/{regId}/{revId}/witness REQUEST

```shell

curl --location --request GET https://api.dock.io/revocationStatus/{regId}/{revId} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

The accumulator witness is utilized by the holder to generate a proof, which combines the witness with their revocation id associated with the credential id (`revId`) and the accumulator associated with the registry id (`regId`), allowing the verifier to validate the credential's status without directly accessing the revocation id on the blockchain.

#### Parameters <a href="#get-revocation-status-parameters" id="get-revocation-status-parameters"></a>

| Name  | In   | Type                               | Required | Description               |
| ----- | ---- | ---------------------------------- | -------- | ------------------------- |
| regId | path | [Hex32](index.html.md#schemahex32) | true     | Revocation registry id.   |
| revId | path | [Hex32](index.html.md#schemahex32) | true     | Credential revocation id. |

> 200 Response

```json
{
  "value": "0x81aa308882b663491e2b42803ad0855b030d92a586bc378bc844e1e003c8098a23f0d7d75b4fdbfb4b42cfc42aca8ad3"
}
```

#### Responses <a href="#get-revocation-status-responses" id="get-revocation-status-responses"></a>

| Status | Meaning                                                                          | Description                                                                                                                                                                   | Schema                             |
| ------ | -------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will return the membership witness.                                                                                                            | Inline                             |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)                   | The request was unsuccessful, because the registry was not found.                                                                                                             | [Error](index.html.md#schemaerror) |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                                                                                                                      | [Error](index.html.md#schemaerror) |
| 400    | [Server Error](https://datatracker.ietf.org/doc/html/rfc7231#section-6.6.1)      | The request was unsuccessful, because you have not revoked or unrevoked the registered credential yet. Please try to revoke/unrevoke the registered credential and try again. | [Error](index.html.md#schemaerror) |

## Credential Schemas <a href="#credential-schemas" id="credential-schemas"></a>

> Endpoints

[POST /schemas](index.html.md#create-schema-responses)\
[GET /schemas](index.html.md#list-schemas-responses)\
[GET /schemas/{schemaId}](index.html.md#get-schema-parameters)\\

Schemas are useful when enforcing a specific structure on a collection of data like a Verifiable Credential. Data Verification schemas, for example, are used to verify that the structure and contents of a Verifiable Credential conform to a published schema. On the other hand, Data Encoding schemas are used to map the contents of a Verifiable Credential to an alternative representation format, such as a binary format used in a zero-knowledge proof.

### Create Schema

> POST /schemas REQUEST

```shell
curl --location --request POST https://api.dock.io/schemas \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '{
 "$schema": "http://json-schema.org/draft-07/schema#",
 "description": "Dock Schema Example",
 "type": "object",
 "properties": {
  "id": {
    "type": "string"
 },
 "emailAddress": {
  "type": "string",
  "format": "email"
 },
 "alumniOf": {
  "type": "string"
 }
 },
 "required": [
  "emailAddress",
  "alumniOf"
 ],
 "additionalProperties": false,
 "author": "{{did}}"
}'


```

```json-doc
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "description": "Dock Schema Example",
  "type": "object",
  "properties": {
    "id": {
      "type": "string"
    },
    "emailAddress": {
      "type": "string",
      "format": "email"
    },
    "alumniOf": {
      "type": "string"
    }
  },
  "required": [
    "emailAddress",
    "alumniOf"
  ],
  "additionalProperties": false,
  "author": "{{did}}"
}
```

Schemas are used to describe the structure of credentials, specifically the credential subject. It helps the issuer, holder, and verifier to unambiguously determine the claims contained within the credential. To create a schema, you need to define the object body using JSON schema.

#### Parameters <a href="#create-schema-parameters" id="create-schema-parameters"></a>

| Name | In   | Type   | Required | Description  |
| ---- | ---- | ------ | -------- | ------------ |
| body | body | object | true     | JSON-schema. |

> 200 Response

```json
{
  "id": "1082",
  "data": {
    "schema": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "description": "Dock Schema Example 3",
      "type": "object",
      "properties": {
        "id": {
          "type": "string"
        },
        "emailAddress": {
          "type": "string",
          "format": "email"
        },
        "alumniOf": {
          "type": "string"
        }
      },
      "required": [
        "emailAddress",
        "alumniOf"
      ],
      "additionalProperties": false
    },
    "author": "did:dock:5FBZNTZ4eg2EBuvEcYdkEtAhCXhCEA8zmPzYTwexM3g13fkF",
    "signature": {
      "Secp256k1": "..."
    },
    "id": "https://schema.dock.io/TestSchema-V1-1695817897561.json",
    "uri": "https://schema.dock.io/TestSchema-V1-1695817897561.json"
  }
}
```

#### Responses <a href="#create-schema-responses" id="create-schema-responses"></a>

| Status | Meaning                                                                          | Description                                                                                    | Schema                             |
| ------ | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will try to create schema.                                      | [JobId](index.html.md#schemajobid) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)                 | The request was unsuccessful, because of invalid params, e.g., size not supported or not JSON. | [Error](index.html.md#schemaerror) |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                                       | [Error](index.html.md#schemaerror) |

### List Schemas

> GET /schemas REQUEST

```shell
curl --location --request GET https://api.dock.io/schemas \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

Return a list of all schemas created by the authenticated user.

> 200 Response

```json
[
  {
    "schema": {
      "$schema": "http://json-schema.org/draft-07/schema#",
      "description": "Dock Schema Example",
      "type": "object",
      "properties": {
        "id": {
          "type": "string"
        },
        "emailAddress": {
          "type": "string",
          "format": "email"
        },
        "alumniOf": {
          "type": "string"
        }
      },
      "required": [
        "emailAddress",
        "alumniOf"
      ],
      "additionalProperties": false
    },
    "author": "did:dock:5HcbppP8LjoJFYRV7PTLEyPy3ZUK9JCkzC4PQHuVF34gRhe6",
    "id": "https://schema.dock.io/TestSchema-V1-1695817897561.json",
    "uri": "https://schema.dock.io/TestSchema-V1-1695817897561.json"
  }
]
```

#### Parameters <a href="#list-schemas-parameters" id="list-schemas-parameters"></a>

| Name   | In    | Type    | Required | Description                                   |
| ------ | ----- | ------- | -------- | --------------------------------------------- |
| offset | query | integer | false    | How many items to offset by for pagination    |
| limit  | query | integer | false    | How many items to return at one time (max 64) |

#### Responses <a href="#list-schemas-responses" id="list-schemas-responses"></a>

| Status | Meaning                                                                          | Description                                                                 | Schema                             |
| ------ | -------------------------------------------------------------------------------- | --------------------------------------------------------------------------- | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will return all schemas created by the user. | Inline                             |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                    | [Error](index.html.md#schemaerror) |

### Get Schema

> GET /schemas/{schemaId} REQUEST

```shell
curl --location --request GET https://api.dock.io/schemas/{schemaId} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

Reading a Schema from the Dock chain can easily be achieved by using the `get` method which will return the JSON schema to a specific schema ID. The `schemaId`needs to be URL encoded (e.g. `/schemas/https%3A%2F%2Fschema.dock.io%2FTestSchema-V1-1695817897561.json`)

#### Parameters <a href="#get-schema-parameters" id="get-schema-parameters"></a>

| Name     | In   | Type   | Required | Description              |
| -------- | ---- | ------ | -------- | ------------------------ |
| schemaId | path | String | true     | A URL encoded schema id. |

> 200 Response

```json
{
  "schema": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "description": "Dock Schema Example",
    "type": "object",
    "properties": {
      "id": {
        "type": "string"
      },
      "emailAddress": {
        "type": "string",
        "format": "email"
      },
      "alumniOf": {
        "type": "string"
      }
    },
    "required": [
      "emailAddress",
      "alumniOf"
    ],
    "additionalProperties": false
  },
  "author": "did:dock:5HcbppP8LjoJFYRV7PTLEyPy3ZUK9JCkzC4PQHuVF34gRhe6",
  "id": "https://schema.dock.io/TestSchema-V1-1695817897561.json",
  "uri": "https://schema.dock.io/TestSchema-V1-1695817897561.json"
}
```

#### Responses <a href="#get-schema-responses" id="get-schema-responses"></a>

| Status | Meaning                                                                          | Description                                                     | Schema                             |
| ------ | -------------------------------------------------------------------------------- | --------------------------------------------------------------- | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and returns the requested Schema.    | Inline                             |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)                   | The request was unsuccessful, because the schema was not found. | [Error](index.html.md#schemaerror) |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed        | [Error](index.html.md#schemaerror) |

## Anchors <a href="#anchors" id="anchors"></a>

> Endpoints

\
[POST /anchors](index.html.md#create-anchor-responses)\
[GET /anchors](index.html.md#list-anchors-responses)\
[GET /anchors/{anchor}](index.html.md#get-anchor-responses)

Anchoring allows users to store a digest of one or more credentials (or any document) on our blockchain, tying them to immutable timestamps and proving that they were generated at a certain moment in time. By enabling this feature, users will have more options for auditing credentials given and timestamping any documents.

The Dock Blockchain includes a module explicitly intended for proof of existence. You post the hash of a document on-chain at a specific block. Later you can use that hash to prove the document existed at or before that block.

The API allows you to create, get, and retrieve anchors as well as a list of all anchors created by the user.

For a detailed example of the anchor workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/anchorsFlow.js).

### Create Anchor

> POST /anchors REQUEST

```shell
curl --location --request POST https://api.dock.io/anchors \

  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '[
  "can be a string",
  {
    "or": "a JSON document"
  }
]'

```

```json-doc

[
  "can be a string",
  {
    "or": "a JSON document"
  }
]
```

Creating an anchor will state on the blockchain that one or more document hashes were created at a specific time. In the context of verifiable credentials, anchors are used to attest that the credential document was not altered and was created at a specific time. Batching multiple documents/credentials into a single anchor is done through a Merkle tree and can save on cost/time as only the Merkle root has to be anchored.

The API will store the `blake2b256` hash of a document or string that you provide. Dock provides a [fully functioning reference client](https://fe.dock.io/#/anchor/batch) and [SDK example](https://github.com/docknetwork/sdk/blob/master/example/anchor.js) for anchoring.

#### Parameters <a href="#create-anchor-parameters" id="create-anchor-parameters"></a>

| Name | In   | Type                     | Required | Description                                                                                                                                                                   |
| ---- | ---- | ------------------------ | -------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| body | body | array of strings or JSON | true     | Supply an array of strings or JSON documents to be hashed and anchored to the blockchain. For credentials, send the Verifiable Credential document(s) or anchor when issuing. |

> 200 Response

```json
{
  "id": "829",
  "data": {
    "root": "0xdfc3cd9ff7836143746c292d4099e62277fac4c2b6a1c004d784adcbc0319634",
    "proofs": []
  }
}
```

#### Responses <a href="#create-anchor-responses" id="create-anchor-responses"></a>

| Status | Meaning                                                                          | Description                                                                    | Schema                             |
| ------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------ | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will try to create an anchor on the blockchain. | [JobId](index.html.md#schemajobid) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)                 | The request was unsuccessful, because of invalid params.                       | [Error](index.html.md#schemaerror) |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                       | [Error](index.html.md#schemaerror) |

### List Anchors

> GET /anchors REQUEST

```shell
curl --location --request GET https://api.dock.io/anchors \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''

```

Return a list of all anchors created by the authenticated user, regardless of whether they have contributed to the batching or not.

> 200 Response

```json
[
  {
    "anchor":"54bdd55207c4d41d2b8a7780e967bb5a06bdfb793fc4055baf244e60cd0d839c",
    "type": "single",
    "data": {
      "proofs": [],
      "root":"0x54bdd55207c4d41d2b8a7780e967bb5a06bdfb793fc4055baf244e60cd0d839c",
      "documentIds": [
        "https://creds.dock.io/credential/b1ed680d3d2d8167dc31bc4913e9c511"
      ]
     },
     "created_at": "2021-11-12T13:53:51.640Z",
     "job_id": "827"
  }
]
```

#### Parameters <a href="#list-anchors-parameters" id="list-anchors-parameters"></a>

| Name   | In    | Type    | Required | Description                                   |
| ------ | ----- | ------- | -------- | --------------------------------------------- |
| offset | query | integer | false    | How many items to offset by for pagination    |
| limit  | query | integer | false    | How many items to return at one time (max 64) |

#### Responses <a href="#list-anchors-responses" id="list-anchors-responses"></a>

| Status | Meaning                                                                          | Description                                                                 | Schema                             |
| ------ | -------------------------------------------------------------------------------- | --------------------------------------------------------------------------- | ---------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will return all anchors created by the user. | Inline                             |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                    | [Error](index.html.md#schemaerror) |

### Get Anchor

> GET /anchors/{anchor} REQUEST

```shell
curl --location --request GET https://api.dock.io/anchors/{anchor} \
  --header 'DOCK-API-TOKEN: API_KEY'
  --data-raw ''

```

Get a specific anchor with the given ID.

#### Parameters <a href="#get-anchor-parameters" id="get-anchor-parameters"></a>

| Name   | In   | Type                               | Required | Description   |
| ------ | ---- | ---------------------------------- | -------- | ------------- |
| anchor | path | [Hex32](index.html.md#schemahex32) | true     | An anchor id. |

> 200 Response

```json
{
  "type": "single",
  "proofs": [],
  "root": "0x00",
  "created_at": "2021-11-30T15:47:24.667Z"
}
```

#### Responses <a href="#get-anchor-responses" id="get-anchor-responses"></a>

| Status | Meaning                                                                          | Description                                                                                | Schema                               |
| ------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------ |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and returns the anchor's details, e.g., `blockHash` and `root`. | [Anchor](index.html.md#schemaanchor) |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)                   | The request was unsuccessful, because the anchor was not found.                            | [Error](index.html.md#schemaerror)   |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                                   | [Error](index.html.md#schemaerror)   |

### Verify Anchor

> POST /verify REQUEST

```shell
curl --location --request POST https://api.dock.io/anchors \

  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw '[
  "can be a string",
  {
    "or": "a JSON document"
  }
]'
```

```json-doc

{
  "documents": [],
  "proofs": [],
  "root": "0x00"
}
```

Verify an anchor's merkle root and proof by supplying the source documents (array of strings of JSON objects, same as in anchor creation).

#### Parameters <a href="#get-anchor-parameters" id="get-anchor-parameters"></a>

| Name      | In   | Type                               | Required | Description                                                             |
| --------- | ---- | ---------------------------------- | -------- | ----------------------------------------------------------------------- |
| documents | body | array of strings or JSON           | true     | An array of strings or JSON objects to represent documents to be hashed |
| proofs    | body | JSON object array                  | true     | An array of proofs given on anchor creation                             |
| root      | body | [Hex32](index.html.md#schemahex32) | true     | The anchor merkle root/ID.                                              |

> 200 Response

```json
{
  "verified": true,
  "results": [
    {}
  ]
}
```

#### Responses <a href="#get-anchor-responses" id="get-anchor-responses"></a>

| Status | Meaning                                                                          | Description                                                                                | Schema                               |
| ------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------ |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and returns the anchor's details, e.g., `blockHash` and `root`. | [Anchor](index.html.md#schemaanchor) |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed                                   | [Error](index.html.md#schemaerror)   |

## Jobs <a href="#jobs" id="jobs"></a>

> Endpoints

[GET /jobs/{Id}](index.html.md#get-job-status-and-data-parameters)\\

In Dock Certs, "jobs" are blockchain transactions that we submit on your behalf. You can choose to either register a webhook or poll the API to receive job information. Certain things in the API, such as revoking a credential, require a blockchain transaction to finalize before the job can be considered "done". The time to wait varies on network load and other factors, but typically is within 5-10 seconds.

You can track the current job status by querying the job id returned as part of the initial API response that triggered the job. The work is done asynchronously.

### Get Job Status and Data

> GET /jobs/{Id} REQUEST

```shell
curl --location --request GET https://api.dock.io/jobs/{id} \
  --header 'DOCK-API-TOKEN: API_KEY'

```

To check the Job status and data, you can use the `GET` method and simply put the Job id. It will return information related to the job being processed and its associated blockchain transaction. On completion or failure, the job data will be updated with a response from the blockchain.

#### Parameters <a href="#get-job-status-and-data-parameters" id="get-job-status-and-data-parameters"></a>

| Name | In   | Type                               | Required | Description          |
| ---- | ---- | ---------------------------------- | -------- | -------------------- |
| id   | path | [JobId](index.html.md#schemajobid) | true     | Represents a Job id. |

> 200 Response

```json
{
  "id": "123",
  "result": {
    "InBlock": "0x00"
  },
  "status": "finalized"
}
```

#### Responses <a href="#get-job-status-and-data-responses" id="get-job-status-and-data-responses"></a>

| Status | Meaning                                                                          | Description                                                     | Schema                                 |
| ------ | -------------------------------------------------------------------------------- | --------------------------------------------------------------- | -------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and return the job description.      | [JobDesc](index.html.md#schemajobdesc) |
| 404    | [Not Found](https://tools.ietf.org/html/rfc7231#section-6.5.4)                   | The request was unsuccessful, because the Job id was not found. | [Error](index.html.md#schemaerror)     |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed        | [Error](index.html.md#schemaerror)     |

## Verify <a href="#verify" id="verify"></a>

### VCDM Verification

> POST /verify REQUEST

```shell
curl --location --request POST https://api.dock.io/verify \
  --header 'DOCK-API-TOKEN: API_KEY'
  --header 'Content-Type: application/json' \
  --data-raw '{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "https://creds.dock.io/credential/93a1cd57a46fd5e6e641f0288e2f8b44",
  "type": [
    "VerifiableCredential"
  ],
  "credentialSubject": [
    {
      "id": "did:dock:5Gwh4PxDjLUXnfqExALYTju9UpZTHzBLNb7j8Ug8NhTKivUe"
    }
  ],
  "issuanceDate": "2021-11-18T19:28:49.840Z",
  "proof": {
    "type": "EcdsaSecp256k1Signature2019",
    "created": "2021-11-18T19:28:51Z",
    "verificationMethod": "did:dock:5FfmGmkY1BqEqRQhRLCLDLHPBFvhSbEBK3DJhEk9mbkpfAXT#keys-1",
    "proofPurpose": "assertionMethod",
    "proofValue": "zAN1rKvtics5d8AZ5rvm9n9DNjfXGtFegv48PorsWvQdeVKPkzSSyKJzdN3jjnfTNqFDg5FWpXeYhubsFKnX8zLNiBsb3D32k3"
  },
  "issuer": {
    "id": "did:dock:5FfmGmkY1BqEqRQhRLCLDLHPBFvhSbEBK3DJhEk9mbkpfAXT",
    "name": "my issuer"
  }
}'


```

```json-doc

{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "https://creds.dock.io/credential/93a1cd57a46fd5e6e641f0288e2f8b44",
  "type": [
    "VerifiableCredential"
  ],
  "credentialSubject": [
    {
      "id": "did:dock:5Gwh4PxDjLUXnfqExALYTju9UpZTHzBLNb7j8Ug8NhTKivUe"
    }
  ],
  "issuanceDate": "2021-11-18T19:28:49.840Z",
  "proof": {
    "type": "EcdsaSecp256k1Signature2019",
    "created": "2021-11-18T19:28:51Z",
    "verificationMethod": "did:dock:5FfmGmkY1BqEqRQhRLCLDLHPBFvhSbEBK3DJhEk9mbkpfAXT#keys-1",
    "proofPurpose": "assertionMethod",
    "proofValue": "zAN1rKvtics5d8AZ5rvm9n9DNjfXGtFegv48PorsWvQdeVKPkzSSyKJzdN3jjnfTNqFDg5FWpXeYhubsFKnX8zLNiBsb3D32k3"
  },
  "issuer": {
    "id": "did:dock:5FfmGmkY1BqEqRQhRLCLDLHPBFvhSbEBK3DJhEk9mbkpfAXT",
    "name": "my issuer"
  }
}
```

A verifier upon receiving a verifiable presentation verifies the validity of each credential in the presentation. This includes checking the correctness of the data model of the credential, the authenticity by verifying the issuer's signature and revocation status if the credential is revocable. It then checks whether the presentation contains the signature from the holder on the presentation, including his given challenge.

You can verify issued/received credentials and presentations using this route. Verification will check that the JSON-LD document's cryptographic proof is correct and that it has not been revoked. It will return a verification status with a boolean verified result.

#### Parameters <a href="#verify-a-credential-or-presentation-parameters" id="verify-a-credential-or-presentation-parameters"></a>

| Name | In   | Type                                                                                                                                     | Required | Description                                                                              |
| ---- | ---- | ---------------------------------------------------------------------------------------------------------------------------------------- | -------- | ---------------------------------------------------------------------------------------- |
| body | body | [VerifiableCredential](index.html.md#schemaverifiablecredential) or [VerifiablePresentation](index.html.md#schemaverifiablepresentation) | true     | Provide as the body a Verifiable Credential or Verifiable Presentation JSON-LD document. |

> 200 Response

```json
{
  "verified": true,
  "results": [...]
}
```

#### Responses <a href="#verify-a-credential-or-presentation-responses" id="verify-a-credential-or-presentation-responses"></a>

| Status | Meaning                                                                          | Description                                                         | Schema                                                           |
| ------ | -------------------------------------------------------------------------------- | ------------------------------------------------------------------- | ---------------------------------------------------------------- |
| 200    | [OK](https://tools.ietf.org/html/rfc7231#section-6.3.1)                          | The request was successful and will return the verification result. | [VerificationResponse](index.html.md#schemaverificationresponse) |
| 400    | [Bad Request](https://tools.ietf.org/html/rfc7231#section-6.5.1)                 | The request was unsuccessful, because of invalid credential params. | [Error](index.html.md#schemaerror)                               |
| 402    | [Payment required](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402) | Transaction limit reached or upgrade required to proceed            | [Error](index.html.md#schemaerror)                               |

## Sub-Accounts <a href="#subaccounts" id="subaccounts"></a>

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
