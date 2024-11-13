# Profiles

Organization Profiles are used to provide more context for an Issuer DID. Details about the issuer such as name and logo can be added using a Organization Profile. These details will be included in credentials that are issued by the DID.

## Create Profile

The `did` and `name` fields are required to create a new Profile.

{% swagger src="../../.gitbook/assets/updated_openapi.yaml" path="/profiles" method="post" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endswagger %}

## Get Profile

When a DID is provided in the path, the API will retrieve the Profile associated with that DID.

{% swagger src="../../.gitbook/assets/updated_openapi.yaml" path="/profiles/{did}" method="get" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endswagger %}



## List Profiles

Return a list of all Profiles that your user account controls.

{% swagger src="../../.gitbook/assets/updated_openapi.yaml" path="/profiles" method="get" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endswagger %}

## Update Profile

The update profile operation means that you can update the details of the profile. To do so, you need to provide a different value for **at least** one of `name`, `description` or `logo`.

{% swagger src="../../.gitbook/assets/updated_openapi.yaml" path="/profiles/{did}" method="patch" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endswagger %}

## Delete Profile

Deletes a profile from our platform. It does NOT delete the associated DID, nor revoke the credentials issued for the profile.

{% swagger src="../../.gitbook/assets/updated_openapi.yaml" path="/profiles/{did}" method="delete" %}
[updated_openapi.yaml](../../.gitbook/assets/updated_openapi.yaml)
{% endswagger %}
