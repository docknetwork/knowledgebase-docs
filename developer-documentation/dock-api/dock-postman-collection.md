# Dock Postman Collection

Download and use our [Postman Collection](https://github.com/docknetwork/api-docs/blob/main/Dock%20API.postman\_collection.json) to experiment with basic API flows:

* Download Postman [here](https://www.postman.com/downloads/).
* Download our [API collection here](https://github.com/docknetwork/api-docs/blob/main/Dock%20API.postman\_collection.json).
* Import Dock Collection in Postman with our API collection that you have downloaded previously. For the detailed instructions to import the json file, please refer [here](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/).
* Create a new environment in Postman. For the detailed instruction to create a new environment, please refer [here](https://learning.postman.com/docs/sending-requests/managing-environments/).
* In your new Postman environment, you need to create two new `ApiKey` and `BaseUrl` variables. Please refer [here](https://learning.postman.com/docs/sending-requests/variables/) for the instructions to set the new variables.
* Login to [Dock Certs](https://certs.dock.io/).
* Enable the **Test mode** in your Dock Certs dashboard to use the sandbox environment.
* In your Dock Certs dashboard, click **Create API key** on the keys page to generate the key, copy and save it.
* Set `ApiKey` initial and current values with the value that you generated in Dock Certs.
* Set `BaseUrl` initial and current values with [https://api-testnet.dock.io](https://api-testnet.dock.io)

## Simple E2E Create Credentials/Presentation Flow

This flow refers to Postman, but the general steps are the same however you use the API. The Postman collection includes the scripts that automatically propagate results into the next request bodies when you follow the below steps. To issue a credential and or a presentation on the holder's behalf, the following steps are required:

### 1. Create a DID

To create a new DID to issue with, go to **Create DID** and click **Send**. The `id` property denotes a job ID in the system that you can use to query for blockchain transaction status.

The Dock API supports `did:dock`, `did:polygonid` and `did:key` method creation.

<details>

<summary>DID CREATED - 200 Response</summary>

```json
{
    "id": "823",
    "data": {
        "did": "did:dock:5FDFd1Woa3cG1m18PLgPpYgGfwE5S1RqXyHeEYC86vUxzzkg",
        "hexDid": "0x8b3997a95f86c80e5eb8a4ab67dbb164d5cc19ea24c072a85a3eb0d552fa837f",
        "controller": "did:dock:5FDFd1Woa3cG1m18PLgPpYgGfwE5S1RqXyHeEYC86vUxzzkg"
    }
}
```

</details>

{% hint style="info" %}
Creating a Dock DID submits a transaction to the blockchain, this could take some time to process. Please hit the \`/jobs\` endpoint to check the status of the job to see if it's finalized or not.
{% endhint %}

{% hint style="info" %}
When creating a Polygon ID DID, be sure to set the \`keyType\` field to \`bjj\`.
{% endhint %}

### 2. Verify the New DID

To verify if the new DID has been registered, go to **Verify DID Registered** and click **Send**.

<details>

<summary>DID VERIFIED - 200 Response</summary>

```json
{
    "@context": "https://www.w3.org/ns/did/v1",
    "id": "did:dock:5FDFd1Woa3cG1m18PLgPpYgGfwE5S1RqXyHeEYC86vUxzzkg",
    "authentication": [
        "did:dock:5FDFd1Woa3cG1m18PLgPpYgGfwE5S1RqXyHeEYC86vUxzzkg#keys-1"
    ],
    "assertionMethod": [
        "did:dock:5FDFd1Woa3cG1m18PLgPpYgGfwE5S1RqXyHeEYC86vUxzzkg#keys-1"
    ],
    "publicKey": [ ... ]
}
```

</details>

{% hint style="info" %}
You only need to create a DID once and then you can issue many credentials with it. A subject/holder DID should not be the same as the issuer DID in a real world credential.
{% endhint %}

### 3. Create a Signed Credential

To create a Verifiable Credential using the the new issuer DID, go to **Create Signed Credential** and click **Send**. This will send some example credential data to the API and sign it with your DID keypair. It will return a Verifiable Credential that conforms to the W3C spec.

<details>

<summary>CREDENTIAL ISSUED - 200 Response</summary>

```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1"
    ],
    "id": "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb",
    "type": [
        "VerifiableCredential"
    ],
    "credentialSubject": {
        "id": "did:dock:5FDFd1Woa3cG1m18PLgPpYgGfwE5S1RqXyHeEYC86vUxzzkg"
    },
    "issuanceDate": "2021-11-12T14:43:46.504Z",
    "proof": { ... },
    "issuer": { ... }
}
```

</details>

### 4. Verify the Signed Credential

To verify if the credential's cryptographic proof, revocation status and more go to **Verify Signed Credential** and click **Send**.

<details>

<summary>CREDENTIAL VERIFIED - 200 Response</summary>

```json
{
    "verified": true,
    "results": [ ... ]
}
```

</details>

### 5. Create a Presentation

To create a Verifiable Presentation by using the credential, go to **Create Presentation** and click **Send**.

<details>

<summary>PRESENTATION CREATED - 200 Response</summary>

```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1"
    ],
    "verifiableCredential": [
        {
            "@context": [
                "https://www.w3.org/2018/credentials/v1",
                "https://www.w3.org/2018/credentials/examples/v1"
            ],
            "id": "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb",
            "type": [
                "VerifiableCredential"
            ],
            "credentialSubject": {
                "id": "did:dock:5FDFd1Woa3cG1m18PLgPpYgGfwE5S1RqXyHeEYC86vUxzzkg"
            },
            "issuanceDate": "2021-11-12T14:43:46.504Z",
            "proof": { ... },
            "issuer": { ... }
        }
    ],
    "id": "https://creds.dock.io/presentation/adfb13f1a4b8934d0e94d2aa507e006c",
    "type": [
        "VerifiablePresentation"
    ],
    "proof": { ... }
}
```

</details>

### 6. Verify the Presentation

The same credential verification route can be used to verify a presentation. In Postman, go to **Verify Presentation** and click **Send**.

<details>

<summary>PRESENTATION VERIFIED - 200 Response</summary>

```json
{
    "verified": true,
    "results": []
}
```

</details>

{% hint style="info" %}
These steps involve using the API to create presentations on behalf of your holders. Ideally, you should not do this and distribute the credential to your users and have their own wallet apps create the presentations for a verifier.
{% endhint %}

