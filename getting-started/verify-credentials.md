# Verify Credentials

## Verification process <a href="#h_d119e38335" id="h_d119e38335"></a>

In the verification process, there are three main parties:

1. Issuer: Party that creates and issues a Verifiable Credential to a holder (individual or organization)
2. Holder: Person or organization that holds the credential (e.g. degree, professional certificate, or identity document)
3. Verifier: Party that checks that the credential is valid and authentic

![](https://downloads.intercomcdn.com/i/o/801931889/c9976b09a48fe6e88920e78a/631f7526f09bcf3b4b2e6209\_3-certificate+fraud-issuer%2C+holder%2C+verifier.jpeg)

## Steps for the Verifier <a href="#h_4638f9252a" id="h_4638f9252a"></a>

❗ Verification request templates can only be created in Dock Certs, not the wallet. These templates can be important into the wallet from Dock Certs for wallet-to-wallet verification.

Click on Verification in the left menu and select Create verification template

![](https://downloads.intercomcdn.com/i/o/801933692/5203a19c476d97fd6531e65f/63dd39a9db4a3e2a50cf9e20\_1-Create+a+verification+template+.png)

First, type in the template title and template purpose, which the holder will be able to see.

Optionally, you can choose a Verifier DID which will be shown to the holder so that they can verify who you are.

![](<../.gitbook/assets/Screenshot 2024-01-19 at 15.00.55.png>)

The verifier can choose which credential details the holder is required to send in order for the credential to be accepted.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2024-01-19 at 15.03.35.png" alt=""><figcaption></figcaption></figure>

The list will have all attributes that are included in the credential templates - schemas, therefore if you want to include an attribute to the verification template it has to be included in at least one of your credential templates.

For Zero Knowledge Proof credentials you can use range proof verification conditions that will verify the credential without disclosing the actual value of that attribute. For example if you want to verify that the holder is older than 18 you can choose attribute Age and condition is greater than 18.

![](<../.gitbook/assets/Screenshot 2024-01-19 at 15.11.23.png>)

Last step for a verification request is to click Request, which will generate a QR code. Every time a new request is made, it generates a new QR code.\
​

![](https://downloads.intercomcdn.com/i/o/801942152/e6f4175aa1923403d2509951/63dc133a7f9006477e2c9e15\_4-select+request.png)

## Steps for the Holder <a href="#h_551a4bc680" id="h_551a4bc680"></a>

First step for the Holder is to scan the QR code with their wallet and select the credential(s) that contain the information the verifier is requesting.

![](https://downloads.intercomcdn.com/i/o/801943894/2a128a33ac2dd9ef2ef8391f/63dc147a07bea77af71f759a\_1-select+Verifiable+Credentials.png)

If the credentials were issued with [Zero Knowledge Proof signatures](https://help.dock.io/en/articles/8223764-zero-knowledge-proof-signatures) the holder will be able to choose which details on the credentials to share with the verifier.

![](https://downloads.intercomcdn.com/i/o/801947490/0b185ff2f10af16683eb8a88/63dc15a7115db97d3d27ffa6\_2-uni+selective+disclosure.png)



If the credentials are valid and the verification is successful, this is what the holder will see.

![](https://downloads.intercomcdn.com/i/o/801948125/699766b45be84fc4789b2466/63dc17aa818e23242e079689\_6-credential+verificaiton+successful.png)

If the credentials are not valid, the verification will fail and this is what the holder will see:

![](https://downloads.intercomcdn.com/i/o/801948297/5adc23ec2eeeb1ce8bf1c6d0/63dc1885de0cb2965586d87d\_9-credential+verification+failed.png)

For the verifier to see a log of all your verification requests, go to Verification>History

![](https://downloads.intercomcdn.com/i/o/801948701/e62394c921696d957bcd9fde/63dc17caa81c505860578114\_7-select+history.png)

When the credentials are valid it will show up as “Verified” under Status. The verifier won’t get a notification if the credential is invalid because Dock’s tools won’t let the holder submit invalid credentials.

![](https://downloads.intercomcdn.com/i/o/801948999/996e97fbbc669281dff49d03/63dc17fdac49966e2cfebd6c\_8-credential+verified+and+requested.png)

## Wallet-to-Wallet Verification <a href="#h_9833d67c15" id="h_9833d67c15"></a>

After creating the verification request in Dock Certs it can be imported in to the wallet for a wallet-to-wallet verification.

Go to Settings and choose Credential Verifier.

![](https://downloads.intercomcdn.com/i/o/801963474/f0e42a69cd04be5cb000afa0/Screenshot\_20230807\_140939\_DockApp.jpg)

Click Import via QR code.

![](https://downloads.intercomcdn.com/i/o/801963734/25223c44489a69890998611e/393c66b9-cd1e-4828-9866-68027bca228f.jpeg)

After the Verification presentation is imported you can share it with the holder to present and verify their credential.

![](https://downloads.intercomcdn.com/i/o/801966471/8b2b8552b1276fc19e7bc89d/Screenshot\_20230807\_141402\_DockApp.jpg)![](https://downloads.intercomcdn.com/i/o/801966603/b402e7174ad1418e09682394/Screenshot\_20230807\_141406\_DockApp.jpg)

Holder will scan this QR code with their Dock Wallet and get a presentation request message, choose the credential, and select Continue.

![](https://downloads.intercomcdn.com/i/o/801976550/2b69f8a9b9e780f39264ce53/Screenshot\_20230807\_142653\_DockApp.jpg)

Select which details from that credential you want to share. The requested attributes will be highlighted.

![](https://downloads.intercomcdn.com/i/o/801977630/bb5c9ed31f3af980d469a9e5/Screenshot\_20230807\_142709\_DockApp.jpg)

If the credential is valid, it would say Verification Successful for the holder.

![](https://downloads.intercomcdn.com/i/o/801978611/b792766a23d2acdf8d28586a/Screenshot\_20230807\_142737\_DockApp.jpg)

The verifier will see that the credential is valid on their wallet as well. The verifier will not receive any credential if the verification is not valid.
