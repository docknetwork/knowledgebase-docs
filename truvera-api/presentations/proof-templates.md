# Proof templates

It is common to repeatedly request the same information from holders in subsequent proof requests. The Truvera API makes this easy by allowing you to create proof request templates to define the contents of the proof requests in a way that can be reused. The [Truvera Workspace](../../workspace/verify-credentials.md) refers to proof request templates as "verification templates".

To verify a credential with Truvera, the verifier will need to create a proof template and generate a proof request to which the holder wallet will provide the verifiable presentation. Verifiable presentations can not be created via the REST API, as [the Truvera Wallet SDK](../../credential-wallet/wallet-sdk/) should be used.

## Create a proof template <a href="#create-proof-request" id="create-proof-request"></a>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Get proof templates <a href="#create-proof-request" id="create-proof-request"></a>

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Get details of a specific proof template

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Update a proof template

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}" method="patch" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Get proof requests from template

{% hint style="info" %}
Use the Verified parameter when needing to get only those verifications that were succsessful.
{% endhint %}

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}/history" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Delete a proof template

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Delete history for a proof template

This endpoint provides an irreversible deletion of all of proof template's verification history data.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}/history" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Delete a proof template

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}
