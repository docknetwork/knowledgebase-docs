# Decentralized identity explained

Decentralized  identity is a way of managing online identities that do not rely on storing personal data in centralized databases such as social media platforms or government ID systems. Decentralized identity systems enable users to completely own and control their data.&#x20;

#### **The 3 main parties involved in a decentralized identity system are:**

1. **Issuer:** An organization that has the authority to issue Verifiable Credentials such a KYC company issuing a KYC credential or online course platform issuing completion certificates
2. **Holder:** User who owns the credential and stores it in their digital wallet
3. **Verifier:** The party validating or authenticating the credential like an employer needing to check a candidate’s educational credentials or staff at a store that needs to verify that a customer is at least 18 to buy alcohol

<figure><img src="../../.gitbook/assets/decentralized identity system.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Decentralized identity is often used interchangeably with the term Self-Sovereign Identity (SSI).&#x20;
{% endhint %}

#### The technical building blocks of decentralized identity



### Blockchain

{% embed url="https://youtu.be/XIE4KoE_sLo" %}

A blockchain is a decentralized digital record of transactions that is shared with every computer in the blockchain network. This chain of blocks is stored on every computer in the network, so everyone has a copy of the transaction history.&#x20;

**High security**

What makes the blockchain so secure is that even if someone were to hack into one computer and view the blockchain, they wouldn't be able to read it or make any changes without the encryption key.&#x20;

Each block contains a "hash" (like a unique digital fingerprint) of the previous block. So if anyone tries to tamper with a block, that would change its hash meaning that the block would no longer match up with the next block in the chain. As soon as someone tries to tamper with the blockchain, everyone else in the network would know immediately.&#x20;

**How blockchain is used in decentralized identity systems**

With Dock, we only store DIDs on the blockchain needed for a verifier to validate the authenticity of a credential like an issuer’s cryptographic key (digital signature) that matches the one on the credential. The data on credentials are stored on the user's mobile devices only and the information is securely encrypted.&#x20;

### **Decentralized Identifiers (DIDs)**

{% embed url="https://youtu.be/zaYYQLDnS6s" %}

Decentralized identifiers (DIDs) are globally unique identifiers made up of a string of letters and numbers that can be stored on the blockchain and doesn’t rely on a central authority to verify their authenticity. DIDs are used to give people and organizations a unique online identity that can be used to access services and conduct transactions. Unlike traditional identifiers, such as Social Security numbers or email addresses, DIDs cannot be centrally controlled or revoked.&#x20;

Here’s an example of a Dock DID:

<figure><img src="../../.gitbook/assets/decentralized identifier example.jpeg" alt=""><figcaption></figcaption></figure>

**Key features of DIDs:**

* Created, owned, and managed completely by the user (individual or organization) without depending on any third party
* Allow the owner to securely prove control over them
* Don’t contain any personal data or wallet information&#x20;
* Easily created with the [Dock Wallet](https://www.dock.io/dock-wallet-app) and [Dock Certs](https://certs.dock.io/) platform

Users can create as many DIDs as they want for different purposes. For example, someone can use:&#x20;

* DID 1: To purchase things online
* DID 2: To hold professional credentials like training certificates and their university degree
* DID 3: To log into online gaming sites
* DID 4: To log into trading and investment services

<figure><img src="../../.gitbook/assets/decentralized identifier (DID) profiles.jpeg" alt=""><figcaption></figcaption></figure>

Every DID that is created comes with a private and public key pair and DIDs can have multiple pairs. A key acts like a password and is also a string of letters and numbers that aren’t identifiable. A public key is visible to everyone on the network, while a private key is known only to the individual. This system ensures that only the intended recipient can read the data, even if it is intercepted by someone else.

Here is an example of an employer’s DID and its private and public keys:

<figure><img src="../../.gitbook/assets/Decentralized identifier (DID) private and public key.png" alt=""><figcaption></figcaption></figure>

**Private key**&#x20;

It’s a piece of code that allows you to access data associated with the public key. You can think of a private key like a password where if someone has your private key, they can access all your valuable information. That’s why the private key should never be shared with anyone.&#x20;

**Public key**

You can compare a public key like an email address where anyone can use it to send you information but only you can access the data.&#x20;

**The Role of DIDs In the Decentralized Identity System**

* Issuers use DIDs to create credentials that are tamper-proof and verifiable
* Holders use their DIDs to securely store and manage their credentials
* Verifiers use DIDs to verify the authenticity of credentials without relying on a third party

Whenever an organization issues someone a Verifiable Credential, their public DID is attached to that credential. Because the public DID (and issuer’s public key) is stored on the blockchain, whenever a party wants to verify the authenticity of the credentials, they can check the DID on the blockchain to see if it was really the issuer’s private key that signed the Credential.

[Learn more from our complete guide on Decentralized Identifiers](https://www.dock.io/post/decentralized-identifiers).

### Verifiable Credentials

Examples of documents that can be issued as Verifiable Credentials include university degrees, professional certifications, driver’s licenses, and identity documents.

{% embed url="https://youtu.be/L3wbfHpwthA" %}

Digital credentials that conform to the [Verifiable Credentials Data Model 1.0](https://www.w3.org/TR/vc-data-model/) developed by the World Wide Web Consortium (W3C) can be referred to as Verifiable Credentials. This standard is a “specification \[that] provides a standard way to express credentials on the Web in a way that is cryptographically secure, privacy-respecting, and machine-verifiable.”&#x20;

<figure><img src="../../.gitbook/assets/Sign in with decentralized identifiers (DID).png" alt=""><figcaption></figcaption></figure>

Here is an example of how a holder, issuer, and verifier interact together:

<figure><img src="../../.gitbook/assets/Verifiable credential example.png" alt=""><figcaption></figcaption></figure>

**Benefits of Verifiable Credentials:**

* Instantly verifiable within seconds compared to days, weeks, and months with conventional verification processes
* Verifying organizations don’t need to waste time, money, and resources contacting the issuer
* Data is tamper-resistant with the use of cryptography&#x20;
* Holder has full control of their data
* Providers privacy for users
* No personal or sensitive data is stored on the blockchain

[Learn more from our complete guide on Verifiable Credentials](https://www.dock.io/post/verifiable-credentials)

<figure><img src="../../.gitbook/assets/Verifiable Credential tech flow.png" alt=""><figcaption></figcaption></figure>

\
