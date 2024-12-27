# Issue Store Verify Sample flow

This flow refers to Postman, but the general steps are the same however you use the API. The Issue Store Verify collection includes the scripts that automatically propagate results into the next request bodies when you follow the below steps.&#x20;

Download the sample collection [here](../../Postman_collections/Issue-Store-Verify%20flow).

To issue a credential and or a presentation on the holder's behalf, the following steps are required:

## 1. Create a DID

To create a new DID to issue with, go to **Create DID** and click **Send**. The `id` property denotes a job ID in the system that you can use to query for blockchain transaction status.

The Truvera API supports `did:dock`, `did:polygonid` and `did:key` method creation.

<details>

<summary>Body</summary>

```json
{
"type": "dock"
}
```

</details>

<details>

<summary>200 Response</summary>

```json
{
    "did": "did:dock:5CvswSAkWbyn6iQdRtMiD8tUAQmpXBghPVs9JqK5cJTiAhJk",
    "controller": "did:dock:5CvswSAkWbyn6iQdRtMiD8tUAQmpXBghPVs9JqK5cJTiAhJk",
    "id": "23677",
    "data": {
        "did": "did:dock:5CvswSAkWbyn6iQdRtMiD8tUAQmpXBghPVs9JqK5cJTiAhJk",
        "controller": "did:dock:5CvswSAkWbyn6iQdRtMiD8tUAQmpXBghPVs9JqK5cJTiAhJk"
    }
}
```

</details>

{% hint style="info" %}
Creating a Dock DID submits a transaction to the blockchain, this could take some time to process. Please hit the \`/jobs\` endpoint to check the status of the job to see if it's finalized or not.
{% endhint %}

{% hint style="info" %}
When creating a Polygon ID DID, be sure to set the \`keyType\` field to \`bjj\`.
{% endhint %}

## 2. Update the DID

To add information about your Organization to the DID, e.g. name and logo, you will need to update the DID profile.&#x20;

<details>

<summary>Body</summary>

```json
{
    "did":"did:dock:5CfsgqHioKCHNddVK9Y2Lu8fHQpvXh3nc9xVjLZNDqk1ZJ9z",
    "name": "Postman Test",
    "logo":""
}
```

</details>

<details>

<summary>200 Response</summary>

```json
{
    "did": "did:dock:5CfsgqHioKCHNddVK9Y2Lu8fHQpvXh3nc9xVjLZNDqk1ZJ9z",
    "name": "Postman Test",
    "logo": ""
}
```

</details>

{% hint style="info" %}
You only need to create a DID once and then you can issue many credentials with it. A subject/holder DID should not be the same as the issuer DID in a real world credential.
{% endhint %}

## 3. Create a Schema

To issue a credential you will need to set a schema that will define which attributes need to be included in the credential.

<details>

<summary>Body</summary>

```json
{
      "$schema": "http://json-schema.org/schema",
      "name": "Postman test schema",
      "description": "describing Postman test schema",
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
    }
