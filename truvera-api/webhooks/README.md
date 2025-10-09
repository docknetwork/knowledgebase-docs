# Webhooks

We provide webhooks for asynchronous integration with the API. You can configure a webhook to receive notifications whenever events occur within the API (see below for the list of published events). To use our webhook, you need to set the webhook URL that acts as a receiver receiving the information whenever an event happens. You also need to select **at least one** of the webhook events from Truvera Workspace to trigger the data exchange.

## How to setup a webhook

To setup webhook, simply follow the steps below:

* Go to **Webhooks** in Truvera Workspace.
* Click **Add Endpoint**.
* Fill in the **Endpoint URL** and select **Endpoint Events** for the webhook events.
* Click **Create Webhook**.
* Once the webhook is created you will see a secret token. This token is sent in the webook POST request for you to validate that the webhook came from Truvera.

You can subscribe to all events by clicking **Receive All** next to **Endpoint Events**

## Webhook events

You can configure the following events to trigger the HTTP request to send the data to your application.

### credential\_create

This event indicates a credential has been created. It will fire when a credential has been created.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "credential_create",
  "data": {
    "id": "http://example.com/39",
    "signingOps": 1,
    "byteSize": 727,
    "key": "did:dock:5DhSFTFJwD6bFdrPdTibhxQypDruZkBGeWs1p34FS87ko5Vy#5GsBC74MW9DxHkFUYDVGPnbtioEaFgPgkdytQU3cRTQcHJCz",
    "credential": {
      "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1"
      ],
      "id": "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb",
      "type": [
        "VerifiableCredential"
      ],
      "credentialSubject": {
        "id": "did:dock:5DhSFTFJwD6bFdrPdTibhxQypDruZkBGeWs1p34FS87ko5Vy"
      },
      "issuanceDate": "2019-08-24T14:15:22Z",
      "expirationDate": "2019-08-24T14:15:22Z",
      "proof": {
        "type": "Sr25519Signature2020",
        "created": "2021-11-23T03:16:47Z",
        "verificationMethod": "did:dock:5DhSFTFJwD6bFdrPdTibhxQypDruZkBGeWs1p34FS87ko5Vy#keys-1",
        "proofPurpose": "assertionMethod",
        "proofValue": "z4jUYjc4CyQSfVCivjjTpngjg9TsSL5GkdNesqQFBxwtZwgruophe7xaAzFMSx2gZt4CmXhhhWz4aEyA9wtpqwhdn"
      },
      "issuer": {
        "id": "did:dock:5DhSFTFJwD6bFdrPdTibhxQypDruZkBGeWs1p34FS87ko5Vy",
        "name": "Issuer Name"
      }
    }
  }
}
```

</details>

### credential\_issued

This event indicates a credential has been issued. It will fire when a credential has been issued.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "credential_issued",
  "data": {
    "id": "http://example.com/39",
    "signingOps": 1,
    "byteSize": 691,
    "key": "did:dock:5DhSFTFJwD6bFdrPdTibhxQypDruZkBGeWs1p34FS87ko5Vy#5GsBC74MW9DxHkFUYDVGPnbtioEaFgPgkdytQU3cRTQcHJCz",
    "credential": {
      "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1"
      ],
      "id": "https://creds.dock.io/f087cbfabc90f8b996971ba47598e82b1a03523cb9460217ad58a819cd9c09eb",
      "type": [
        "VerifiableCredential"
      ],
      "credentialSubject": {
        "id": "did:dock:5DhSFTFJwD6bFdrPdTibhxQypDruZkBGeWs1p34FS87ko5Vy"
      },
      "issuanceDate": "2021-11-23T03:16:25.321Z",
      "proof": {
        "type": "Sr25519Signature2020",
        "created": "2021-11-23T03:16:25Z",
        "verificationMethod": "did:dock:5DhSFTFJwD6bFdrPdTibhxQypDruZkBGeWs1p34FS87ko5Vy#keys-1",
        "proofPurpose": "assertionMethod",
        "proofValue": "z41DNxuUzSvKz68L2YkXehR3nQ9PWoAfj6zk44gUzFXKK7pd2zEQByYAUGGg5TT2cZCxiYAmg49NGMX8tRLyf9W1G"
      },
      "issuer": {
        "id": "did:dock:5DhSFTFJwD6bFdrPdTibhxQypDruZkBGeWs1p34FS87ko5Vy",
        "name": "Issuer Name"
      }
    }
  }
}
```

