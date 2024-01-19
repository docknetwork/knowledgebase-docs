# Issue Verifiable Credentials

### Issuing Credentials <a href="#h_c3a1aee140" id="h_c3a1aee140"></a>

In the Credentials menu, click Issue credentials.

![](https://downloads.intercomcdn.com/i/o/797669904/4c77143e4d9f9ce6f4f345fc/Screenshot+2023-08-01+at+14.47.45.png)

### Select a credential template <a href="#h_e6f35266ad" id="h_e6f35266ad"></a>

Select a pre-made credential template by clicking on it's name or [Create your own template](https://help.dock.io/en/articles/8201064-create-a-credential-template). You can click on Preview to see what attributes are included in the template.

![](https://downloads.intercomcdn.com/i/o/797670025/fc5ac03614def89819df7b28/Screenshot+2023-08-01+at+14.48.04.png)

### Select a design <a href="#h_662fe7eaa5" id="h_662fe7eaa5"></a>

Select a design or [create a new one](https://help.dock.io/en/articles/8201081-create-a-new-design) for your credentials. Alternatively, you can proceed without a design.

![](https://downloads.intercomcdn.com/i/o/797670108/d8f1948a00a9b8d934c5b070/Screenshot+2023-08-01+at+14.50.40.png)

### Add recipients <a href="#h_5fb66344c4" id="h_5fb66344c4"></a>

If you have many credentials to issue, you can issue them in bulk. To do this, select Import Spreadsheet.

![](https://downloads.intercomcdn.com/i/o/797670167/d0dbab0c2d32c4b8fb42882a/Screenshot+2023-08-01+at+14.51.00.png)

Download the sample CSV template and fill in the details needed for your credential template. Upload the completed .csv file back to Dock Certs.[ Read more how to correctly format the Spreadsheet for CSV upload.](https://help.dock.io/en/articles/8201104-import-from-spreadsheet)

![](https://downloads.intercomcdn.com/i/o/797695179/a28c99740299645f876ce8be/6356f7181e5260685afe7bd9\_9-Download+CSV.png)

If you want to add recipients one by one, select Add Manually.

![](https://downloads.intercomcdn.com/i/o/797700428/213956fd1fef006ab1f9adba/Screenshot+2023-08-01+at+14.51.00.png)

You can distribute your credentials by email or directly to their wallet through a DID.

To send the credential by email, fill in their email in the Recipient Email field.

![](https://downloads.intercomcdn.com/i/o/797721246/2840f531c2020bf9df3a117c/64744417375359ce3af2c7ea\_1-email+distribution.png)

To send the credential directly to the holders wallet fill in their DID in the Subject ID (Recipient ID) field.

![](https://downloads.intercomcdn.com/i/o/797721371/4e40e894e866ea0da0b1d5f0/647443c237f7aab507122ff3\_2-DID+distribution.png)

Fill in all other attributes that need to be included in the credential _e.g. Subject name, Credential Title etc._

### Expire credential <a href="#h_c9b588481e" id="h_c9b588481e"></a>

If you need the credential to expire, turn off expiration and enter expiration date.

![](https://downloads.intercomcdn.com/i/o/797671954/0a79de9246c232395c2825c1/Screenshot+2023-08-01+at+14.52.52.png)

### Choose credential settings <a href="#h_e26a4957df" id="h_e26a4957df"></a>

Select which Issuer Profile (DID) you want to use to issue the credentials.

![](https://downloads.intercomcdn.com/i/o/797708546/ada9869c6e3b399c5cea38e2/Screenshot+2023-08-01+at+15.34.15.png)

You have the options to:

* **Persist credential:** This option will encrypt the credential by providing a password to access it and store it on Dock’s servers. The credential can be accessed and verified by a URL or QR Code. The recipient can scan the QR Code to import the credential into a wallet app. The credential can be deleted from Dock’s cloud whenever you decide.
* **Generate PDF:** If you choose to persist the credentials, the PDFs will contain a QR code the recipient can scan to view and store their credential in their phone wallet app.
* **Credential revocation:** By choosing this you leave an option for the credential to be revoked to invalid state at any time. If you leave this option unchecked, the credential can never be revoked and will always be verifiable.
* **Anchor credentials:** This adds a hash of the credentials you issue on the Dock blockchain that can be referenced later to verify when and who created it.
* **Zero-Knowledge Proof:** Selecting this option will issue your credential with a Dock BBS+ signing scheme. This allows credential holders to share specific data rather than show the whole credential to enhance their privacy.

### Distribute credentials <a href="#h_22a510abcd" id="h_22a510abcd"></a>

If you have entered the holders DIDs to Subject ID the holder will receives the credential directly in their wallet without any additional communication needed.

![](https://downloads.intercomcdn.com/i/o/797749646/ccd7861183dd7a3d07a392dc/Screenshot\_20230801\_160347\_DockApp.jpg)![](https://downloads.intercomcdn.com/i/o/797749786/65a19e3bd9bdb27970ce16ea/e4aebe54-e4c5-46b4-b30e-1b9083b74a87.jpeg)

If you have entered the email address, you will have an option to write a message and preview the email that is going to be sent to the receiver of the credential.

![](https://downloads.intercomcdn.com/i/o/797730898/839d62e93c6bb388f29eb493/Screenshot+2023-08-01+at+15.57.06.png)![](https://downloads.intercomcdn.com/i/o/797731022/a4ca1c0385b4919197452603/Screenshot+2023-08-01+at+15.57.28.png)

If you do not have or want to use DIDs or email for credential distribution you can skip entering those details into the credential. System will notify you that there is no recipient data and credentials will have to be distributed manually.

![](https://downloads.intercomcdn.com/i/o/797753106/a79c8b3a06f8b9022db49223/Screenshot+2023-08-01+at+16.18.12.png)

Once the credential has been issued, it’s important that you download the credentials especially if you didn’t persist them otherwise you can’t get them back.

![](https://downloads.intercomcdn.com/i/o/797754454/75bc4cbf24590fcd6ec79e6c/Screenshot+2023-08-01+at+16.18.34.png)

If you chose to generate a PDF format, this is how your files will appear when you download the credentials:

![](https://downloads.intercomcdn.com/i/o/797765639/fe42442c912b2ded4a964613/6356f612c0a00c4c5380a8ed\_11a-PDF+and+JSON+credentials.png)

This is how the JSON file looks when you open it. JSON is used if you want to import this to a wallet or send it to another platform. A JSON file is a file that stores simple data structures and objects in JavaScript Object Notation (JSON) format, which is a standard data exchange format.

![](https://downloads.intercomcdn.com/i/o/797765858/b084dd886402eca1e5be9c27/6356f626d561c75a0316ad0d\_11b-JSON+contents.png)

This is an example of how a pdf credential can look:

![](https://downloads.intercomcdn.com/i/o/797766854/960c1aaeedfd789ac1cf4a2a/63e68b64a7726364e88277a1\_2-self-sovereign+identity+verifiable+credential.png)

This is how the credential looks when it is imported into the Dock Wallet:

![](https://downloads.intercomcdn.com/i/o/797766989/c7fb150f925ee058ec39220e/63e68ba046f3584041d1cf0f\_3-self-sovereign+identity+wallet+credentials.png)

## &#x20;<a href="#h_655a2ecaf5" id="h_655a2ecaf5"></a>
