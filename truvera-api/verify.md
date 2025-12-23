# Verify

## VCDM verification

VCDM verification is usually done in context of a presentation request as [documented with the presentations endpoint](presentations/). You probably do not want to call the verify endpoint directly.

This route allows manual verification of issued/received credentials and presentations. Verification will check that the JSON-LD document's cryptographic proof is correct and that it has not been revoked. It will return a verification status with a boolean verified result.

A verifier upon receiving a verifiable presentation verifies the validity of each credential in the presentation. This includes checking the correctness of the data model of the credential, the authenticity by verifying the issuer's signature and revocation status if the credential is revocable. It then checks whether the presentation contains the signature from the holder on the presentation, including the given challenge.

### Parameters <a href="#verify-a-credential-or-presentation-parameters" id="verify-a-credential-or-presentation-parameters"></a>

<table data-full-width="false"><thead><tr><th width="106">Name</th><th width="82">In</th><th width="205">Type</th><th width="89">Required</th><th>Description</th></tr></thead><tbody><tr><td>body</td><td>body</td><td><a href="../developer-documentation/dock-api/index.html.md#schemaverifiablecredential">VerifiableCredential</a> or <a href="../developer-documentation/dock-api/index.html.md#schemaverifiablepresentation">VerifiablePresentation</a></td><td>true</td><td>Provide as the body a verifiable credential or verifiable presentation JSON-LD document.</td></tr></tbody></table>



{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/verify" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}
