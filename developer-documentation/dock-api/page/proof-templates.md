# Proof templates

To verify a credential verifier will need to create a proof template and generate a proof request to which the holder wallet will provide the verifiable presentation. Verifiable presentations can not be done via the API, the [credential SDK](https://github.com/docknetwork/sdk) is needed to create a presentation.&#x20;

## Create a proof template <a href="#create-proof-request" id="create-proof-request"></a>

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/proof-templates" method="post" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## Get proof templates <a href="#create-proof-request" id="create-proof-request"></a>

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/proof-templates" method="get" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## Get details of a specific proof template

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/proof-templates/{id}" method="get" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## Update a proof template

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/proof-templates/{id}" method="patch" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## Get proof requests from template

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/proof-templates/{id}/history" method="get" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## Delete history for proof template

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/proof-templates/{id}/history" method="delete" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## Delete a proof template

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/proof-templates/{id}" method="delete" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

