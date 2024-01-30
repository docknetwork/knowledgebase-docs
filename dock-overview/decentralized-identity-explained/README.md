# Decentralized identity explained

Decentralized  identity is a way of managing online identities that do not rely on storing personal data in centralized databases such as social media platforms or government ID systems. Decentralized identity systems enable users to completely own and control their data.&#x20;

## **The 3 parties of decentralized identity systems**

1. **Issuer:** An organization that has the authority to issue Verifiable Credentials such a KYC company issuing a KYC credential or online course platform issuing completion certificates
2. **Holder:** User who owns the credential and stores it in their digital wallet
3. **Verifier:** The party validating or authenticating the credential like an employer needing to check a candidate’s educational credentials or staff at a store that needs to verify that a customer is at least 18 to buy alcohol

<figure><img src="../../.gitbook/assets/decentralized identity system.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Decentralized identity is often used interchangeably with the term Self-Sovereign Identity (SSI).&#x20;
{% endhint %}

## The technical building blocks of decentralized identity

### Blockchain

Blockchain acts as an immutable registry containing the Decentralized Identifiers (DIDs) of all credential issuers. When verifying a credential, a Verifier will look up the Issuer's DID to see if it was truly that Issuer that signed that credential.&#x20;

{% tabs %}
{% tab title="What goes on chain?" %}
* Issuers' Decentralized Identifiers (DIDs) and associated Public Keys&#x20;
* Credential Schemas&#x20;
* Revocation Registries
{% endtab %}

{% tab title="What does not go on chain?" %}
* Personally identifiable information&#x20;
* Verifiable Credentials. Credentials are stored on the users' devices (e.g. their Wallets)
{% endtab %}
{% endtabs %}

{% embed url="https://youtu.be/XIE4KoE_sLo" fullWidth="false" %}

### **Decentralized Identifiers (DIDs)**

Decentralized identifiers (DIDs) are unique identifiers that are associated with a digital identity. DIDs are made up of a string of letters and numbers that can be stored on the blockchain and can be used to authenticate that identity.

{% embed url="https://youtu.be/zaYYQLDnS6s" %}

Here’s an example of a Dock DID:

<figure><img src="../../.gitbook/assets/decentralized identifier example.jpeg" alt=""><figcaption></figcaption></figure>

Every DID that is created comes with a private and public key pair and some DID methods allow multiple key pairs.&#x20;

Whenever an organization issues someone a Verifiable Credential, their public DID is attached to that credential. Because the public DID (and issuer’s public key) is stored on the blockchain, whenever a party wants to verify the authenticity of the credentials, they can check the DID on the blockchain to see if it was really the issuer’s private key that signed the Credential.

### Verifiable Credentials

Digital credentials that conform to the [Verifiable Credentials Data Model 1.0](https://www.w3.org/TR/vc-data-model/) developed by the World Wide Web Consortium (W3C) can be referred to as Verifiable Credentials. This standard is a “specification \[that] provides a standard way to express credentials on the Web in a way that is cryptographically secure, privacy-respecting, and machine-verifiable.”&#x20;

{% embed url="https://youtu.be/L3wbfHpwthA" %}

**Benefits of Verifiable Credentials:**

* Instantly verifiable, without the need to contact the issuer&#x20;
* Tamper-resistant with the use of cryptography&#x20;
* Privacy preserving by giving holders full control of their data
