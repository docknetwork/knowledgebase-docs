# Verify

## VCDM Verification

A verifier upon receiving a verifiable presentation verifies the validity of each credential in the presentation. This includes checking the correctness of the data model of the credential, the authenticity by verifying the issuer's signature and revocation status if the credential is revocable. It then checks whether the presentation contains the signature from the holder on the presentation, including his given challenge.

You can verify issued/received credentials and presentations using this route. Verification will check that the JSON-LD document's cryptographic proof is correct and that it has not been revoked. It will return a verification status with a boolean verified result.

### Parameters <a href="#verify-a-credential-or-presentation-parameters" id="verify-a-credential-or-presentation-parameters"></a>

<table data-full-width="false"><thead><tr><th width="106">Name</th><th width="82">In</th><th width="205">Type</th><th width="89">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td><a href="../developer-documentation/dock-api/index.html.md#schemaverifiablecredential">VerifiableCredential</a> or <a href="../developer-documentation/dock-api/index.html.md#schemaverifiablepresentation">VerifiablePresentation</a></td><td>true</td><td>Provide as the body a Verifiable Credential or Verifiable Presentation JSON-LD document.</td></tr></tbody></table>

{% swagger src="https://swagger-api.truvera.io/openapi.yaml" path="/verify" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endswagger %}



