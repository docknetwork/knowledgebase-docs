# Presentations

The presentation is signed using the holder's private key as it is being created. To validate the presentation, the verifier must also check the issuer's signature and the holder's public key. One way to achieve this is to make the holder have a DID too, so that the verifier can look up the DID on the chain and learn the public key.

The API allows you to create and sign a verifiable presentation out of one or more Verifiable Credentials.

For a detailed example of the presentations workflow. Please refer [here](https://github.com/docknetwork/dock-api-js/blob/main/workflows/presentationsFlow.js).

## Create Presentation <a href="#create-a-presentation" id="create-a-presentation"></a>

The holder while creating the presentation signs it with his private key. For the verifier to verify the presentation, in addition to verifying the issuer's signature, he/she needs to verify this signature as well, and for that he must know the holder's public key.

This is an operation to create and sign a verifiable presentation out of one or more Verifiable Credentials.

### Parameters <a href="#create-a-presentation-parameters" id="create-a-presentation-parameters"></a>

<table data-full-width="true"><thead><tr><th width="133">Name</th><th width="86">In</th><th width="111">Type</th><th width="90">Required</th><th>Description</th></tr></thead><tbody><tr><td>holder</td><td>body</td><td><a href="index.html.md#schemadiddock">DIDDock</a></td><td>true</td><td>DID as fully qualified, e.g., <code>did:dock:xyz</code>.</td></tr><tr><td>challenge</td><td>body</td><td>string</td><td>false</td><td>Presentation's Challenge in a string format. The default value for this is <code>random hex string</code>. NOTE: if this presentation is being created to respond to a <code>proof-request</code> the challenge should be set to the value from the <code>nonce</code> field in the proof-request.</td></tr><tr><td>domain</td><td>body</td><td>string</td><td>false</td><td>A domain for the proof in a string format. The default value for the domain is <code>dock.io</code>.</td></tr><tr><td>credentials</td><td>body</td><td><a href="index.html.md#schemaverifiablecredential">VerifiableCredential</a></td><td>false</td><td>Verifiable (signed) Credential returned by API.</td></tr></tbody></table>

### Enumerated Values

<table data-full-width="true"><thead><tr><th width="166">Parameter</th><th width="273">Value</th><th>Description</th></tr></thead><tbody><tr><td>type</td><td>Sr25519Signature2020 <strong>or</strong> Ed25519Signature2018 <strong>or</strong> EcdsaSecp256k1Signature2019</td><td>Type of Signature.</td></tr><tr><td>proofPurpose</td><td>assertionMethod <strong>or</strong> authentication</td><td>The purpose the credential will be used for.</td></tr></tbody></table>

### Responses <a href="#create-a-presentation-responses" id="create-a-presentation-responses"></a>

<table data-full-width="true"><thead><tr><th width="106">Status</th><th width="135">Meaning</th><th width="327">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and returns a Verifiable Presentation.</td><td><a href="index.html.md#schemaverifiablepresentation">VerifiablePresentation</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid/insufficient parameters.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>401</td><td><a href="https://tools.ietf.org/html/rfc7235#section-3.1">Unauthorized</a></td><td>The request was unsuccessful, either because of a missing/invalid auth header or you don't own the DID.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /presentations REQUEST PAYLOAD</summary>

```json

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

</details>

<details>

<summary>POST /presentations REQUEST CURL</summary>

```bash
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

</details>

<details>

<summary>200 Response</summary>

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

</details>

## Create Proof Request <a href="#create-proof-request" id="create-proof-request"></a>

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

### Parameters <a href="#create-proof-request-parameters" id="create-proof-request-parameters"></a>

<table data-full-width="true"><thead><tr><th width="124">Name</th><th width="86">In</th><th width="97">Type</th><th width="119">Required</th><th>Description</th></tr></thead><tbody><tr><td>attributes</td><td>body</td><td>object</td><td>false</td><td>Requested attribute specifications of proof request</td></tr><tr><td>name</td><td>body</td><td>string</td><td>false</td><td>Proof request name, will be shown to the holder</td></tr><tr><td>nonce</td><td>body</td><td>string</td><td>false</td><td>Nonce or challenge for the presentation to match</td></tr></tbody></table>

### Responses <a href="#create-proof-request-responses" id="create-proof-request-responses"></a>

<table data-full-width="true"><thead><tr><th width="104">Status</th><th width="146">Meaning</th><th width="307">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and returns a Verifiable Presentation.</td><td><a href="index.html.md#schemaverifiablepresentation">VerifiablePresentation</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid/insufficient parameters.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>401</td><td><a href="https://tools.ietf.org/html/rfc7235#section-3.1">Unauthorized</a></td><td>The request was unsuccessful, either because of a missing/invalid auth header or you don't own the DID.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /proof-requests REQUEST PAYLOAD</summary>

```json
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

</details>

<details>

<summary>POST /proof-requests REQUEST CURL</summary>

```bash
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

</details>

<details>

<summary>200 Response</summary>

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

</details>

## List Proof Requests

Return a list of all proof requests and their verification status

### Parameters <a href="#list-proof-requests-parameters" id="list-proof-requests-parameters"></a>

<table data-full-width="true"><thead><tr><th width="109">Name</th><th width="98">In</th><th width="109">Type</th><th width="125">Required</th><th>Description</th></tr></thead><tbody><tr><td>offset</td><td>query</td><td>integer</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

### Responses <a href="#list-proof-requests-responses" id="list-proof-requests-responses"></a>

<table data-full-width="true"><thead><tr><th width="123">Status</th><th width="111">Meaning</th><th width="349">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return all proof requests created by the user.</td><td>Inline</td></tr></tbody></table>

<details>

<summary>GET /proof-requests REQUEST CURL</summary>

```bash
curl --location --request GET https://api.dock.io/proof-requests/ \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --header 'Content-Type: application/json' \
  --data-raw'{

  }'

```

</details>

<details>

<summary>200 Response</summary>

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

</details>

## Get Proof Request

Get the details of an existing proof request and its verification status.

### Parameters <a href="#get-proof-request-parameters" id="get-proof-request-parameters"></a>

<table data-full-width="true"><thead><tr><th width="103">Name</th><th width="87">In</th><th width="114">Type</th><th width="157">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td>UUID</td><td>true</td><td>Proof request UUID</td></tr></tbody></table>

### Responses <a href="#get-proof-request-responses" id="get-proof-request-responses"></a>

<table data-full-width="true"><thead><tr><th width="99">Status</th><th width="125">Meaning</th><th width="353">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return the proof request.</td><td><a href="index.html.md#schemaregistry">Registry</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>The request was unsuccessful, because the proof request was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /proof-requests/{id} REQUEST CULR</summary>

```bash
curl --location --request GET https://api.dock.io/proof-requests/{id} \
  --header 'DOCK-API-TOKEN: API_KEY' \
  --data-raw ''
```

</details>

<details>

<summary>200 Response</summary>

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

</details>

## List Proof Request Templates

When working with Proof Requests you will often want to request the same information from holders. To make this easier you can create Proof Request Templates to define the contents of the proof requests to be re-used.

### Parameters <a href="#get__proof-templates-parameters" id="get__proof-templates-parameters"></a>

<table data-full-width="true"><thead><tr><th width="102">Name</th><th width="89">In</th><th width="136">Type</th><th width="100">Required</th><th>Description</th></tr></thead><tbody><tr><td>offset</td><td>query</td><td>integer(int32)</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer(int32)</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

### Responses <a href="#get__proof-templates-responses" id="get__proof-templates-responses"></a>

<table data-full-width="true"><thead><tr><th width="109">Status</th><th width="103">Meaning</th><th width="301">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>A paged array of proof templates</td><td><a href="index.html.md#schemaproofrequests">ProofRequests</a></td></tr></tbody></table>

<details>

<summary>GET /proof-templates REQUEST CURL</summary>

```bash
# You can also use wget
curl -X GET https://api-testnet.dock.io/proof-templates \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>200 Response</summary>

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

</details>

## Create Proof Request Template

### Parameters <a href="#post__proof-templates-parameters" id="post__proof-templates-parameters"></a>

<table data-full-width="true"><thead><tr><th width="95">Name</th><th width="82">In</th><th width="143">Type</th><th width="130">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td><a href="index.html.md#schemaproofrequest">ProofRequest</a></td><td>true</td><td>Proof template object</td></tr></tbody></table>

### Responses <a href="#post__proof-templates-responses" id="post__proof-templates-responses"></a>

<table data-full-width="true"><thead><tr><th width="104">Status</th><th width="135">Meaning</th><th width="248">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Proof request template created</td><td><a href="index.html.md#schemaprooftemplateobject">ProofTemplateObject</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>Invalid parameters</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.2">Payment Required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /proof-templates REQUEST CURL</summary>

```bash
# You can also use wget
curl -X POST https://api-testnet.dock.io/proof-templates \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>Body parameter</summary>

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

</details>

<details>

<summary>200 Response</summary>

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

</details>

## Get Proof Template History

Get all of the previously created proof requests based on the specified template.

### Parameters <a href="#get__proof-templates_-id-_history-parameters" id="get__proof-templates_-id-_history-parameters"></a>

<table data-full-width="true"><thead><tr><th width="105">Name</th><th width="103">In</th><th>Type</th><th width="107">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td>string(uuid)</td><td>true</td><td>Proof template UUID</td></tr><tr><td>offset</td><td>query</td><td>integer(int32)</td><td>false</td><td>How many items to offset by for pagination</td></tr><tr><td>limit</td><td>query</td><td>integer(int32)</td><td>false</td><td>How many items to return at one time (max 64)</td></tr></tbody></table>

### Responses <a href="#get__proof-templates_-id-_history-responses" id="get__proof-templates_-id-_history-responses"></a>

<table data-full-width="true"><thead><tr><th width="118">Status</th><th width="134">Meaning</th><th width="294">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Returns the information about the proof request history</td><td><a href="index.html.md#schemaproofrequests">ProofRequests</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>Proof template was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /proof-templates/{id}/history REQUEST CURL</summary>

```bash
# You can also use wget
curl -X GET https://api-testnet.dock.io/proof-templates/{id}/history \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>200 Response</summary>

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

</details>

## Create Proof Request from a Template

Create a proof requtest based on the specified template.

### Parameters <a href="#post__proof-templates_-id-_request-parameters" id="post__proof-templates_-id-_request-parameters"></a>

<table><thead><tr><th width="126">Name</th><th width="96">In</th><th width="127">Type</th><th width="112">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td>object</td><td>true</td><td>Specify optional nonce and domain</td></tr><tr><td>» nonce</td><td>body</td><td>string</td><td>false</td><td>none</td></tr><tr><td>» domain</td><td>body</td><td>string</td><td>false</td><td>none</td></tr><tr><td>id</td><td>path</td><td>string(uuid)</td><td>true</td><td>Proof template UUID</td></tr></tbody></table>

### Responses <a href="#post__proof-templates_-id-_request-responses" id="post__proof-templates_-id-_request-responses"></a>

<table><thead><tr><th width="117">Status</th><th width="170">Meaning</th><th width="269">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Returns the information about the proof request</td><td><a href="index.html.md#schemaproofrequestobject">ProofRequestObject</a></td></tr><tr><td>402</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.2">Payment Required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>Proof template was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /proof-templates/{id}/request REQUEST CURL</summary>

```bash
# You can also use wget
curl -X POST https://api-testnet.dock.io/proof-templates/{id}/request \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>Body parameter</summary>

```json
{
  "nonce": "string",
  "domain": "string"
}
```

</details>

<details>

<summary>200 Response</summary>

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

</details>

## Get Proof Template

Get the details about a specific template.

{% hint style="warning" %}
To perform this operation, you must be authenticated by means of one of the following methods: accessToken, bearerAuth, rapidAPI
{% endhint %}

### Parameters <a href="#get__proof-templates_-id-parameters" id="get__proof-templates_-id-parameters"></a>

<table><thead><tr><th width="105">Name</th><th width="108">In</th><th width="131">Type</th><th width="121">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td>string(uuid)</td><td>true</td><td>Proof template UUID</td></tr></tbody></table>

### Responses <a href="#get__proof-templates_-id-responses" id="get__proof-templates_-id-responses"></a>

<table><thead><tr><th width="120">Status</th><th width="124">Meaning</th><th width="298">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Returns the information about the proof templates</td><td><a href="index.html.md#schemaprooftemplateobject">ProofTemplateObject</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>Proof templates was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>GET /proof-templates/{id} REQUEST CURL</summary>

```bash
# You can also use wget
curl -X GET https://api-testnet.dock.io/proof-templates/{id} \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>200 Response</summary>

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

</details>

## Update Proof Template

### Parameters <a href="#patch__proof-templates_-id-parameters" id="patch__proof-templates_-id-parameters"></a>

<table><thead><tr><th width="97">Name</th><th width="102">In</th><th width="157">Type</th><th width="115">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td><a href="index.html.md#schemaproofrequest">ProofRequest</a></td><td>true</td><td>Proof template object</td></tr><tr><td>id</td><td>path</td><td>string(uuid)</td><td>true</td><td>Proof template UUID</td></tr></tbody></table>

### Responses <a href="#patch__proof-templates_-id-responses" id="patch__proof-templates_-id-responses"></a>

<table><thead><tr><th width="106">Status</th><th width="178">Meaning</th><th width="271">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Profile has been updated</td><td><a href="index.html.md#schemaprooftemplateobject">ProofTemplateObject</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>Error creating profile</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.2">Payment Required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>Proof templates was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>PATCH /proof-templates/{id} REQUEST CURL</summary>

```bash
# You can also use wget
curl -X PATCH https://api-testnet.dock.io/proof-templates/{id} \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>Body parameter</summary>

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

</details>

<details>

<summary>200 Response</summary>

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

</details>

## Delete Proof Template

Deletes the specified template and any associated data.

### Parameters <a href="#delete__proof-templates_-id-parameters" id="delete__proof-templates_-id-parameters"></a>

<table><thead><tr><th width="102">Name</th><th width="79">In</th><th width="138">Type</th><th width="113">Required</th><th>Description</th></tr></thead><tbody><tr><td>id</td><td>path</td><td>string(uuid)</td><td>true</td><td>Proof template UUID</td></tr></tbody></table>

### Responses <a href="#delete__proof-templates_-id-responses" id="delete__proof-templates_-id-responses"></a>

<table><thead><tr><th width="115">Status</th><th width="140">Meaning</th><th width="318">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>Proof templates will be deleted</td><td>None</td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>Something went wrong.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr><tr><td>404</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.4">Not Found</a></td><td>Proof templates was not found.</td><td><a href="index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>DELETE /proof-templates/{id} REQUEST CURL</summary>

```bash
# You can also use wget
curl -X DELETE https://api-testnet.dock.io/proof-templates/{id} \
  -H 'Accept: application/json' \
  -H 'DOCK-API-TOKEN: API_KEY'

```

</details>

<details>

<summary>400 Response</summary>

```json
{
  "status": 0,
  "type": "string",
  "message": "string"
}
```

</details>
