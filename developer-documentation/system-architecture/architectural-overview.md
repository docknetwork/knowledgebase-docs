# Architectural Overview

### Components

* API
  * AWS
    * us-west-1 (Northern California)
* Certs
  * Vercel
    * us-west-1 (Northern California)
* Relay Service and EDV
  * Vercel
    * us-west-1 (Northern California)
  * MongoDB
    * us-west-1 (Northern California)
* Blockchain
  * AWS
    * us-west-1 (Northern California)
    * us-east-1 (North Virginia)
    * us-east-2 (Ohio)
    * eu-central-2 (Zurich)
    * eu-west-2 (London)

### Dock network diagram

<figure><img src="../../.gitbook/assets/Screenshot 2024-05-29 at 15.38.23.png" alt=""><figcaption></figcaption></figure>

### Storage Details

Dock API:

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

<figure><img src="https://lh7-us.googleusercontent.com/-p6BNQn6-xSP97KXXHEzQ1pOurKt-Ro5TBvay19l-yY-xDfvtwolovKZnKwB_mTl5A_3xoyAQgzT3Rh236pcn1ZI4mRZ8adwtL2lVapFBf-xVwVYJ81U0cf7UKHnaHTH-XRmKveXoiPtx_CsV_1ZGT9D=s2048" alt=""><figcaption></figcaption></figure>
