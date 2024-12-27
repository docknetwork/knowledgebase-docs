# Configuration

You will be invited to a dedicated Github repository, which will contain the files needed to customize, build and sign a white label build of the Truvera Wallet to be distributed in the Apple and Google Play stores.

## General Setup

First clone the GitHub repository to add the source code to your machine.

<figure><img src="../../../.gitbook/assets/Screenshot 2023-09-01 at 17.25.08 (1) (1).png" alt=""><figcaption></figcaption></figure>

First step is to to go through the documentation in [README.md](http://readme.md/).&#x20;

To make changes follow the instructions below and submit a pull request (PR) to this repository to be reviewed by the Truvera team. Once the changes are accepted a new release will be generated.

### Set the Application's Display Name & Package Id

First thing to do is setting the Application Display name and Package Id/Package Name.

:information\_source: _The package name uniquely identifies the app on the device; it is also unique in the Google Play store/ Apple App Store. This means that once you have published an app with this package name, you can never change it; doing so would cause your app to be treated as a brand new app, and existing users of your app will not see the newly packaged app as an update._

In ../app.json set the following fields

```
"displayName": <your application name>
"packageId": <your application package name>
"companyName": <your application package name>
"companyNamePossessive": <your application package name>

For example:
"name": "TruveraApp",
"displayName": "Cool Wallet",
"packageId": "com.coolwallet.app",
"companyName": "Cool",
"companyNamePossessive": "Cool's"
```
