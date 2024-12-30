# 📊 System Architecture

## Architectural Overview

### Components

* Truvera API
  * AWS
    * us-west-1 (Northern California)
* Truvera Workspace
  * Vercel
    * us-west-1 (Northern California)
* Relay Service and EDV
  * Vercel
    * us-west-1 (Northern California)
  * MongoDB
    * us-west-1 (Northern California)
* Blockchain (Dock owned validators)
  * AWS
    * us-west-1 (Northern California)
    * us-east-1 (North Virginia)
    * us-east-2 (Ohio)
    * eu-central-2 (Zurich)
    * eu-west-2 (London)

### Truvera network diagram

<figure><img src="../.gitbook/assets/Screenshot 2024-12-23 at 13.17.00.png" alt=""><figcaption></figcaption></figure>

### Data Storage Details

Truvera strives to minimize the data it stores and works to follow SSI best practices of keeping private data with the individual it belongs to. Below we outline what data is used each component of our system.

Truvera API:

* Issuer metadata (name, logo, etc.)
* VC metadata (id, issue date, etc.)
* Subject reference field\*
* Verification history\*
* Persisted VC’s\* (optional)
* Raw credential data is only stored in memory during issuance and is dropped immediately after

_\* may contain PII_

Relay Service:

* Temporary storage of encrypted VC’s
* Can only be decrypted by recipient DID
* Message deleted once retrieved by recipient

### Blockchain

The blockchain used (if any) depends on the DID method selected when configuring an organization profile. A public blockchain provides Truvera users with assurance that their identity data is not locked-in to the platform. As long as the blockchain can be read, previously issued credentials in standard credential formats remain verifiable.

We recommend the [cheqd blockchain](https://cheqd.io/) built in the Cosmos ecosystem because it is mature, decentralized, public, and permissionless. The Truvera API abstracts the complexity of blockchain transactions and the associated token fees.

We are cautious that user PII, including hashed data, is never written to a public blockchain. User credential information is never written to the chain. Wallet DIDs are in DID:key format and are not stored on-chain.

<figure><img src="../.gitbook/assets/Truvera Client Architecture - Data Sovereignty.drawio.png" alt=""><figcaption></figcaption></figure>

