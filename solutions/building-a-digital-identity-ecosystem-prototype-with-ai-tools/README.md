# Building a digital identity ecosystem prototype with AI tools

## What this is

A walkthrough for building a working verifiable credentials prototype on Truvera in about an hour, using Claude Design for the interface and Claude Code for the implementation.

At the end you have a running application where an employer issues an employee badge, the employee stores it in a cloud wallet in the browser, and an online event platform verifies it to grant access. Revoke the badge and access stops.

What this is not. It is not production code, and it is not a production wallet product. Truvera provides the APIs and the wallet SDKs. The wallet interface and the verifier screens are yours to build, which is what the AI tools are doing here. Nothing in this prototype is hosted by Truvera except the API and the encrypted data vault.

The one hour assumes you already know your use case: who issues, who verifies, what the credential contains. If that is still open, the schema step will take longer than the time allowed for it.

\
Before you start
----------------

### From Truvera support

Email [support@truvera.io](mailto:support@truvera.io) for both of these at once, they take a day or so to come back:

* Ecosystem tools enabled on your account. It is an add-on and off by default.
* An EDV auth key. Required for the cloud wallet.

### On your machine

* A Truvera account with a testnet API key
* Node and npm
* Claude Code, and access to Claude Design
* The Truvera mobile wallet installed, for testing
* A project directory containing the Truvera knowledgebase repo and a CLAUDE.md file.&#x20;
* Clone the docs with `git clone --depth 1 https://github.com/docknetwork/knowledgebase-docs.git`, then add the CLAUDE.md below alongside it. Claude Code reads that file automatically at the start of every session, and it is what stops it inventing endpoint shapes from memory.

{% prompt description="Example Claude.md" %}
```markdown
# Project context

A verifiable credentials prototype on Truvera. Frontend plus a small Node server that holds the API keys and proxies all Truvera calls.

## Documentation

The Truvera knowledgebase is cloned into ./knowledgebase-docs. Consult it before
writing any Truvera API or SDK call. Do not rely on recall for endpoint paths,
request bodies, or SDK method names.

Where things are:
- ./knowledgebase-docs/truvera-api/ — REST API, sub-accounts, Postman collections
- ./knowledgebase-docs/credential-wallet/ — wallet SDKs, cloud wallet integration

SUMMARY.md is the table of contents for the whole repo, use it when something is
not in either folder.

If something is not in the knowledgebase, say so rather than guessing. A wrong
endpoint that returns 200 is worse than a question.

## Environment

Base URL: https://api-testnet.truvera.io
Testnet only. Nothing here touches the mainnet.

## Values

handoff.md holds the issuer DID, verifier DID, schema ID, proof template ID, and
both API keys. Use those values exactly. 
handoff.md includes the schema URL. Fetch it rather than assuming field names.

## Rules

- API keys never reach the browser. Every Truvera API call goes through the proxy.
- Two keys. Issuance uses the issuer key. Proof requests and results use the
  verifier key. Never use one key for both.
- The EDV auth key is used by the wallet SDK in the browser, not by the proxy.
- Build in checkpoints. Stop after each one so I can run it before you continue.CLAUDE.md

```
{% endprompt %}

### What you need to have decided

* Who issues the credential, who holds it, who verifies it
* What the credential contains
* What the verifier needs to check, which is usually less than the credential contains

<figure><img src="../../.gitbook/assets/Screenshot 2026-08-26 at 19.36.42.png" alt=""><figcaption></figcaption></figure>

### The example we used&#x20;

An employer issues an employee badge to its staff. An online event platform accepts that badge as proof of employment, and grants access to a members-only event.

Two organisations: the event platform and the employer. The event platform trusts the employee badge because both organisations are participants in an ecosystem, and the ecosystem records which issuers are permitted to issue this schema.&#x20;

The badge is held in a cloud wallet, running in the browser, because the wallet and the event platform are both web applications. The mobile wallet is used once, to check the setup before any code is written. It can also be used in the prototype itself, since it is available in the app stores and does not need to be custom built.

For your use case. The shape here is one issuer, one credential, one verifier that needs only part of it. That covers most first prototypes. If your use case has several issuers or several verifiers, the sequence does not change, you add participants to the same ecosystem.

<figure><img src="../../.gitbook/assets/Screenshot 2026-08-26 at 19.37.05.png" alt=""><figcaption></figcaption></figure>