</details>

### credential\_revoke

This event indicates a credential has been revoked. It will fire when a credential has been revoked.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "credential_revoke",
  "data": {
    "status": "finalized",
    "encodedTx": "0xa902040a0153b52f6bac3d812853d8aad9c94eb98b4a5dd632c5bf805dc4140965c753641e04aff1aa6770d43d684690c0ad679a8608d5b7576feb3fdc1d6712decf73ca44efd3ec3b0004483fc667eb8a63f8e040bb91cd23f6c650fb668d0152390a026620d05c5168ed00787db3a6322a4d81ab64848fdb4ec7f76404ad2360075b64e2de1c3d4bb0f2624d4684d073e528367a2dba2379254a50be816afa7eb731fa4f4807f1c6b4548f",
    "result": {
      "InBlock": "0x759314aa18d741335ac809ca2d877aed0a00375c3ba4a7dfc398d80dbc7bf2d5"
    }
  }
}
```

</details>

### credential\_unrevoke

This event indicates a credential has been unrevoked. It will fire when a credential has been unrevoked.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "credential_unrevoke",
  "data": {
    "status": "finalized",
    "encodedTx": "0xa902040a0253b52f6bac3d812853d8aad9c94eb98b4a5dd632c5bf805dc4140965c753641e04aff1aa6770d43d684690c0ad679a8608d5b7576feb3fdc1d6712decf73ca44ef45ed3b0004483fc667eb8a63f8e040bb91cd23f6c650fb668d0152390a026620d05c5168ed0052ced1926bc978029cf9ebe9107450961ca8f0aed21033b61087a901271e1451c67a1f8feb7851f8dda0913223fc3bb5a26b9550014dccce61b5392e9a5e3181",
    "result": {
      "InBlock": "0x4279f477c280d1721efaee8a3ee621f3d96068fe978811db73d4ab27fecc687a"
    }
  }
}
```

</details>

### did\_create

This event indicates a DID has been created. It will fire when a DID has been created.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "did_create",
  "data": {
    "status": "finalized",
    "encodedTx": "0x91010409004e0d07d7121cbfb78be48fea337f7afd6f90aa233e33c17ab8137c4873c7da924e0d07d7121cbfb78be48fea337f7afd6f90aa233e33c17ab8137c4873c7da920012e604ac480aa06981c9b5dae4fc0e0bd8961fd858584e0a53f8a66e9b5e1648",
    "result": {
      "InBlock": "0xe5f17466a3c4b2ac3f455d923367e6e2baf9970583c2ed56299280d3a269a471"
    }
  }
}
```

</details>

### did\_update\_key

This event indicates a `keyType` value within the DID has been updated. It will fire when the `keyType` value has been updated.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "did_update_key",
  "data": {
    "status": "finalized",
    "encodedTx": "0xa902040901c7f54544fc24f652c4bfd1eded6e26d4400cd2cc91f130f85076aee6f1f6efb2001eabe8649baa2de3ee613dd488a433f743ed36854843e2aef4317a924118487201483fc667eb8a63f8e040bb91cd23f6c650fb668d0152390a026620d05c5168ed15293c000030af292a54c9ac95c999dd746ae61b6f35e1b8e610a637ef7d8710c093826e6d7a01d665bbcc8e4825830711371dade0f78b604b39fa864e92911ed030e15181",
    "result": {
      "InBlock": "0x8c876bd6fe0dbbadc91ed04a5d9f811dca02850f95dda409e558034df24177bb"
    }
  }
}
```

</details>

### did\_update\_controller

This event indicates a `controller` value within the DID has been updated. It will fire when the `controller` value has been updated.

