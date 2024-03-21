# Issue Verifiable Credentials

Issuing Credentials

In the Credentials menu, click Issue credentials.

<figure><img src="https://downloads.intercomcdn.com/i/o/797669904/4c77143e4d9f9ce6f4f345fc/Screenshot+2023-08-01+at+14.47.45.png" alt=""><figcaption></figcaption></figure>

### Select a credential schema <a href="#h_e6f35266ad" id="h_e6f35266ad"></a>

Select a pre-made credential schema by clicking on it's name or [Create your own schema](create-a-schema.md). You can click on Preview to see what attributes are included in the template.

<figure><img src="../.gitbook/assets/Screenshot 2024-03-21 at 16.27.40 (2).png" alt=""><figcaption></figcaption></figure>

### Select a design <a href="#h_662fe7eaa5" id="h_662fe7eaa5"></a>

Select a design or [create a new one](create-a-design.md) for your credentials. Alternatively, you can proceed without a design.

<figure><img src="https://downloads.intercomcdn.com/i/o/797670108/d8f1948a00a9b8d934c5b070/Screenshot+2023-08-01+at+14.50.40.png" alt=""><figcaption></figcaption></figure>

### Add recipients <a href="#h_5fb66344c4" id="h_5fb66344c4"></a>

If you have many credentials to issue, you can issue them in bulk. To do this, select **Import Spreadsheet.**

<figure><img src="https://downloads.intercomcdn.com/i/o/797670167/d0dbab0c2d32c4b8fb42882a/Screenshot+2023-08-01+at+14.51.00.png" alt=""><figcaption></figcaption></figure>

Download the sample CSV template and fill in the details needed for your credential template. Upload the completed .csv file back to Dock Certs. [Read how to correctly format the Spreadsheet for CSV upload.](issue-verifiable-credentials.md#formatting-the-csv-file-for-recipient-upload)

<figure><img src="https://downloads.intercomcdn.com/i/o/797695179/a28c99740299645f876ce8be/6356f7181e5260685afe7bd9_9-Download+CSV.png" alt=""><figcaption></figcaption></figure>

If you want to add recipients one by one, select Add Manually.

<figure><img src="https://downloads.intercomcdn.com/i/o/797700428/213956fd1fef006ab1f9adba/Screenshot+2023-08-01+at+14.51.00.png" alt=""><figcaption></figcaption></figure>

You can distribute your credentials by email or directly to their wallet through their DID.

To send the credential by email, fill in their email in the **Recipient Email** field.

![](https://downloads.intercomcdn.com/i/o/797721246/2840f531c2020bf9df3a117c/64744417375359ce3af2c7ea\_1-email+distribution.png)

To send the credential directly to the holders wallet fill in their DID in the Subject ID (Recipient ID) field.

![](https://downloads.intercomcdn.com/i/o/797721371/4e40e894e866ea0da0b1d5f0/647443c237f7aab507122ff3\_2-DID+distribution.png)

Fill in all other attributes that need to be included in the credential _e.g. Subject name, Credential Title etc._

### Formatting the CSV file for recipient upload

You can download the CSV sample file to use as a base for you recipient data upload. The sample file has only 3 collumns with the _name_, _did_ and _date_ attributes.

<figure><img src="../.gitbook/assets/Screenshot 2024-01-29 at 17.22.04.png" alt=""><figcaption></figcaption></figure>

You will need to add columns and remove the ones you do not have in your credential schema.

When uploading a file you will be able to select a charset specification. UTF-8 will bet the choice for most users. If your dataset contains special characters you might need to choose a different charset, based on the one used to encode your data file.

<figure><img src="../.gitbook/assets/Screenshot 2024-03-21 at 16.19.02.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
If you do not know the holders dids you do not have to use it for the import, you can add emails, for the email distribution or distribute credentials manually.
{% endhint %}

You will be asked to match the columns on the csv file to the credential fields. If there are any required fields on the credential schema they must be filled in, otherwise the import will not be successful.

<figure><img src="../.gitbook/assets/Screenshot 2024-01-29 at 17.29.15.png" alt=""><figcaption></figcaption></figure>

### Expire credential <a href="#h_c9b588481e" id="h_c9b588481e"></a>

If you need the credential to expire, turn on the expiration toggle and enter the expiration date.

![](https://downloads.intercomcdn.com/i/o/797671954/0a79de9246c232395c2825c1/Screenshot+2023-08-01+at+14.52.52.png)

### Choose credential settings <a href="#h_e26a4957df" id="h_e26a4957df"></a>

After you have added your credential recipients you will be able to select the credential settings. First select which Organization Profile (DID) you want to use to issue the credentials.

<figure><img src="../.gitbook/assets/Screenshot 2024-01-25 at 16.27.06.png" alt=""><figcaption></figcaption></figure>

You have the options to:

* **Persist credential:** This option will encrypt the credential by providing a password to access it and store it on Dock’s servers. The credential can be accessed and verified by a URL or QR Code. The recipient can scan the QR Code to import the credential into a wallet app. The credential can be deleted from Dock’s cloud whenever you decide.
* **Generate PDF:** If you choose to persist the credentials, the PDFs will contain a QR code the recipient can scan to view and store their credential in their phone wallet app.
* **Credential revocation:** By choosing this you leave an option for the credential to be revoked to invalid state at any time. If you leave this option unchecked, the credential can never be revoked and will always be verifiable.
* **Anchor credentials:** This adds a hash of the credentials you issue on the Dock blockchain that can be referenced later to verify when and who created it.
* **Zero-Knowledge Proof:** Selecting this option will issue your credential with a Dock BBS+ signing scheme. This allows credential holders to share specific data rather than show the whole credential to enhance their privacy.

{% hint style="info" %}
Persisting is a good option for issuers if they want to securely store the credentials as a backup. It encrypts the credentials using Libsodium crypto secretbox Salsa20/Poly1305 algorithm and stores them on our servers that are located in the US and are powered by Amazon Web Services (AWS). Because the credential information is encrypted, Dock can’t access the information to ensure data privacy and security. ​
{% endhint %}

### Distribute credentials <a href="#h_22a510abcd" id="h_22a510abcd"></a>

If you have entered the holders DIDs to Subject ID the holder will receive the credential directly in their wallet without any additional communication needed.

![](https://downloads.intercomcdn.com/i/o/797749786/65a19e3bd9bdb27970ce16ea/e4aebe54-e4c5-46b4-b30e-1b9083b74a87.jpeg)

If you have entered the email address, you will have an option to write a message and preview the email that is going to be sent to the receiver of the credential.

<figure><img src="https://downloads.intercomcdn.com/i/o/797730898/839d62e93c6bb388f29eb493/Screenshot+2023-08-01+at+15.57.06.png" alt=""><figcaption></figcaption></figure>

If you do not have or want to use DIDs or email for credential distribution you can skip entering those details into the credential. System will notify you that there is no recipient data and credentials will have to be distributed manually.

![](https://downloads.intercomcdn.com/i/o/797753106/a79c8b3a06f8b9022db49223/Screenshot+2023-08-01+at+16.18.12.png)

Once the credential has been issued, it’s important that you download the credentials especially if you didn’t persist them otherwise you can’t get them back.

![](https://downloads.intercomcdn.com/i/o/797754454/75bc4cbf24590fcd6ec79e6c/Screenshot+2023-08-01+at+16.18.34.png)

## &#x20;<a href="#h_655a2ecaf5" id="h_655a2ecaf5"></a>
