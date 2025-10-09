# Biometric-bound credentials

## What are biometric-bound credentials?

Biometric is a a physical characteristic, e.g. eye, finger, face, voice, gait.  When a person’s physical attribute is measured it is translated to something that can be stored - an enrollment template.

After the enrollment is complete, to match the biometric the physical attribute is measured again and translated to something that can be matched - a candidate sample. The sample is then matched with the template. The match score is compared with a threshold to return a positive or negative result.

There are different ways to store biometrics.

<table data-view="cards"><thead><tr><th></th><th></th><th></th><th data-hidden data-card-cover data-type="files"></th></tr></thead><tbody><tr><td><p><strong>Centralized</strong> </p><p>Biometric provider stores biometric data from multiple people in a common database. Each relying party integrates with the provider, and may see biometric data. </p></td><td></td><td></td><td><a href="../.gitbook/assets/Screenshot 2024-07-31 at 16.21.41.png">Screenshot 2024-07-31 at 16.21.41.png</a></td></tr><tr><td><strong>Decentralized</strong></td><td>Biometric provider stores each person’s data in a different sharded vault which cannot be reconstructed without the biometric vector.</td><td></td><td><a href="../.gitbook/assets/Screenshot 2024-07-31 at 16.28.29.png">Screenshot 2024-07-31 at 16.28.29.png</a></td></tr><tr><td><strong>User-stored</strong></td><td>Biometric data is securely stored on the person’s device using tamper-proof credentials.</td><td></td><td><a href="../.gitbook/assets/Screenshot 2024-07-31 at 16.29.23.png">Screenshot 2024-07-31 at 16.29.23.png</a></td></tr></tbody></table>

### How user stored biometrics work

Relying parties use open standards to verify credentials issued by their trusted biometric providers. Relying parties never see biometric data.

|                                                                 |                                                                                                                              |
| --------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| ![](<../.gitbook/assets/Screenshot 2024-07-31 at 16.32.36.png>) | <p>1. Check the biometric and issue an enrollment credential containing the biometric data and a private identifier<br></p>  |
| ![](<../.gitbook/assets/Screenshot 2024-07-31 at 16.37.02.png>) | 2. Check the biometric against the enrollment credential and issue a biometric-check credential with the private identifier  |
| ![](<../.gitbook/assets/Screenshot 2024-07-31 at 16.37.59.png>) | 3. Relying parties verify that a biometric-check credential is recent, trusted, and contains the expected private identifier |

### What is a biometric-bound credential?

**Wallet-bound Credential** - the credential was put into a wallet at issuance, and taken from the same wallet at verification. It is assumed that the same person is in control of the wallet at both times.

**Biometric-bound Credential** - the same person who received the credential at issuance presented the credential for verification.

We suggests 2 possible approaches on how to implement biometric-bound credentials and address these concerns.

## How to implement biometric-bound credentials?

### Samples taken by issuer and verifier approach

In this model the issuer and verifier agree on a common provider of biometrics.&#x20;

Issuer requires holder to enrol in the biometric service and provide a biometric sample through the service before the issuer will issue a credential. &#x20;

The issued credential contains a link to the biometric template.&#x20;

At time of verification, verifier requires holder to provide a biometric sample through the same service and checks that it matches the template linked in the credential.

[Documentation how to add a biometric service plugin](../credential-wallet/wallet-sdk/biometric-plugin.md).

<figure><img src="../.gitbook/assets/Screenshot 2024-12-19 at 14.24.35.png" alt=""><figcaption></figcaption></figure>



| Pros                                                              | Cons                                                                        |
| ----------------------------------------------------------------- | --------------------------------------------------------------------------- |
| Can use biometric hardware provided by the issuer and verifier    | Biometric service can correlate issuer, verifier, and holder \*             |
| Being outside of the holder’s control can mean it is more trusted | Every issuer and verifier needs to integrate with the biometric service\*\* |
|                                                                   |                                                                             |

_\*Some biometric services are designed to be privacy preserving_

_\*\*Biometric standards can reduce cost of integration and lock-in_

