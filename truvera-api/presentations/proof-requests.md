# Proof requests

Proof templates are used to create proof requests. When a proof request is created, you will receive a URL which needs to be displayed in a QR code for a wallet application to scan.&#x20;

## Create proof request <a href="#create-proof-request" id="create-proof-request"></a>

This route uses a template ID and takes the PEX request you defined there.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-templates/{id}/request" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Create proof request <a href="#create-proof-request" id="create-proof-request"></a>

This route lets you create a standalone proof request without storing a verification template first.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-requests" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Get all proof requests

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-requests" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



## Get the details of an existing proof request

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-requests/{id}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Delete the proof request

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/proof-requests/{id}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}



