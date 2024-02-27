# Getting Started

## Prerequisites

You must first have an account and acquire your credentials (API keys) before accessing the Dock Certs API. You can register an account and generate a key in your [Dock Certs](https://certs.dock.io/) dashboard.

{% hint style="warning" %}
Keep in mind that your API keys should be kept private, so keep them safe! Do not post your private API keys on GitHub, in client-side code, or anywhere else that is publicly available.
{% endhint %}

## Endpoints

Dock Certs provides two endpoints based on which mode was selected when creating your API key. By default, the API keys are created for production. You can switch to **test mode** in [Dock Certs](https://certs.dock.io/) by clicking the **test mode** toggle in the top right next to your avatar icon. Once in **test mode** you will see only testnet transactions, API keys, webhooks etc. You can then create an API key from the [Dock Certs dashboard](https://certs.dock.io/keys). It should be noted that in **test mode** your used transaction count **will not increase or hit monthly limits** allowing for sandboxing on our test network.

* For production mode, use the endpoint: [https://api.dock.io](https://api.dock.io)
* For test mode, use the endpoint: [https://api-testnet.dock.io](https://api-testnet.dock.io)

{% hint style="warning" %}
Any transaction you perform in **test mode** cannot be used for **production**. This means that, for example, any DID created in **test mode** will not work for issuing or verification in **production**.
{% endhint %}

{% hint style="warning" %}
**test mode** will be subject to data resets periodically, so the DIDs, etc. that you create there should not be expected to be permanent.
{% endhint %}

## Authentication

Dock Certs uses API keys to authenticate requests. You can obtain an API Key by signing into [Dock Certs](https://certs.dock.io). Once a key has been generated, it should be included in **all** request headers as below:

* API Key (accessToken)
  * Name: **DOCK-API-TOKEN**
  * OR HTTP Bearer Authorization

When you generate an API key, you may include a list of whitelisted IP's that can use with that key.

## Architecture Style

Dock Certs is built using a [REST](https://en.wikipedia.org/wiki/Representational\_state\_transfer) architecture. Our API uses standard HTTP response codes, authentication, delivers JSON-encoded responses, accepts form-encoded request bodies, and accepts form-encoded request bodies.

HTTPS is required for all API requests. Requests performed via plain HTTP will be rejected. API requests that do not include authentication will also fail. JSON requests should typically be encoded as UTF-8.

<table><thead><tr><th width="305">HTTP Method</th><th>Description</th></tr></thead><tbody><tr><td>GET</td><td>Gets one or many resources</td></tr><tr><td>POST</td><td>Creates a new resources</td></tr><tr><td>PATCH</td><td>Partially updates a resource</td></tr><tr><td>DELETE</td><td>Deletes a resource</td></tr></tbody></table>

## Rate Limits

We allow you to make up to 200 requests in a 2 minute window (avg 100 reqs/min or 1.6 reqs/second). If you exceed beyond that, you will receive a 429 Too Many Requests response and have to wait up to a minute for the next request depending on when you hit the limit. If you require higher rate limits, please [contact us](../../support/).

## Error Handling

The Dock Certs API uses standard HTTP response codes to indicate if an API request was successful or unsuccessful.

The table below shows the most frequent HTTP error messages:

<table><thead><tr><th width="101">Code</th><th>Meaning</th></tr></thead><tbody><tr><td>400</td><td>Bad Request -- Your request was rejected (e.g., missing mandatory field).</td></tr><tr><td>402</td><td>Payment required -- Transaction limit reached or upgrade required to proceed</td></tr><tr><td>401</td><td>Unauthorized -- Do not own resource or have an invalid API key in the header.</td></tr><tr><td>404</td><td>Not Found -- The resource that you're trying to interact with could not be found on the server.</td></tr><tr><td>405</td><td>Method Not Allowed -- The requested method does not exist in the API spec. Please check the {did} value and ensure that it's not empty/blank.</td></tr><tr><td>429</td><td>Too Many Requests -- You sent too many requests. Please try to reduce the number of requests.</td></tr><tr><td>500</td><td>Server Errors -- Something has gone wrong on the server. Contact us if this keeps happening.</td></tr></tbody></table>

## Terminology

It is important to fully understand all the terminologies within the Dock ecosystem. The following are common terminologies within our ecosystem:

<table><thead><tr><th width="140">Terminology</th><th>Description</th></tr></thead><tbody><tr><td>DID</td><td>DID stands for Decentralized Identifier. It is a new type of identifier that enables verifiable, decentralized digital identity. A DID refers to any subject (e.g., a person, organization, thing, data model, abstract entity, etc.) as determined by the controller of the DID. For more information, please refer <a href="https://docknetwork.github.io/sdk/tutorials/concepts_did.html">here</a>.</td></tr><tr><td>Anchoring</td><td>A feature that allows users to store a digest of one or more credentials (or any files) on our blockchain so that they are associated with immutable timestamps and hence can be proven to have been created at a certain point in time.</td></tr><tr><td>Data Schema</td><td>The structure that describes the logical view of the data. It is useful to enforce a specific structure on a collection of data like a Verifiable Credential.</td></tr><tr><td>Registries</td><td>A process to verify credentials in such a way that each verified credential has its own unique number. This process references a credential definition and specifies how revocation of that credential type will be handled.</td></tr><tr><td>Schema</td><td>The structure of credentials which are shareable among issuers as they do not contain any cryptographic material and thus are created less frequently.</td></tr><tr><td>Blob</td><td>Blob stands for Binary Large OBject. It is a collection of binary data stored as a single entity. The schemas are identified and retrieved by their unique blob id, which is a 32-byte long hex string.</td></tr><tr><td>DID Resolver</td><td>The tool that initiates the process of learning the DID document.</td></tr></tbody></table>

