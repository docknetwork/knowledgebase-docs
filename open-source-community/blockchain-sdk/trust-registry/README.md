---
hidden: true
noIndex: true
---

# Trust registry

Verifiable credentials have an advantage over physical documents, because they cannot be forged. However, there is still a fraud risk if a credential is issued by someone that has no authority to do so.

How can a verifier be sure that the credential came from an authorized issuer? And vice-versa, how can a credential holder know which verifiers are trustworthy and that it is okay to share their credentials with them? Trust registry is a solution to answer this problem.

## What is a trust registry?

\
A trust registry is an on-chain list of relationships between issuers and verifiers. It simplifies the process of identifying which issuers and verifiers are trustworthy within a particular ecosystem.  These registries serve as secure repositories for identity information, leveraging blockchain technology to ensure its integrity and reliability.

Trust registries are governed by trust frameworks, a set of operating rules that participants of the ecosystem must follow.

<figure><img src="../../../.gitbook/assets/Sales Demo v2 (2).png" alt=""><figcaption></figcaption></figure>

## Why use a trust registry

By having a trust registry, credential verifiers do not need to manage a list of valid issuers and holders know which verifiers they can trust to share their credentials with. They only need to trust one Ecosystem administrator. [Ecosystem Tools](../../../workspace/ecosystem-tools/) exemplifies the power of trust registries in creating a network of trusted digital identity issuers and verifiers.&#x20;

Trust registry contains the following information:

* Name of the Trust Registry and the Governance Framework
* Ecosystem Administrator and Issuers DIDs, Organization Names, Logos and descriptions
* A record associated with the SchemaID, which consists of a mapping from the Issuer DID to the verification prices and set of the Verifier DIDs