```

</details>

<details>

<summary>200 Response</summary>

```json
{
    "id": "0",
    "data": {
        "schema": {
            "$schema": "http://json-schema.org/schema",
            "name": "Postman test schema",
            "description": "describing VPI test schema",
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
            "$metadata": {
                "version": 1,
                "uris": {
                    "jsonSchema": "https://schema.dock.io/PostmanTestSchema-V1-1723810163796.json",
                    "jsonLdContext": "https://schema.dock.io/PostmanTestSchema-V1723810163796.json-ld"
                }
            },
            "$id": "https://schema.dock.io/PostmanTestSchema-V1-1723810163796.json"
        },
        "id": "https://schema.dock.io/PostmanTestSchema-V1-1723810163796.json",
        "uri": "https://schema.dock.io/PostmanTestSchema-V1-1723810163796.json",
        "created": "2024-08-16T12:09:23.911Z",
        "isOwner": true,
        "ownerName": "",
        "ownerLogo": ""
    }
}
```

</details>

## 4. Issue a verifiable credential

To create a Verifiable Credential using the the new issuer DID, update Issuer with the DID you have created in the first step and add the required information to the attributes. It will return a Verifiable Credential that conforms to the W3C spec.

<details>

<summary>Body</summary>

```json
{
  "persist": true,
  "password": "1234",
  "anchor": false,
  "recipientEmail":"agne@truvera.io",
  "distribute": true,
  "format": "jsonld",
  "credential": {
    "name": "VPI test credential",
    "description": "describing vpi test credential",
    "schema": "https://schema.dock.io/VPITestSchema-V1-1723546475527.json",
    "type": [
      "VPITestSchema"
    ],
    "subject": {
        "id":"agne@truvera.io",
        "emailAddress":"agne@truvera.io",
        "alumniOf":"University of Vilnius"
    },
    "issuer": "did:dock:5DciJXakYFsCfpFzQzrHCdoRvRwi1gu2uUGJnys5Aj4cvWUx",
    "issuanceDate": "2024-08-13T11:03:35.610Z"
   }
}
```

</details>

<details>

<summary>200 Response</summary>

```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        {
            "VPITestSchema": "dk:VPITestSchema",
            "alumniOf": "dk:alumniOf",
            "description": "http://schema.org/description",
            "dk": "https://ld.dock.io/credentials#",
            "emailAddress": "dk:emailAddress",
            "name": "dk:name"
        }
    ],
    "id": "https://creds-testnet.dock.io/43800063042edf33e7092653e487aeb795e528d24664be5ea641b62f279dc69d",
    "type": [
        "VerifiableCredential",
        "VPITestSchema"
    ],
    "credentialSubject": {
        "id": "agne@truvera.io",
        "emailAddress": "agne@truvera.io",
        "alumniOf": "University of Vilnius"
    },
    "issuanceDate": "2024-08-13T11:03:35.610Z",
    "issuer": {
        "name": "VPI test issuer",
        "id": "did:dock:5DciJXakYFsCfpFzQzrHCdoRvRwi1gu2uUGJnys5Aj4cvWUx"
    },
    "credentialSchema": {
        "id": "https://schema.dock.io/VPITestSchema-V1-1723546475527.json",
        "type": "JsonSchemaValidator2018"
    },
    "name": "VPI test credential",
    "description": "describing vpi test credential",
    "proof": {
        "type": "Ed25519Signature2018",
        "created": "2024-08-16T12:14:55Z",
        "verificationMethod": "did:dock:5DciJXakYFsCfpFzQzrHCdoRvRwi1gu2uUGJnys5Aj4cvWUx#keys-1",
        "proofPurpose": "assertionMethod",
        "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..IbZADG6nhKe7lSHUuQ4OyEAToeGybN7nYl2Pp8rsUzc-oVAKYzBzZX2gMM8Bj4Np1cNK9WvpjlyRWjgVviz_Bg"
    }
}
```

</details>



## 5. Import the credential into the wallet

[Download Truvera wallet ](../../credential-wallet/download-truvera-wallet.md)and click on the email link that was sent when issuing the credential. If not using the email distribution download the json of the credential an import it to the wallet using the json import option.

<div align="left"><figure><img src="../../.gitbook/assets/1723811020918.jpeg" alt="" width="188"><figcaption></figcaption></figure></div>

## 5. Create a proof template

To verify a credential you will need a verification template, that will indicate which attributes need to be fulfilled for successful verification. Verification templates can be reused.

<details>

<summary>Body</summary>

```json
{
  "name": "Postman proof request",
  "nonce": "1234567890",
  "request": {
    "name": "test request",
    "purpose": "my purpose",
    "input_descriptors": [
      {
        "id": "Credential 1",
        "name": "test request",
        "purpose": "my purpose",
        "constraints": {
          "fields": [
            {
                "path": [
                    "$.credentialSubject.alumniOf"
                ]
            },
            {
            "path": [
                "$.credentialSubject.dateIssued"
                ],
                "optional": true
            },
            {
                "path": [
                        "$.credentialSchema.id"
                ],
                "filter": {
                    "const": "https://schema.dock.io/PostmanTestSchemaJune18-V1-1718711073065.json"
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

<details>

<summary>200 Response</summary>

```json
{
    "id": "acbff85d-a556-4832-b118-2194c51d3401",
    "did": "",
    "name": "Postman proof request",
    "created": "2024-08-16T12:28:00.638Z",
    "updated": "2024-08-16T12:28:00.638Z",
    "request": {
        "name": "test request",
        "purpose": "my purpose",
        "input_descriptors": [
            {
                "id": "Credential 1",
                "name": "test request",
                "purpose": "my purpose",
                "constraints": {
                    "fields": [
                        {
                            "path": [
                                "$.credentialSubject.alumniOf"
                            ]
                        },
                        {
                            "path": [
                                "$.credentialSubject.dateIssued"
                            ],
                            "optional": true
                        },
                        {
                            "path": [
                                "$.credentialSchema.id"
                            ],
                            "filter": {
                                "const": "https://schema.dock.io/PostmanTestSchemaJune18-V1-1718711073065.json"
                            }
                        }
                    ]
                }
            }
        ]
    },
    "totalRequests": 0
}
```

</details>

## 6. Create a proof presentation

Using the verification template created in the previous step in the endpoint **POST/proof-templates/{id}/** request a single use verification or proof presentation will be created.&#x20;

<details>

<summary>200 Response</summary>

```json
{
    "id": "806be681-494c-4483-bf49-e1aee96473d9",
    "name": "Postman proof request",
    "nonce": "f3db4810cd8bf8df17bb04ace82dee36",
    "did": "",
    "verified": false,
    "created": "2024-08-16T12:33:32.867Z",
    "updated": "2024-08-16T12:33:32.867Z",
    "signature": null,
    "presentation": {},
    "response_url": "https://api-testnet.dock.io/proof-requests/806be681-494c-4483-bf49-e1aee96473d9/send-presentation",
    "type": "proof-request",
    "qr": "https://creds-testnet.dock.io/proof/806be681-494c-4483-bf49-e1aee96473d9",
    "request": {
        "name": "test request",
        "purpose": "my purpose",
        "input_descriptors": [
            {
                "id": "Credential 1",
                "name": "test request",
                "purpose": "my purpose",
                "constraints": {
                    "fields": [
                        {
                            "path": [
                                "$.credentialSubject.alumniOf"
                            ]
                        },
                        {
                            "path": [
                                "$.credentialSubject.dateIssued"
                            ],
                            "optional": true
                        },
                        {
                            "path": [
                                "$.credentialSchema.id"
                            ],
                            "filter": {
                                "const": "https://schema.dock.io/PostmanTestSchemaJune18-V1-1718711073065.json"
                            }
                        }
                    ]
                }
            }
        ],
        "id": "806be681-494c-4483-bf49-e1aee96473d9"
    }
}
```

</details>

{% hint style="info" %}
The proof request is one time use so that the information from the credential can be associated to a specific transaction event. However, the proof template can be used as many times as needed.&#x20;

If there is a need to have a static QR code for multiple verification, a small service can be created to make proof requests from the verification template as and when needed.
{% endhint %}

## 7. Verify the Presentation

Scan the QR code from the proof presentation using your wallet to verify the credential.