### Samples taken by identity wallet approach

In this approach issuer asks the holder to provide a proof of biometric check before issuing a primary credential.&#x20;

Identity wallet detects the request, processes biometric, enrolls the holder, issues a credential and provides the credential to the issuer.&#x20;

Primary credential with biometric binding is issued by the issuer.&#x20;

Verifier asks for primary credential with a proof of biometric check.&#x20;

Wallet detects the request, processes biometric, and provides compound proof to the verifier.

{% hint style="info" %}
Primary credential: the credential which contains the attributes of interest to the verifier in addition to the biometric binding attributes
{% endhint %}

<figure><img src="../.gitbook/assets/Screenshot 2024-12-19 at 14.22.20.png" alt=""><figcaption></figcaption></figure>

#### Biometric enrollment

Holder sets up a wallet integrated with the biometric service. When a biometric binding is first required, the holder wallet enrolls the holder in the biometric service.

The biometric service issues a credential that generally contains at least the following attributes:

1. An attribute that contains the enrollment template - the reference biometric sample that is stored during enrollment to which future biometric samples are compared
2. Attributes that can be embedded in primary credentials to bind them to valid biometric verification credentials issued to the same holder

{% hint style="info" %}
Biometric data needs to be converted to a text based format so it can be embedded in JSON. The most popular method is to use "Base64" encoding.
{% endhint %}

A sufficiently privacy preserving biometric template can be embedded directly in the primary credential, avoiding the need for an enrollment credential.

The biometric enrollment and initial verification credentials may be issued using the same biometric sample to avoid an additional sample being taken from the holder.

The biometric binding attributes can usually be a smaller size than embedding the biometric template directly in a credential.

The enrollment credential contains the PII that would previously be stored in the BSP’s database.

#### Issuance

Holder requests a primary credential from the issuer. Issuer requests a proof of a recent biometric check.

The holder’s identity wallet detects that the request includes biometric binding attributes, and triggers the associated plugin that requests a biometric verification credential from the biometric service.

Biometric service requests to verify the biometric enrollment credential. Biometric service checks a new biometric sample against the template included in the enrollment credential. Biometric service issues a credential showing a valid biometric check, that contains the biometric binding attributes and a timestamp of the check.

The wallet provides the biometric verification credential to the issuer, who checks that the credential is recent.

Issuer issues the primary credential, with additional biometric binding attributes including the identity of the issuing biometric service.

#### Verification

Verifier requests a compound proof of a primary credential and a recent biometric verification credential.

The holder’s identity wallet detects that the request includes biometric binding attributes, and triggers the associated plugin that requests a biometric verification credential from the biometric service. The wallet’s biometric plugin follows the same process as was used during issuance to obtain a recent biometric verification credential.

Holder provides the biometric verification credential in a compound proof with the primary credential

Verifier checks that the biometric verification credential is from a trusted biometric service provider that was used at issuance and that the biometric binding attributes of the primary credentials matches the biometric binding attributes in the biometric verification credential.

#### Benefits

* Biometric is taken on the device, and only accessed by the biometric service provider
* Biometric service doesn’t have to store holder data, yet has assurance that the data has not been manipulated by the holder
* Issuer and verifier do not need to integrate with the biometric service
* Holder wallet can easily integrate with multiple biometric services
* Trust registry can list biometric services that should be trusted within an ecosystem
* The biometric service providers can enforce that all interactions are with a trusted wallet

### Privacy concerns and suggested solutions

**How to store the enrollment template in a privacy preserving manner?**

Identity Wallet Approach: Have the identity subject hold a tamper-proof verifiable credential issued by the biometric service provider.

Issuer-Verifier Approach:  Depends on the specific biometric service used.

**How to bind a credential to a biometric template without correlation by the verifier?**

The verifier checks a Zero-Knowledge Proof (ZKP) comparing the biometric binding attributes of the primary credential with the biometric verification credential without disclosing the binding attributes.

**How to bind a credential to a biometric template without correlation by the issuer?**

&#x20;Use blind signatures to not disclose the actual binding attribute.
