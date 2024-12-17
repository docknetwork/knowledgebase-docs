# Verify

## VCDM Verification

A verifier upon receiving a verifiable presentation verifies the validity of each credential in the presentation. This includes checking the correctness of the data model of the credential, the authenticity by verifying the issuer's signature and revocation status if the credential is revocable. It then checks whether the presentation contains the signature from the holder on the presentation, including his given challenge.

You can verify issued/received credentials and presentations using this route. Verification will check that the JSON-LD document's cryptographic proof is correct and that it has not been revoked. It will return a verification status with a boolean verified result.

### Parameters <a href="#verify-a-credential-or-presentation-parameters" id="verify-a-credential-or-presentation-parameters"></a>

<table data-full-width="false"><thead><tr><th width="106">Name</th><th width="82">In</th><th width="205">Type</th><th width="89">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td><a href="../dock-api/index.html.md#schemaverifiablecredential">VerifiableCredential</a> or <a href="../dock-api/index.html.md#schemaverifiablepresentation">VerifiablePresentation</a></td><td>true</td><td>Provide as the body a Verifiable Credential or Verifiable Presentation JSON-LD document.</td></tr></tbody></table>

### Responses <a href="#verify-a-credential-or-presentation-responses" id="verify-a-credential-or-presentation-responses"></a>

<table data-full-width="false"><thead><tr><th width="114">Status</th><th width="178">Meaning</th><th width="278">Description</th><th>Schema</th></tr></thead><tbody><tr><td>200</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.3.1">OK</a></td><td>The request was successful and will return the verification result.</td><td><a href="../dock-api/index.html.md#schemaverificationresponse">VerificationResponse</a></td></tr><tr><td>400</td><td><a href="https://tools.ietf.org/html/rfc7231#section-6.5.1">Bad Request</a></td><td>The request was unsuccessful, because of invalid credential params.</td><td><a href="../dock-api/index.html.md#schemaerror">Error</a></td></tr><tr><td>402</td><td><a href="https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/402">Payment required</a></td><td>Transaction limit reached or upgrade required to proceed</td><td><a href="../dock-api/index.html.md#schemaerror">Error</a></td></tr></tbody></table>

<details>

<summary>POST /verify REQUEST PAYLOAD</summary>

```json

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

</details>

<details>

<summary>POST /verify REQUEST CURL</summary>

```bash
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

</details>

<details>

<summary>200 Response</summary>

```json
{
  "verified": true,
  "results": [...]
}
```

</details>

