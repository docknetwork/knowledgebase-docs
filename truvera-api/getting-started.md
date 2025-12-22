# Getting started

## Architecture style

Truvera is built using a [REST](https://en.wikipedia.org/wiki/Representational_state_transfer) architecture. Our API follows common patterns including standard HTTP header authentication and standard HTTP response codes. It accepts form-encoded request bodies and  delivers JSON-encoded responses.

HTTPS is required for all API requests. Requests performed via plain HTTP will be rejected. API requests that do not include authentication will also fail. JSON requests should typically be encoded as UTF-8.

## Terminology

Understanding key terminology in Truvera will help you to use the API:

<table><thead><tr><th width="140">Terminology</th><th>Description</th></tr></thead><tbody><tr><td>DID</td><td>Decentralized Identifiers (DIDs) are identifiers that enable verifiable, decentralized digital identity. A DID refers to any subject (e.g., a person, organization, thing, data model, abstract entity, etc.) as determined by the controller of the DID. For more information, please refer to the <a href="https://www.w3.org/TR/did/">W3C standard</a> or <a href="https://docknetwork.github.io/sdk/tutorials/concepts_did.html">Credential SDK docs</a>.</td></tr><tr><td>Verifiable Credential</td><td>A verifiable credential is a specific way to express a set of claims made by an issuer so that it is tamper-resistant and can be delivered to a verifier via a wallet in control of the data subject. For more information, pleases refer to the <a href="https://www.w3.org/TR/vc-data-model/">W3C standard</a>.</td></tr><tr><td>Data Schema</td><td>The structure that describes the logical view of the data. It is useful to enforce a specific structure on a collection of data like a verifiable credential.</td></tr><tr><td>Schema</td><td>The list of attributes and structure of a credential that is used to create a verifiable credential of a specific type. It does not contain any cryptographic material and is shareable among issuers.</td></tr><tr><td>Registries</td><td>A reference to a unique credential in context of a process for handling revocation of that credential type.</td></tr><tr><td>Blob</td><td>Blob stands for Binary Large OBject. It is a collection of binary data stored as a single entity. The schemas are identified and retrieved by their unique blob id, which is a 32-byte long hex string.</td></tr><tr><td>DID Resolver</td><td>The tool that initiates the process of learning the DID document.</td></tr></tbody></table>

## Integration paradigms

There are three general patterns for using the Truvera API.

### Synchronous responses

Simply calling the API will result in a synchronous response. Calls to the API will block until a response is returned.

This is a simple approach for development and testing, but is not suitable for production use because system resources will be blocked until the response is received. This can take a long time if you are waiting for the credential holder to take an action.

### Asynchronous polling

By adding a callback URL to an API call, a synchronous response will be immediately returned informing the caller of success or failure. The caller then polls a callback URL until the response is available. This allows the polling to be done in a background thread, unblocking system resources. It also allows the polling to be done by a proxy behind a white-labeled API.

### Asynchronous webhook responses

[By registering a webhook](webhooks/), the response will be provided asynchronously when available. The webhook response will confirm that an event occurred and provide you with a identifier that you use to call back and receive the event details. This helps minimize data that would be seen by a 3rd party webhook provider.

## Prerequisites

You must have an account and acquire your credentials (API keys) before accessing the Truvera API. You can register an account and generate a key in your [Truvera Workspace](https://truvera.io/keys) dashboard.

{% hint style="warning" %}
Keep in mind that your API keys should be kept private, so keep them safe! Do not post your private API keys on GitHub, in client-side code, or anywhere else that is publicly available.
{% endhint %}

We generally recommend configuring your solution in the [Truvera Workspace](../truvera-workspace/), as it provides an easy to use interface for managing organization profiles, creating schemas, setting up verification templates, and administering ecosystems. You can even manually issue and verify through the web interface. When creating schemas and verification templates, you can download JSON that can then be used to complete the same action via the API.

We also recommend using the [Truvera Wallet](../credential-wallet/truvera-mobile-wallet/) to hold and present your credentials while you are testing the API. Once you have your basic flow working, you can then customize the holder's wallet experience using the [Truvera Wallet SDK](../credential-wallet/wallet-sdk/).

## Endpoints

Truvera provides two endpoints based on which mode was selected when creating your API key. By default, trial users only have access to Test data. Paid subscribers can create production API keys by switching the **test mode** toggle in Truvera Workspace in the top right next to your avatar icon. When in **test mode** you will see only testnet transactions, API keys, webhooks etc.

It should be noted that in **test mode** your used transaction count **will not increase or hit monthly limits** allowing for sandboxing on our test network.

* For production mode, use the endpoint: [https://api.truvera.io](https://api.truvera.io)
* For test mode, use the endpoint: [https://api-testnet.truvera.io](https://api-testnet.truvera.io)

{% hint style="warning" %}
Any transaction you perform in **test mode** cannot be used for **production**. This means that, for example, any DID created in **test mode** will not work for issuing or verification in **production**.
{% endhint %}

{% hint style="warning" %}
**Test mode** will be subject to data resets periodically, so the DIDs, etc. that you create there should not be expected to be permanent.
{% endhint %}

## Authentication

Truvera uses API keys to authenticate requests. You can obtain an API key by signing into [Truvera Workspace](https://truvera.io/). Once a key has been generated, it should be included in **all** request headers as below:

* Authorization: Bearier API\_KEY

When you generate an API key, you may include a list of whitelisted IP's that can use with that key.

## Rate limits

We allow you to make up to 200 requests in a 2 minute window (avg 100 reqs/min or 1.6 reqs/second). If you exceed beyond that, you will receive a 429 Too Many Requests response and have to wait up to a minute for the next request depending on when you hit the limit. If you require higher rate limits, please [contact us](../support/).

## Error handling

The Truvera API uses standard HTTP response codes to indicate if an API request was successful or unsuccessful.

The table below shows the most frequent HTTP error messages:

<table><thead><tr><th width="101">Code</th><th>Meaning</th></tr></thead><tbody><tr><td>400</td><td>Bad Request — Your request was rejected (e.g., missing mandatory field).</td></tr><tr><td>402</td><td>Payment required — Transaction limit reached or upgrade required to proceed</td></tr><tr><td>401</td><td>Unauthorized — Do not own resource or have an invalid API key in the header.</td></tr><tr><td>404</td><td>Not Found — The resource that you're trying to interact with could not be found on the server.</td></tr><tr><td>405</td><td>Method Not Allowed — The requested method does not exist in the API spec. Please check the {did} value and ensure that it's not empty/blank.</td></tr><tr><td>429</td><td>Too Many Requests — You sent too many requests. Please try to reduce the number of requests.</td></tr><tr><td>500</td><td>Server Errors — Something has gone wrong on the server. Contact us if this keeps happening.</td></tr></tbody></table>

## Troubleshooting

The Truvera Workspace is built using the REST API, so the network request viewer in your browser's developer tools will show the JSON used in requests and responses which you can then copy to your API calls. You can also examine errors in the browser developer console to get more insight into what is happening.
