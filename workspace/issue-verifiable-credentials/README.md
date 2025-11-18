# Issue verifiable credentials

## Issuing credentials <a href="#h_c3a1aee140" id="h_c3a1aee140"></a>

In the Credentials menu, click Issue credentials.

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-19 at 14.42.59.png" alt=""><figcaption></figcaption></figure>

### Select a credential schema <a href="#h_e6f35266ad" id="h_e6f35266ad"></a>

Select a pre-made credential schema by clicking on it's name or [Create your own schema](../create-a-schema.md). You can click on Preview to see what attributes are included in the template.

<figure><img src="../../.gitbook/assets/Screenshot 2024-03-21 at 16.27.40 (1).png" alt=""><figcaption></figcaption></figure>

### Select a design <a href="#h_662fe7eaa5" id="h_662fe7eaa5"></a>

Select a design or [create a new one](../create-a-design.md) for your credentials. Alternatively, you can proceed without a design.

### Add recipients <a href="#h_5fb66344c4" id="h_5fb66344c4"></a>

If you have many credentials to issue, you can issue them in bulk. To do this, select **Import Spreadsheet.**

<figure><img src="https://downloads.intercomcdn.com/i/o/797670167/d0dbab0c2d32c4b8fb42882a/Screenshot+2023-08-01+at+14.51.00.png" alt="" width="375"><figcaption></figcaption></figure>

Download the sample CSV template and fill in the details needed for your credential template. Upload the completed .csv file back to Truvera. [Read how to correctly format the Spreadsheet for CSV upload.](./#formatting-the-csv-file-for-recipient-upload)

<figure><img src="https://downloads.intercomcdn.com/i/o/797695179/a28c99740299645f876ce8be/6356f7181e5260685afe7bd9_9-Download+CSV.png" alt=""><figcaption></figcaption></figure>

If you want to add recipients one by one, select Add Manually.

You can distribute your credentials by email or directly to their wallet through their DID.

To send the credential by email, fill in their email in the **Recipient Email** field.

![](https://downloads.intercomcdn.com/i/o/797721246/2840f531c2020bf9df3a117c/64744417375359ce3af2c7ea_1-email+distribution.png)

To send the credential directly to the holders wallet fill in their DID in the Subject ID (Recipient ID) field.

Fill in all other attributes that need to be included in the credential _e.g. Subject name, Credential Title etc._

### Formatting the CSV file for recipient upload

You can download the CSV sample file to use as a base for you recipient data upload. The sample file has only 3 collumns with the _name_, _did_ and _date_ attributes.

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-29 at 17.22.04.png" alt=""><figcaption></figcaption></figure>

You will need to add columns and remove the ones you do not have in your credential schema.

When uploading a file you will be able to select a charset specification. UTF-8 will bet the choice for most users. If your dataset contains special characters you might need to choose a different charset, based on the one used to encode your data file.

<figure><img src="../../.gitbook/assets/Screenshot 2024-03-21 at 16.19.02.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If you do not know the holders dids you do not have to use it for the import, you can add emails, for the email distribution or distribute credentials manually.
{% endhint %}

You will be asked to match the columns on the csv file to the credential fields. If there are any required fields on the credential schema they must be filled in, otherwise the import will not be successful.

<figure><img src="../../.gitbook/assets/Screenshot 2024-01-29 at 17.29.15.png" alt=""><figcaption></figcaption></figure>

### Expire credential <a href="#h_c9b588481e" id="h_c9b588481e"></a>

If you need the credential to expire, turn on the expiration toggle and enter the expiration date.

![](https://downloads.intercomcdn.com/i/o/797671954/0a79de9246c232395c2825c1/Screenshot+2023-08-01+at+14.52.52.png)

### Choose credential options <a href="#h_e26a4957df" id="h_e26a4957df"></a>

After you have added your credential recipients you will be able to select the credential settings. You have the options to:

**Persist credential:** This option will encrypt the credential by providing a password to access it and store it on Truvera's servers. The credential can be accessed and verified by a URL or QR Code. The recipient can scan the QR Code to import the credential into a wallet app. The credential can be deleted from Truvera's cloud whenever you decide.

{% hint style="info" %}
Persisting is a good option for issuers if they want to securely store the credentials as a backup. It encrypts the credentials using Libsodium crypto secretbox Salsa20/Poly1305 algorithm and stores them on our servers that are located in the US and are powered by Amazon Web Services (AWS). Because the credential information is encrypted, Truvera can’t access the information to ensure data privacy and security. ​
{% endhint %}

**Credential revocation:** By selecting Enable Revocation, you leave an option for the credential to be revoked to invalid state at any time. If you leave this option unchecked, the credential can never be revoked and will always be verifiable.

Select which [Organization Profile (DID)](../create-an-organization-profile-did.md) you want to use to issue the credentials.

<figure><img src="../../.gitbook/assets/Screenshot 2025-04-07 at 13.50.43.png" alt=""><figcaption></figcaption></figure>

### Choose credential variant <a href="#h_e26a4957df" id="h_e26a4957df"></a>

Truvera offers a choice of 3 different credential variants that have distinct features and are best fit for different use cases.

* **Standard Signature (ed25519)** - a more simple credential variant that is the best option for interoperability with other verifiable credential services.
* **Anonymous (dockbbs23)** - uses BBS+ to enable selective disclosure and zero knowledge proofs. Best for use cases where user data privacy is a top priority.
* **EUDI (SD-JWT-VC) -** follows European identity standards for compliance and interoperability.

\
There is a 4th credential variant **Ecosystem-bound (BBDT16)** that is used for [Ecosystem bound credentials.](../monetizing-credentials/) It will get automatically selected when a price is assigned to a schema in an ecosystem.

<figure><img src="../../.gitbook/assets/Screenshot 2025-04-07 at 14.11.14.png" alt="" width="375"><figcaption></figcaption></figure>

### Distribute credentials <a href="#h_22a510abcd" id="h_22a510abcd"></a>

If you have entered the holders DIDs to Subject ID the holder will receive the credential directly in their wallet without any additional communication needed.

![](https://downloads.intercomcdn.com/i/o/797749786/65a19e3bd9bdb27970ce16ea/e4aebe54-e4c5-46b4-b30e-1b9083b74a87.jpeg)

If you have entered the email address, you will have an option to write a message and preview the email that is going to be sent to the receiver of the credential.

<figure><img src="https://downloads.intercomcdn.com/i/o/797730898/839d62e93c6bb388f29eb493/Screenshot+2023-08-01+at+15.57.06.png" alt="" width="375"><figcaption></figcaption></figure>

If you do not have or want to use DIDs for the credential distribution you will need to enter an email of the recipient or persist the credential.

<figure><img src="../../.gitbook/assets/Screenshot 2025-04-07 at 14.16.32.png" alt="" width="375"><figcaption></figcaption></figure>
