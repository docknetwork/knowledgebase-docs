# Sub-accounts

Sub-accounts are a feature of the Dock Certs API that allows Dock enterprise customers to segregate their data within Dock's platform based on their own customers. Each sub-account can have its own keys, organization profiles, credential designs and verification templates conviently organized to help with tracking and auditing of the activity performed by each.

<figure><img src="../../.gitbook/assets/sub-accounts-cdf773cc.png" alt=""><figcaption></figcaption></figure>

When using a sub-account the parent account will set up separate API keys for each sub-account and then use the sub-account specific API key for the transactions associated with that sub-account.&#x20;

In order to easier manage sub-account assets [Ecosystem Tools](ecosystem-tools/) can be used.

### Sample sub-account Postman collection

Download the collection [here](../../Postman\_collections/Subaccounts).

This Postman collection shows a simple example of sub-account set up in 5 steps:

1. Creating a sub-account
2. Creating an API key for a sub-account
3. Creating a DID for the sub-account
4. Inviting sub-account as a participant in an already existing ecosystem
5. Accepting the invite

## Create sub-account

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/subaccounts" method="post" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## List sub-accounts

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/subaccounts" method="get" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## Get sub-account by ID

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/subaccounts/{id}" method="get" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}

## Update the specified sub-account

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/subaccounts/{id}" method="patch" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}



## Deletes the specified sub-account

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/subaccounts/{id}" method="delete" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}



## Get sub-account usage

Get details about the activity that this sub-account has performed in the system.

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/subaccounts/{id}/usage" method="get" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}



## Create sub-account API key

Creates an API key for a sub-account. In order for activity to be associated with the given sub-account an API key needs to be created for that sub-account and then that key must be used for all transactions related to that sub-account.

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/subaccounts/{id}/keys" method="post" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}



## List sub-account API keys

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/subaccounts/{id}/keys" method="get" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}



## Delete a sub-account API key

Delete the specified API key for the given sub-account.

{% swagger src="https://swagger.api.dock.io/openapi.yaml" path="/subaccounts/{id}/keys/{keyId}" method="delete" %}
[https://swagger.api.dock.io/openapi.yaml](https://swagger.api.dock.io/openapi.yaml)
{% endswagger %}
