# Create an Organization Profile (DID)

***

### What is a DID? <a href="#h_95e2ff9378" id="h_95e2ff9378"></a>

Decentralized identifiers (DIDs) are unique identifiers that are associated with a digital identity. DIDs are made up of a string of letters and numbers that can be stored on the blockchain and can be used to authenticate that identity.

### Create an Organization Profile (DID) <a href="#h_95e2ff9378" id="h_95e2ff9378"></a>

To create your organization profiles (DIDs) , select Organization Profiles on the left side menu and then click Create Organization Profile.

<div align="left" data-full-width="true">

<figure><img src="../.gitbook/assets/Screenshot 2024-01-19 at 14.11.19.png" alt=""><figcaption></figcaption></figure>

</div>

Fill in the Public Name, add the Logo and Public Description you can leave the DID Type to the default setting “dock” (learn more about different [DID Types](create-an-organization-profile-did.md#choosing-a-did-type)). Then select **Create Organization Profile**.

<div align="left">

<figure><img src="../.gitbook/assets/Screenshot 2024-01-19 at 14.13.24.png" alt="" width="188"><figcaption></figcaption></figure>

</div>

{% hint style="info" %}
The Logo image should not exeed 1MB in size. Accepted formats: 'jpeg', 'jpg', 'png', 'bmp'. Logo image can be square or round it will be optimized on display.
{% endhint %}

All of your profiles (DIDs) will be listed on this page.&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2024-04-18 at 16.33.22.png" alt=""><figcaption></figcaption></figure>

***

### Choosing a DID type

Many different types of DIDs exist today, they all support the same basic functionality, but they differ in how a DID is created or where and how the DID document is stored and retrieved.These different types of DIDs are known as DID methods. The second part of the DID identifier format—between the first and second colons—is called the DID method name.

Dock supports 3 types of DID methods did:key, did:dock and did:polygonid

<table><thead><tr><th width="153">Method</th><th width="184">Storage</th><th>Keys</th></tr></thead><tbody><tr><td>did:key</td><td>Stored on the user’s device</td><td>Only one key pair is attached to this DID type, if your keys get exposed you will need to change the DID and all the credentials associated to it</td></tr><tr><td>did:dock</td><td>Stored on the Dock blockchain</td><td>Multiple key pairs can be attached to this DID type, keys can be rotated as needed</td></tr><tr><td>did:polygonid</td><td>Stored on the Polygon blockchain</td><td>Only one key pair is attached to this DID type, if your keys get exposed you will need to change the DID and all the credentials associated to it</td></tr></tbody></table>

***

### Edit an Organization Profile (DID) <a href="#h_c1052e8bf2" id="h_c1052e8bf2"></a>

Click on Organization Profiles in the menu, click on the three dots of the DID you want to edit, and select **Update DID**.

<figure><img src="../.gitbook/assets/Screenshot 2024-01-19 at 14.38.28.png" alt=""><figcaption></figcaption></figure>

Update the details and select **Update DID**.

***

### Export an Organization Profile (DID) <a href="#h_157926b249" id="h_157926b249"></a>

Click on the three dots of the DID you want to export, and select Export DID.

<figure><img src="../.gitbook/assets/Screenshot 2024-01-19 at 14.38.28.png" alt=""><figcaption></figcaption></figure>

You can export your DID to a wallet or another platform. Create a password to encrypt the file and select Export.

![](https://downloads.intercomcdn.com/i/o/797658873/66234318d10e677cec479706/Screenshot+2023-08-01+at+14.37.22.png)

***

### Delete an Organization Profile (DID) <a href="#h_88118e48bc" id="h_88118e48bc"></a>

Click on the three dots of the DID you want to delete, and select Delete DID.

<figure><img src="../.gitbook/assets/Screenshot 2024-01-19 at 14.38.28.png" alt=""><figcaption></figcaption></figure>

{% hint style="warning" %}
Deleting your DID will make it unresolvable. This means that any credentials you issued with it will become invalid and it cannot be looked up on the blockchain anymore. Your associated key pair will also be deleted. This action cannot be undone.
{% endhint %}
