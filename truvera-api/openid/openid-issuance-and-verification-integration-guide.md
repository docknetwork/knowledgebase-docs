# OpenID Issuance and Verification Integration Guide

This guide provides detailed instructions for implementing OpenID for Verifiable Credential Issuance (OID4VCI) and OpenID for Verifiable Presentation (OID4VP) using a series of API endpoints. It outlines the steps required to set up an issuer, create credential offers, manage the issuance flow, create presentations and verify the issued credentials.&#x20;

## Prerequisites

Before starting, ensure you have:

* **Issuer DID** (`did:dock:issuer`): The did for the credential issuer.
* **Verifier DID** (`did:dock:verifier`): The did for the credential verifier.
* **Holder DID** (`did:key:holder`): The DID for the credential holder (optional)

Download and use our [Postman Collections](../../Postman_collections/OID4VC%20and%20OID4VP%20testing) to experiment with OpenID standards based credentials.

## Set Up an OID4VCI Issuer

Create an OID4VCI issuer with the necessary configurations, including claim mappings, credential options, and authentication provider settings.

<mark style="color:green;">`POST`</mark> /openid/issuers

This endpoint creates an OID4VCI issuer. "authProvider" and "claimMap" are supplied as part of the [Authorization Code Flow](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html#name-authorization-code-flow). It can be omitted for the [Pre-Authorized Code Flow](https://openid.net/specs/openid-4-verifiable-credential-issuance-1_0.html#name-pre-authorized-code-flow).

**Request/Response**

{% tabs %}
{% tab title="Body" %}
```json
 {
    "claimMap": {
      "name": "name"
    },
    "credentialOptions": {
      "credential": {
        "type": ["UniversityDegreeCredential"],
        "context": ["https://www.w3.org/2018/credentials/examples/v1"],
        "subject": {
          "alumniOf": "Truvera University",
          "degree": "Credential Science"
          // name will be added by claims flow
        },
        "expirationDate": "2099-08-24T14:15:22Z",
        "issuer": "did:dock:issuer"
      }
    },
    "authProvider": {
      "url": "https://creds.dock.io/claims",
      "scope": ["openid"],
      "clientId": "eyAic2NoZW1hIjogImh0dHBzOi8vZG9ja25ldHdvcmsuZ2l0aHViLmlvL3ZjLXNjaGVtYXMvYmFzaWMtY3JlZGVudGlhbC5qc29uIiwgImNsYWltcyI6IFsibmFtZSJdIH0=",
      "clientSecret": "gpO2IVK+OALL8W+DcFlIfFhJtNA="
    },
    "singleUse": false
  }
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "id": "{issuerId}",
  "created": "2024-09-20T08:53:50.524Z",
  "updated": "2024-09-20T08:53:50.524Z",
  "credentialOptions": { ... },
  "authProvider": { ... },
  "claimMap": { ... },
  "qrUrl": "openid://discovery?issuer=https://api.example.com/openid/issuers/issuer-id"
}
```
{% endtab %}
{% endtabs %}

### Check the OpenID Issuer Configuration

<mark style="color:green;">`GET`</mark> /openid/issuers/{issuerId}/.well-known/openid-configuration

This endpoint retrieves the OpenID configuration for the specified issuer.

**Request/Response**

{% tabs %}
{% tab title="Response" %}
```json
{
  "issuer": "https://api-testnet.dock.io/openid/issuers/{issuerId}",
  "credential_formats_supported": ["ldp_vc", "jwt"],
  "credential_claims_supported": ["name"],
  "response_types_supported": ["code"],
  "grant_types_supported": ["authorization_code"]
}
```
{% endtab %}
{% endtabs %}

## Create Credential Offers

Generate credential offers to initiate the issuance process. Credential offers can be shared with the holder to claim the credential.

<mark style="color:green;">`POST`</mark> /openid/credential-offers

This endpoint creates a credential offer linked to the OpenID issuer.

**Request/Response**

{% tabs %}
{% tab title="Body" %}
```json
  {
    "id": "{issuerId}"
  }
```
{% endtab %}

{% tab title="Response" %}
```json
{
  "url": "openid-credential-offer://?credential_offer=...",
  "offer": {
    "credential_issuer": "https://api-testnet.dock.io/openid/issuers/{issuerId}",
    "credentials": ["ldp_vc:UniversityDegreeCredential"],
    "grants": {
      "authorization_code": { "issuer_state": "state123" }
    }
  }
}
```
{% endtab %}
{% endtabs %}

## Retrieve and Store Credentials

Using the [Truvera Wallet ](../../credential-wallet/)or any OID4VCI Wallet, scan the QR code received and follow the process to receive the credential.

## Verify Credentials

### Create a new Proof Request&#x20;

This step involves creating a proof request that specifies the requirements for the verifiable presentation. The proof request defines what credentials and claims are expected from the holder.

<mark style="color:green;">`POST`</mark> /proof-requests

This endpoint creates a new proof request that the verifier can use to request credentials from the holder.

**Request/Response**

{% tabs %}
{% tab title="Body" %}
```json
{
      "did": "did:dock:5HCXuyBhXRiZxSmyLG2j6NhoeqL4dYHV9EGwLE2FKJVUmXL4",
	  "name": "OID4VP Proof request 2",
	  "request": {
		"name": "OID4VP test proof request",
		"purpose": "To present a test credential using OID4VPI",
		"input_descriptors": [
		  {
			"id": "Truvera Credential",
			"name": "OID4VP test proof request",
			"purpose": "To present a test credential using OID4VP",
			"constraints": {
			  "fields": [
				{
				  "path": [
					"$.credentialSubject.name"
				  ]
				},
				{
				  "path": [
					"$.type",
					"$.vc.type"
				  ],
				  "filter": {
					"type": "array",
					"contains": {
					  "const": "UniversityDegreeCredential"
					}
				  }
				}
			  ]
			}
		  }
		]
	  }
  }
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "id": "{proofRequestId}",
    "name": "OID4VP Proof request",
    "nonce": "...",
    "did": "did:dock:verifier",
    "verified": false,
    "created": "...",
    "updated": "...",
    "signature": "...",
    "presentation": {},
    "response_url": "...",
    "type": "proof-request",
    "qr": "...",
    "request": {...},
    "types": ["jsonld"]
}
```
{% endtab %}
{% endtabs %}

### Get the request url for the OID4VP

This step generates a request URL that can be shared with the holder. The holder can use this URL to present the requested credentials through their wallet.

<mark style="color:green;">`POST`</mark> /openid/vp/{proofRequestId}/request-url

This endpoint generates a request URL based on the proof request ID. The withRequestURI parameter determines whether the URL includes the request\_uri.

**Request/Response**

{% tabs %}
{% tab title="Body" %}
```json
  {
      "withRequestURI": true
  }
```
{% endtab %}

{% tab title="Response" %}
```json
{
    "url": "openid://?client_id=...&request_uri=..."
}
```
{% endtab %}
{% endtabs %}

### Verify Presentation

Using the [Truvera Wallet ](../../credential-wallet/)or any OID4VP Wallet, scan the QR code received and follow the process to verify the credential.

### Check proof request status

This step involves checking the status of a specific proof request to see if it has been fulfilled, and to retrieve any relevant information associated with the request.

<mark style="color:green;">`GET`</mark> /proof-requests/{proofRequestId}

This endpoint retrieves the status and details of the specified proof request, including whether the requested credentials have been presented and verified

**Request/Response**

{% tabs %}
{% tab title="Response" %}
```json
{
    "id": "{proofRequestId}",
    "name": "OID4VP Proof request",
    "nonce": "...",
    "did": "did:dock:verifier",
    "verified": true,
    "created": "...",
    "updated": "...",
    "signature": "...",
    "presentation": {
	    "holder": "did:dock:holder"
	    ...
    },
    "response_url": "...",
    "type": "proof-request",
    "qr": "...",
    "request": {...},
    "types": ["jsonld"]
}
```
{% endtab %}
{% endtabs %}

