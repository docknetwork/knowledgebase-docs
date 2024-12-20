# How Data is Processed and Stored

Truvera is designed to balance the requirements of user convenience with privacy and security. This document explains how we make those trade-offs in each part of the platform. This document does not replace the \[Dock Labs Master Services Agreement] or \[Data Processing Agreement], but provides additional insight into our architecture and practices.

The Truvera platform is intended to be deployed within a user-facing identity solution configured by a customer of Dock Labs or one of our integration partners. The security and privacy characteristics of the delivered solution might be different from the characteristics of the Truvera platform documented here. We attempt to call out relevant security considerations in the discussion below.

Truvera Workspace and API Organizations use Truvera’s API to set up their identity solution and interact with credentials. In order to make the system easy to use, Truvera stores the organization’s information in the system database. Data which is intended to be private, such as the private keys used to establish ownership of Decentralized IDentifiers (DIDs) and for signing, is encrypted on a per-row basis for each organization. Other data in the database includes presentation templates, PDF designs, verification templates, ecosystem membership, and activity logs. Data which is intended to be public, such as schemas and organization profile logos, is stored in AWS S3 with a public URL. Organizations can set up subaccounts to track the solution information of their customers. There is no way for an organization to access the information of a different organization. Depending on the DID method selected when setting up an organization profile, organization DIDs, revocation registries, and ecosystem information also may be stored on an external blockchain for public access (see below).

Organizations use the API or Truvera Workspace to submit credentials for issuance. These credentials often contain PII of the credential holder. This information is deleted immediately after processing.

Similarly, organizations use the API or Truvera Workspace to verify credential information shared as part of a proof presentation. This information is stored until it is delivered to the verifier either synchronously or via a webhook. The verifier should then call the delete endpoint to purge the information from Truvera.

Organization information is accessible in two ways: 1) through a Truvera Workspace account that is part of the organization’s team and which is protected by an email address or oAuth federated login or 2) through an API key. Users are encouraged to carefully protect these methods of system access. Should access be abused, team members can be removed from an organization and API keys can be revoked.

The Truvera Workspace uses Firebase and Google Analytics to track anonymized user activity so that we can improve the service for all users.

Truvera Credential Wallets Credential holders store their credentials in a Truvera Credential Wallet built with the Truvera Wallet SDK. There are two options for storing credentials: on-device or in the cloud.

On-device storage keeps all credential data in an Encrypted Data Vault (EDV). This is usually used in mobile applications, as persistent browser storage can be challenging to configure. Though the process for unlocking the wallet can be customized, mobile applications that use on-device storage will generally put the key for the wallet in the mobile operating system’s keystore. Dock Labs does not have access to the encryption keys or credential data.

Wallet applications can also be configured to use Truvera’s cloud wallet for storage. Our SaaS cloud wallet is an EDV that stores information for multiple users in the same vault. The information is end-to-end encrypted using a key generated in the application. This key is normally derived from a biometric configured by the developer integrating our platform into a user-facing identity solution. A hash of the encryption key is used as the index to the holder’s credential data in the EDV. Credentials can be searched by field name, but the field contents are opaque. Dock Labs does not have access to the encryption keys, but the identity solution that generates the key must be trusted by the user to not access their wallets inappropriately. Credential data that is stored in the cloud wallet may also be cached in the EDV of the edge device for quick access and offline use.

Solution developers can also choose to host their own EDV service accessible by the Truvera Wallet SDK. The API of that service is the same as the Truvera SaaS cloud wallet, but its security posture could be significantly different. Holders should investigate the design of any identity wallet that they use.

Truvera has a deprecated feature to persist issued credentials so that holders can later import them into a wallet using a password provided by the issuer. Instead of using this feature, we recommend setting up a cloud wallet using the user’s biometric collected during verification with the issuer and issuing the credential into that wallet. If it is not possible to set up a wallet, a credential offer should be given to the holder which will result in the credential being issued when the offer is accessed by the holder’s wallet.

Other wallet information may be stored unencrypted in the wallet database, such as the DID:keys associated with the wallet. Credential data is transmitted through a relay service which allows Truvera to route messages to the correct wallet using one of its DIDs. Communication with the relay service is done with encrypted messages using the DIDComm Mediator protocol and the messages are deleted once they are retrieved by the client. These messages are delivered to the correct mobile application with push notifications using Google Firebase.

Truvera’s white label wallets use Firebase and Google Analytics to track anonymized user activity so that we can improve the service for all users.

General Considerations The SaaS components of the Truvera platform are hosted in the United States (AWS Northern California Availability Zone). European data is processed under the terms of the US-EU Data Sharing Standard Contractual Clauses which are incorporated into our MSA.

Logging for our production systems does not contain PII of any kind. Logging on our public test systems may contain customer information when an error is reported, so we encourage customers not to use real PII when issuing test credentials. We perform internal audits to ensure that our practices conform with this policy.

The above mentioned data storage is preserved in nightly encrypted backups for disaster recovery.

As noted above, some data is stored on a blockchain in order to provide our customers assurance that their identity solution is not locked-in to our services. The specifics of blockchain storage will depend on the DID method selected. Our default blockchain is did:cheqd, which is a Cosmos based proof-of-stake network with a globally diverse set of validators. Information about organizations may be stored on a blockchain, such as organization DIDs, ecosystem information such as the participating organizations, and revocation registries.

Holder information is never stored on a blockchain, with the exception of credential revocation status which is stored in a privacy preserving manner. Revocation registries based on the W3C Bitstring Status List are used in many solutions, though they allow some types of verifier correlation. We also support an accumulator based revocation registry with improved privacy characteristics. You can learn more \[in the relevant documentation].

The Truvera system will continue to evolve to give our customers more control over how their data is stored and processed. If you have any questions about how we process data, please contact our support team.
