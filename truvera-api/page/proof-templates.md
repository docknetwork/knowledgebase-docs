# Proof templates

To verify a credential verifier will need to create a proof template and generate a proof request to which the holder wallet will provide the verifiable presentation. Verifiable presentations can not be done via the API, the [credential SDK](https://github.com/docknetwork/sdk) is needed to create a presentation.&#x20;

When working with proof requests you will often want to request the same information from holders. To make this easier you can create proof request templates to define the contents of the proof requests to be re-used.

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
Use the Verified  parameter when needing to get only those verifications that were succsessful.&#x20;
{% endhint %}

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}/history" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



## Delete a proof template

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



## Delete history for proof template

This endpoint provides an irreversible deletion of all of proof template's verification history data.&#x20;

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}/history" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



## Delete a proof template

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