When you update both `controller` and `keyType`, you will receive `did_update_controller` event notification too on your webhook since updating `controller` value will update the `keyType` value.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "did_update_controller",
  "data": {
    "status": "finalized",
    "encodedTx": "0xad02040901c81cd739fdd090d889280f04ddec47cad8240290e974319eaf1a7d7f10213c500203d5dc1a348b80aa06673fc36b8d1c0405125ad61d90c43e157815cc0779a8696801483fc667eb8a63f8e040bb91cd23f6c650fb668d0152390a026620d05c5168ed822b3c000139a87a45eaf9ada41c964bada887ebffa7bf34d66aec88821fb7a6d2177d634e83ab7a45f685835add00cebcc96a8c572e2833ad01d6dcacb0f72fb9bf80fa0a",
    "result": {
      "InBlock": "0x47c6640633a8a22df1de8fdc8e80f36dc403e735975e6f14d1a30419a18a6abd"
    }
  }
}
```

</details>

### did\_delete

This event indicates a DID has been deleted. It will fire when a DID has been deleted.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "did_delete",
  "data": {
    "status": "finalized",
    "encodedTx": "0xa1010409024e0d07d7121cbfb78be48fea337f7afd6f90aa233e33c17ab8137c4873c7da92c0ea3b000008dcdfb22efd01604ca38facdb6c1086f2d76c2a36425f293e4c687e48f0ea295e02162e8af53f334544676bbf906f12f60d36a0b42dad89e169bc2816d68a85",
    "result": {
      "InBlock": "0x588b2170d114f68f47d697b92c4c2184db26deada7e114f205a6bb95a157a3bd"
    }
  }
}
```

</details>

### registry\_create

This event indicates a registry has been created. It will fire when a registry has been created.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "registry_create",
  "data": {
    "status": "finalized",
    "encodedTx": "0x1901040a0035cbd5b17285e74b86b198543f712c03c99b75d7e2ed82923fa1fde7f1129ef40004483fc667eb8a63f8e040bb91cd23f6c650fb668d0152390a026620d05c5168ed00",
    "result": {
      "InBlock": "0x2407aa20e16ae915698888ed84f41d1bc06d3733ed17c89041b897e91ecf8fac"
    }
  }
}
```

</details>

### registry\_delete

This event indicates a registry has been deleted. It will fire when a registry has been deleted.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "registry_delete",
  "data": {
    "status": "finalized",
    "encodedTx": "0x2502040a0335cbd5b17285e74b86b198543f712c03c99b75d7e2ed82923fa1fde7f1129ef443ec3b0004483fc667eb8a63f8e040bb91cd23f6c650fb668d0152390a026620d05c5168ed00405a766d239405e6e3c63104581168cbb831e32299f7af72e39b5e8774631674f41595542249599a454ce957374be99fc061ec40200d380a8df1776e4417fa82",
    "result": {
      "InBlock": "0x4c58ebd08823a2dd5d776eaed526bfeddacf988d79c8e85cd807e8765622de7a"
    }
  }
}
```

</details>

### schema\_create

This event indicates a schema has been created. It will fire when a schema has been created.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "4A_Z0fYD19q1qKZ03qAfB0zTu8XYuLPpGk0oHfP8OrvGGDi5Jz8C86F6EVz8Wd2c",
  "event": "schema_create",
  "data": {
    "status": "finalized",
    "encodedTx": "0xa106040b00e1420661c333988c024f0a4bd3ea4ed0e75773247a369419acdaa67447c22ca489047b2224736368656d61223a22687474703a2f2f6a736f6e2d736368656d612e6f72672f64726166742d30372f736368656d6123222c226164646974696f6e616c50726f70657274696573223a66616c73652c226465736372697074696f6e223a22446f636b20536368656d61204578616d706c65222c2270726f70657274696573223a7b22616c756d6e694f66223a7b2274797065223a22737472696e67227d2c22656d61696c41646472657373223a7b22666f726d6174223a22656d61696c222c2274797065223a22737472696e67227d2c226964223a7b2274797065223a22737472696e67227d7d2c227265717569726564223a5b22656d61696c41646472657373222c22616c756d6e694f66225d2c2274797065223a226f626a656374227d483fc667eb8a63f8e040bb91cd23f6c650fb668d0152390a026620d05c5168ed00c2d11f1a68160f1a7d926c7c89a937866d70fdd0b5d350a6b2be88ad099a8776c6518e1d798553f596baff8d3be36d0172860e7a9b1368019339c7da05bf3485",
    "result": {
      "InBlock": "0x8b7042e52223334929e1cb2507e9be5b35014573dbe693bbcda2952f6254934f"
    }
  }
}
```

</details>

### proof\_submitted

This event indicates that a proof has been submitted. Minimal data is included in the event but the details can be retrieved using the proof\_request API.

<details>

<summary>SAMPLE JSON PAYLOAD</summary>

```json
{
  "token": "15f2irRkZFz1tjOjGdA0cGh66abwd4ckC8pR2suxVIPt97yc_zDTQIiNkT20JqAm",
  "event": "proof_submitted",
  "data": {
    "id": "7fbbe582-66d6-4fbc-92f3-c13d9cf7975a",
    "verified": true
  }
}
```

</details>
