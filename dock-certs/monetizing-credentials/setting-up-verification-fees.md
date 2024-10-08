# Setting up monetizable credentials

This is a detailed guide on how to monetize your credentials using Dock.

### Creating an ecosystem

Verification fees can be set by Ecosystem administrators to the participants of an ecosystem. Verifiers will only be able to access a credential if they are in the same ecosystem with the Issuer.  See the step by step guide on [Ecosystem set up](../ecosystem-tools/ecosystem-set-up.md).&#x20;

{% hint style="info" %}
Ecosystem administrators should only invite verifiers to an ecosystem with paid credentials if they have a billing relationship in place.
{% endhint %}

### Assigning schemas and adding verification prices

Verification prices are added to the schemas when assigning them to participants in the ecosystem.&#x20;

First a schema needs to be [created](../create-a-schema.md) and then [assigned to an ecosystem](https://docs.dock.io/dock-certs/ecosystem-tools/ecosystem-set-up#assign-credential-schemas).

<figure><img src="../../.gitbook/assets/Screenshot 2024-07-16 at 15.57.21.png" alt="" width="375"><figcaption></figcaption></figure>

Verification fee will be displayed to all ecosystem participants. Verification fee is displayed in USD, but ecosystem administrators can transact with their ecosystem participants in their preferred currency.&#x20;

{% hint style="warning" %}
Dock will charge a percentage of the Verification fee as a platform commission. For each verification where that commission is too low, we will charge a minimum platform fee.&#x20;
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2024-07-16 at 16.14.08.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
The systems supports tracking fees in fractions of a cent to six decimal places.
{% endhint %}

### Issueing credentials&#x20;

The process of issuing credentials will be the same. [See step by step instructions.](setting-up-verification-fees.md#issue-credentials)

The issuer will see a message showing that the credential can only be verified by participants of the specified ecosystem and requires a verification fee.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-07-16 at 16.47.37.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Zero-Knowledge Proof type of credential is mandatory for paid verification and will be selected by default.
{% endhint %}

For the holders monetizable credentials will look almost the same as regular credentials, they will be able to see an Ecosystem Bound badge in the credential settings withthe explantion, that this credential was issued within a specific ecosystem and is sharable only with verifiers authorized by that ecosystem.

<div align="left">

<figure><img src="../../.gitbook/assets/1721302321937.jpeg" alt="" width="188"><figcaption></figcaption></figure>

</div>

### Creating a verification template and assigning it

When [creating a verification template ](../verify-credentials.md)a message will be shown that there is a fee for verifying each credential using the selected schema.

<figure><img src="../../.gitbook/assets/Screenshot 2024-07-18 at 14.41.40.png" alt=""><figcaption></figcaption></figure>

[Verification templates need to be added to an ecosystem](https://docs.dock.io/dock-certs/ecosystem-tools/ecosystem-set-up#add-verification-templates) and will be visible for all participants.

{% hint style="info" %}
Wallet-to-wallet verification is not supported by monetizable credentials.
{% endhint %}

### Choosing a DID for verification

When using a monetizable credential verification template verifier will be prompted to choose the verifiers DID. It has to be the same DID that is participating in the ecosystem.

<figure><img src="../../.gitbook/assets/Screenshot 2024-07-18 at 14.51.39.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
When the holder has the same information in monetizable credentials from two different ecosystems, verification will default to the least expensive ecosystem.
{% endhint %}

### Getting the billing report&#x20;

All payments are  managed by the ecosystem administrator. Dock provides a billing report that can be downloaded by the ecosystem administrator.

<figure><img src="../../.gitbook/assets/Screenshot 2024-07-18 at 15.28.00.png" alt="" width="375"><figcaption></figcaption></figure>

Billing report data can be selected for a specific date range and will include information about the date of verification, schema that was verified, verification ID, DIDs of Issuer and Verifier, whether the verification was successful and verification and platform fees.

<figure><img src="../../.gitbook/assets/Screenshot 2024-10-08 at 14.47.48.png" alt=""><figcaption></figcaption></figure>



Billing report includes all verifications where a credential was submited for verification e.g if a verification request was made, but no credential was presented it will not be included, however if an invalid credential is presented and verification fails it will be included in the billing report.&#x20;

{% hint style="info" %}
Ecosystem administrators take responsibility for charge-backs and disputes.&#x20;
{% endhint %}

{% hint style="info" %}
Ecosystem administrators can remove ecosystem participants that do not meet ecosystem requirements.
{% endhint %}
