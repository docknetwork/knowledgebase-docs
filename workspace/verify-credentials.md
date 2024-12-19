# Verify Credentials

Verification process

In a typical verification process, there are three main parties:

1. **Issuer:** Party that creates and issues a Verifiable Credential to a holder (individual or organization)
2. **Holder:** Person or organization that holds the credential (e.g. degree, professional certificate, or identity document)
3. **Verifier:** Party that checks that the credential is valid and authentic

<figure><img src="https://downloads.intercomcdn.com/i/o/801931889/c9976b09a48fe6e88920e78a/631f7526f09bcf3b4b2e6209_3-certificate+fraud-issuer%2C+holder%2C+verifier.jpeg" alt=""><figcaption></figcaption></figure>

## Steps for the Verifier <a href="#h_4638f9252a" id="h_4638f9252a"></a>

Click on Verification in the left menu and select Create verification template

<figure><img src="../.gitbook/assets/Screenshot 2024-12-19 at 15.51.09.png" alt=""><figcaption></figcaption></figure>

First, type in the **Template Title** and **Template Purpose**, which the holder will be able to see.

Optionally, you can choose a **Verifier DID** which will be shown to the holder so that they can verify who you are.

<figure><img src="../.gitbook/assets/Screenshot 2024-01-19 at 15.00.55.png" alt=""><figcaption></figcaption></figure>

The verifier can choose which credential details the holder is required to share  for the credential to be accepted.  Each attribute will be either required for verification and if not present will return an invalid verification or optional which means that the holder can choose if they want to share that information or not.

When creating a template you can choose a specific schema and those attributes will be available for selection in the drop down boxes.

You can combine verifying multiple credentials in one verification template by adding a credential and selecting schema and attributes.

<figure><img src="../.gitbook/assets/Screenshot 2024-08-16 at 16.09.39.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
The list will have only the attributes that are included in the credential schemas. If you want to include an attribute that is not on the schemas owned by that account it can be typed in instead of the listed attributes.
{% endhint %}

When verifying Zero Knowledge Proof credentials, you can use range proof verification conditions, that will verify the credential without disclosing the actual value of an attribute. For example, if you want to verify that the credential holder is older than 18 you can choose attribute Age and condition is greater than 18.

<figure><img src="../.gitbook/assets/Screenshot 2024-01-19 at 15.11.23.png" alt=""><figcaption></figcaption></figure>

If the verification template contains a paid schema a notification on the bottom will appear.

<figure><img src="../.gitbook/assets/Screenshot 2024-08-16 at 16.16.17.png" alt=""><figcaption></figcaption></figure>

Last step for a verification request is to click Request, which will generate a QR code. Every time a new request is made, it generates a new QR code.\
​

<figure><img src="../.gitbook/assets/63dc133a7f9006477e2c9e15_4-select request.png" alt=""><figcaption></figcaption></figure>

## Steps for the Holder <a href="#h_551a4bc680" id="h_551a4bc680"></a>

First step for the holder is to **Scan** the QR code with their wallet and select the credential(s) that contain the information the verifier is requesting.

<div align="left"><figure><img src="../.gitbook/assets/63dc147a07bea77af71f759a_1-select Verifiable Credentials.png" alt="" width="203"><figcaption></figcaption></figure></div>

{% hint style="info" %}
If the credentials were issued with Zero Knowledge Proof signatures the holder will be able to choose which details on the credentials to share with the verifier.
{% endhint %}

If the credentials are valid and the verification is successful, this is what the holder will see a **Verification Successful** message, if the credential could not be verified a **Verification Failed** message will appear.

## Verification History

To see a log of all your verification requests, go to Verification and click on **History**.

<figure><img src="../.gitbook/assets/Screenshot 2024-12-19 at 16.38.05.png" alt=""><figcaption></figcaption></figure>

When the credentials are valid it will show up as “Verified” under Status. The verifier won’t get a notification if the credential is invalid because Dock’s tools won’t let the holder submit invalid credentials.

<div align="left"><figure><img src="../.gitbook/assets/Screenshot 2024-01-25 at 17.59.50.png" alt="" width="375"><figcaption></figcaption></figure></div>

{% hint style="warning" %}
Verification request templates can only be created in Truvera Workspace, not the wallet. These templates can be important into the wallet from Truvera Workspace for wallet-to-wallet verification.
{% endhint %}

## Wallet-to-Wallet Verification <a href="#h_9833d67c15" id="h_9833d67c15"></a>

After creating the verification request in Truvera Workspace it can be imported in to the wallet for a wallet-to-wallet verification.

Go to **Settings** and choose **Credential Verifier**.

<div align="left"><figure><img src="https://downloads.intercomcdn.com/i/o/801963474/f0e42a69cd04be5cb000afa0/Screenshot_20230807_140939_DockApp.jpg" alt="" width="188"><figcaption></figcaption></figure></div>

Click Import via QR code and scan the verification template QR code generated in Truvera Workspace. [See how to create a verification template here.](verify-credentials.md#h_4638f9252a)

After the Verification template is imported you can share it with the holder to present and verify their credential.

![](https://downloads.intercomcdn.com/i/o/801966471/8b2b8552b1276fc19e7bc89d/Screenshot_20230807_141402_DockApp.jpg)

Holder will scan this QR code with their Truvera Wallet and follow the [verification steps for the holder](verify-credentials.md#h_551a4bc680).
