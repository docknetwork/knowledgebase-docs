# Profiles

Organization profiles are used to provide more context for an Issuer DID. Details about the issuer such as name and logo can be added using a organization profile. These details will be included in credentials that are issued by the DID.

## Create profile

The `did` and `name` fields are required to create a new Profile.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/profiles" method="post" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Get profile

When a DID is provided in the path, the API will retrieve the profile associated with that DID.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/profiles/{did}" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## List profiles

Return a list of all profiles that your user account controls.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/profiles" method="get" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Update profile

The update profile operation means that you can update the details of the profile. To do so, you need to provide a different value for **at least** one of `name`, `description` or `logo`.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/profiles/{did}" method="patch" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}

## Delete profile

Deletes a profile from our platform. It does NOT delete the associated DID, nor revoke the credentials issued for the profile.

{% openapi src="https://swagger-api.truvera.io/openapi.yaml" path="/profiles/{did}" method="delete" %}
[https://swagger-api.truvera.io/openapi.yaml](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi %}
