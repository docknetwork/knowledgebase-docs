# OpenID

OpenID issuance is the best way to go, when you need to send the credential to the holder using a deeplink or QR code.

OpenID issuer endpoint should not be confused with the credential Issuer as it is in the Truvera platform. With OpenID creating an OpenID issuer is the first step of credential issuance and will need to be done for each individual credential.&#x20;

{% openapi src="../../.gitbook/assets/updated_openapi.yaml" path="/openid/issuers" method="post" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endopenapi %}

### Credential offers

Generate credential offers to initiate the issuance process. Credential offers can be shared with the holder to claim the credential. This endpoint creates a credential offer linked to the OpenID issuer.

{% openapi src="../../.gitbook/assets/updated_openapi.yaml" path="/openid/credential-offers" method="post" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endopenapi %}



{% openapi src="../../.gitbook/assets/updated_openapi.yaml" path="/openid/issuers" method="get" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endopenapi %}



{% openapi src="../../.gitbook/assets/updated_openapi.yaml" path="/openid/issuers/{id}" method="get" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endopenapi %}



{% openapi src="../../.gitbook/assets/updated_openapi.yaml" path="/openid/issuers/{id}" method="delete" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/updated_openapi.yaml" path="/openid/vp/{id}/request" method="get" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endopenapi %}

{% openapi src="../../.gitbook/assets/updated_openapi.yaml" path="/openid/vp/{id}/request-url" method="post" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endopenapi %}



