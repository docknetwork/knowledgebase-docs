# Filtering, downloading and deleting credentials

### Filtering credentials <a href="#h_5ef77bc181" id="h_5ef77bc181"></a>

For easier management of the credentials issuers can filter the credential view table by Credential ID, Issue date (use YYYY-MM-DD format), Type (schema used) or subject reference.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-11-04 at 16.45.20.png" alt=""><figcaption></figcaption></figure>

### Downloading credentials <a href="#h_5ef77bc181" id="h_5ef77bc181"></a>

If you need to download an already issued credential you can do it by selecting credential you want to download and clicking Download.

{% hint style="warning" %}
For a credential to be downloadable you need to select [Persist Credential](https://help.dock.io/en/articles/8200914-issue-verifiable-credentials#h_e26a4957df) when issuing credentials. If the persisting was not selected upon creation the credential an encrypted copy is not stored on our servers and therefore can not be downloaded.
{% endhint %}

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-19 at 14.51.50.png" alt=""><figcaption></figcaption></figure>

### Deleting Credentials

If you don’t want to see a certain Verifiable Credentials in your account, select the ones you want to remove and click Delete. This does not delete the credentials themselves, it just removes them from the account view.

If the credential is not revocable, then the recipients will still have the credential in their wallet and be able to present it to verifiers because they have full ownership of it. Only credential holders will be able to delete the credential if they chose to.

If you wish to revoke the credential before deleting it see this [article.](../revoking-credentials.md)

<figure><img src="https://downloads.intercomcdn.com/i/o/797888254/e8fbbc3e7be024a587d7d93d/63e69f45b5c87181fe442538_14-digital+credential+platform+delete+credential+from+account+view.jpg" alt=""><figcaption></figcaption></figure>

