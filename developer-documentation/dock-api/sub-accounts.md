# Sub-accounts

Sub-accounts are a feature of the Dock Certs API that allows Dock enterprise customers to segregate their data within Dock's platform based on their own customers. Each sub-account can have its own keys, organization profiles, credential designs and verification templates conviently organized to help with tracking and auditing of the activity performed by each.

<figure><img src="../../.gitbook/assets/sub-accounts-cdf773cc.png" alt=""><figcaption></figcaption></figure>

When using a sub-account the parent account will set up separate API keys for each sub-account and then use the sub-account specific API key for the transactions associated with that sub-account.&#x20;

In order to easier manage sub-account assets [Ecosystem Tools](ecosystem-tools/) can be used.

### Sample Subaccount Postman Collection

Download the collection here.

This Postman collection shows a simple example of sub-account set up in 5 steps:

1. Creating a subaccount
2. Creating an API key for a subaccount
3. Creating a DID for the subaccount
4. Inviting subaccount as a participant in an already existing ecosystem
5. Accepting the invite

## Create Sub-account

{% swagger src="../../.gitbook/assets/openapi (1) (1).yaml" path="/subaccounts" method="post" %}
[openapi (1) (1).yaml](<../../.gitbook/assets/openapi (1) (1).yaml>)
{% endswagger %}

## List Sub-Accounts

{% swagger src="../../.gitbook/assets/openapi (1) (1).yaml" path="/subaccounts" method="get" %}
[openapi (1) (1).yaml](<../../.gitbook/assets/openapi (1) (1).yaml>)
{% endswagger %}

## Get Sub-Account by ID

{% swagger src="../../.gitbook/assets/openapi (1) (1).yaml" path="/subaccounts/{id}" method="get" %}
[openapi (1) (1).yaml](<../../.gitbook/assets/openapi (1) (1).yaml>)
{% endswagger %}

## Update the specified sub-account

{% swagger src="../../.gitbook/assets/openapi (1) (1).yaml" path="/subaccounts/{id}" method="patch" %}
[openapi (1) (1).yaml](<../../.gitbook/assets/openapi (1) (1).yaml>)
{% endswagger %}

## Deletes the specified sub-account

{% swagger src="../../.gitbook/assets/openapi (1) (1).yaml" path="/subaccounts/{id}" method="delete" %}
[openapi (1) (1).yaml](<../../.gitbook/assets/openapi (1) (1).yaml>)
{% endswagger %}

## Get Sub-Account Usage

Get details about the activity that this sub-account has performed in the system.

{% swagger src="../../.gitbook/assets/openapi (1) (1).yaml" path="/subaccounts/{id}/usage" method="get" %}
[openapi (1) (1).yaml](<../../.gitbook/assets/openapi (1) (1).yaml>)
{% endswagger %}

## Create Sub-Account API Key

Creates an API key for a subaccount. In order for activity to be associated with the given sub-account an API key needs to be created for that sub-account and then that key must be used for all transactions related to that sub-account.

{% swagger src="../../.gitbook/assets/openapi (1) (1).yaml" path="/subaccounts/{id}/keys" method="post" %}
[openapi (1) (1).yaml](<../../.gitbook/assets/openapi (1) (1).yaml>)
{% endswagger %}

## List Sub-Account API Keys

{% swagger src="../../.gitbook/assets/openapi (1) (1).yaml" path="/subaccounts/{id}/keys" method="get" %}
[openapi (1) (1).yaml](<../../.gitbook/assets/openapi (1) (1).yaml>)
{% endswagger %}

## Delete a Sub-Account API Key

Delete the specified API key for the given sub-account.

{% swagger src="../../.gitbook/assets/openapi (1) (1).yaml" path="/subaccounts/{id}/keys/{keyId}" method="delete" %}
[openapi (1) (1).yaml](<../../.gitbook/assets/openapi (1) (1).yaml>)
{% endswagger %}

