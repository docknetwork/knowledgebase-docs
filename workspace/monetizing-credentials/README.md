# Monetizing credentials

### What is credential monetization?

Truvera has a unique feature that allows setting a verification fee on credentials and introduces a new revenue stream that ecosystem administrator can leverage to motivate issuers to join their ecosystem. It converts credential issuance from expense to profit and is an important step in accelerating adoption of verifiable credentials by creating value for participating parties.&#x20;

### How does it work?

The technology is based on KVAC (Keyed Verification Anonymous Credential) to lock the credential making sure, that it can only be verified that a payment has been made.&#x20;

Ecosystem administrator sets a price for each schema and assigns it to participating issuers and verifiers.&#x20;

When a verifier is trying to verify a credential, they will be notified that this verification requires a fee. During the verification process, the issuer is asked to provide an additional secret for the specific credential schema in order to unlock it. This is all done automatically within seconds during the verification process.

{% hint style="info" %}
Holder privacy is a key consideration in our design. The verifier doesn't share any holder-identifying data  with the issuer when asking for verification. Only 2 random looking data items are shared with the issuer and issuer verifies a relationship between them e.g. verifier shares a pair of items (A, B) with the issuer and asks to check whether A equals B \* issuer-secret-key. Here A is the MAC from holder's credential but randomized so issuer can't identify it.
{% endhint %}

The Issuer sees that a credential based on a specific schema was shared with a specific Verifier, but learns nothing about the Holder. Preserving this requirement has forced us to innovate interesting solutions to use cases that previously required the Issuer to identify the Holder. With any technology, there are risks. The Issuer needs to use the same schema for enough credentials for Holders to benefit from herd privacy.

Truvera will track the verifications and provide detailed billing reports to the ecosystem administrators. A small percentage fee will be charged for each verification transaction based on the price set on the schema.
