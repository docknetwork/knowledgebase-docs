# Caller authentication: Truvera Verified Contact

### Overview

Truvera Verified Contact reduces caller verification time up to 80% by replacing security questions with a biometric check through their existing app.

When a customer calls your support center, verification can be triggered automatically through your IVR system or manually by agents within your existing CRM. The customer receives a push notification in your company's mobile app, confirms with biometric authentication, and verification completes—all without the customer sharing any personal information verbally.

### How it works

Truvera Verified Contact uses two components working together to authenticate callers:

**Truvera API** - Handles secure communication between your call center systems and customer mobile apps using the [DIDComm protocol](https://book.didcomm.org/) for end-to-end encryption.

**Your existing mobile app** - The Truvera Wallet SDK integrates into your company's existing mobile application to handle decryption of DIDComm messages, display authentication prompts, collect biometric confirmation, and send cryptographically signed responses.

### Implementation requirements

#### Call center system integration

Truvera Verified Contact integrates into your existing call center infrastructure rather than requiring a separate portal. Integration points include:

**IVR/ACD integration (recommended)** - Automatically trigger verification requests during call routing, allowing authentication to complete before customers reach agents.

**CRM integration** - Add a verification button to your existing agent interface for manual triggering when needed.

**Technical requirements:**

* REST API integration capability in your IVR or CRM system
* Ability to display verification status in agent interface
* Customer identifier matching between your systems and mobile app (phone number, account ID, etc.)

[View API documentation](https://docs.truvera.io/truvera-api/messaging)

#### Mobile app SDK integration

The Truvera Wallet SDK integrates into your existing customer-facing mobile application, customers do not need to download a separate app. The SDK handles secure message decryption and manages the authentication flow within your app.

**SDK capabilities:**

* Receiving and decrypting encrypted verification requests via DIDComm
* Displaying authentication prompts to customers
* Collecting biometric confirmation
* Sending cryptographically signed responses

[View SDK documentation ](../credential-wallet/wallet-sdk/)

#### Customer onboarding

To use Truvera Verified Contact, you need to associate each customer's account with their wallet's DID (Decentralized Identifier). When you integrate the Truvera Wallet SDK into your mobile app, each instance generates a unique DID that can be retrieved and stored in your customer database.

**Basic setup flow:**

1. Customer installs or updates your mobile app with the integrated Truvera Wallet SDK
2. Your app retrieves the wallet's DID from the SDK
3. Your systems associate this DID with the customer's account record (linked by phone number, account ID, or other identifier)
4. Customer can now authenticate via push notification when calling support

Once you have the customer's DID, your call center systems can send encrypted DIDComm messages directly to their wallet without any additional credentials.

**Optional: Using verifiable credentials**

While not required for basic authentication, you may choose to issue verifiable credentials to customer wallets for enhanced functionality:

* Attribute-based verification (e.g., account tier, geographic location)
* Selective disclosure capabilities
* Additional cryptographic proof of account ownership

[View credential issuance documentation](../truvera-api/credentials.md)

### Key benefits

**Operational efficiency** - Reduces authentication time by up to 80%. With IVR integration, authentication completes during call routing, allowing agents to begin helping customers immediately upon connection.

**Cost reduction** - Eliminates per-message costs associated with SMS OTP solutions. Saves significant agent time costs from faster authentication.

**Enhanced security** - More resilient than knowledge-based authentication or OTPs, protecting against data breaches, SIM swaps, and phishing attacks.

**Privacy protection** - Eliminates the need for agents to access or hear sensitive personal information, reducing compliance liability and improving customer trust.

**Seamless customer experience** - Works within your existing mobile app that customers already use and trust—no separate download or registration required.

**Flexible implementation** - Integrates with existing call center infrastructure, supports both automated (IVR) and manual (agent-triggered) flows, enables step-up authentication for sensitive operations, and allows smooth re-verification when transferring between teams.
