# Holder messaging via DIDComm

Holder messaging enables secure, encrypted communication between organizations and digital wallet holders using the DIDComm protocol. This feature allows verifiers to send authenticated requests directly to credential holders' wallets, enabling real-time verification workflows without requiring traditional authentication methods.

### Example use case&#x20;

Consider a customer service scenario where enhanced identity verification is needed. A customer calls their bank to request a credit limit increase or password change. Rather than relying solely on traditional phone-based verification, the call center can leverage the customer's existing digital credentials for stronger authentication.

The process works as follows: the customer receives a credential during onboarding. The call center agent can initiate a credential verification request. The customer receives a secure message in their digital wallet via push notification, reviews the request, and responds using biometric authentication to unlock their wallet and confirm the data sharing.

### Technical implementation

#### Prerequisites

* Issuer has captured the holder's DID during credential issuance

#### **Encrypted message dispatch**

Uses the Truvera API to send an encrypted DIDComm message to the holders  DID. The message script:

```javascript
const axios = require("axios").default;
const API_KEY = ;//Your Truvera API key// 
const API_URL = "https://api-testnet.truvera.io";//for production https://api.truvera.io
const WALLET_DID = ;//Holders wallet DID//

const apiClient = axios.create({
  baseURL: API_URL,
  headers: {
    "Content-Type": "application/json",
    "User-Agent": "insomnia/9.3.2",
    Authorization: `Bearer ${API_KEY}`,
  },
});

async function sendYesNoMessage() {
  const payload = {
    type: "text",
    payload: {
      senderName: , //Name of the message sender DID//
      senderDid: , //Message sender DID//
      senderLogo: , //Logo of the message sender DID//
      title: "Are you currently speaking with our customer support team?",
      question:
        "This confirms you initiated the call and helps prevent fraud. Your personal information will not be shared.",
      yesText: "Yes",
      noText: "No",
      expirationDate: new Date(Date.now() + 1000 * 60 * 60 * 24).toISOString(),
      messageId: 'Internal-message-1234'//add a message ID to track the message
    },
    type: "https://schema.truvera.io/yes-no-payload-V1.json",
    senderDid: ,//the message sender DID//
    algorithm: "ECDH-1PU+A256KW",
    recipientDids: [WALLET_DID],
  };

  const { data: encryptedMessage } = await apiClient.post(
    "/messaging/encrypt",
    payload
  );
  console.log("Message encrypted successfully:", encryptedMessage);

  const sendPayload = {
    to: WALLET_DID,
    message: encryptedMessage.jwe,
  };

  const { data: sentMessage } = await apiClient.post(
    "/messaging/send",
    sendPayload
  );
  console.log("Message sent successfully:", sentMessage);
}


sendYesNoMessage();
```

#### **Response notification and retrieval**

Configure a webhook via the [API](../webhooks/) or the Truvera [Workspace](../../workspace/creating-api-keys-and-webhook-endpoints.md#h_fae99467a4) to listen to didcomm\_message\_received event.&#x20;

You can also get all the received messages using the API.

{% openapi-operation spec="dock-labs-api" path="/messaging/messages" method="get" %}
[OpenAPI dock-labs-api](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi-operation %}

To get the message content make an API call to retrieve the full response.

{% openapi-operation spec="dock-labs-api" path="/messaging/messages/{messageId}" method="get" %}
[OpenAPI dock-labs-api](https://swagger-api.truvera.io/openapi.yaml)
{% endopenapi-operation %}
