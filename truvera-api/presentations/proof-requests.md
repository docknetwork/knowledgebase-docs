# Proof requests

[Proof templates](proof-templates.md) are used to create proof requests. When a proof request is created, you will receive a URL which needs to be delivered to a holder's wallet application either as a link (in the "response\_url" field) or displayed in a QR code for the wallet application to scan (conveniently pre-generated for you in the "qr" field). The holder's wallet will then generate a proof response and deliver it to the Truvera API which will check it for cryptographic correctness. [Like other asynchronous operations](../getting-started.md#integration-paradigms), you can receive the verification response along with the verified attributes either by polling or via a webhook.

To get a response by polling, check [the proof-request details](proof-requests.md#get-the-details-of-an-existing-proof-request) for when the "verified" attribute equals "true". At that point, the "presentation" field will contain the verified attributes as a JSON list. If at any point the "verified" attribute equals "false", the response can be checked to determine the cause of the failure and appropriate next steps.

When creating a proof request, you can optionally provide a verifier DID in order for the holder to know that your verifier is on their trust-list, such as in an [ecosystem of trust](../../workspace/ecosystem-tools/).

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
