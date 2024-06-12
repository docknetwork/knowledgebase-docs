# Release Notes v.0.4.26 May 23, 2024

### **Overview:**

This release of Dock Mobile Wallet introduces enhancements, bug fixes, and documentation updates to improve the user experience and functionality of the application.

### **Bug Fixes:**

* **DCKM-445:** Fixed an issue where white label apps were not sending Sentry events due to the build process not pulling the proper Sentry certificates from the certs repository.
* **DCKM-481:** Resolved a bug where scanning the QR code of a revoked BBS+ credential did not redirect the user to the imported VC as expected.

### **Story:**

* **DCKM-438:** Implemented a feature to disable KVAC in the wallet-to-wallet verification flow. Now, during verification, if the credential is KVAC, the checkbox is disabled, and the holder cannot select this credential. The KVAC badge is displayed, and verifiers see an error message indicating that this credential requires payment, which is not supported during wallet-to-wallet verification. Additionally, tapping the badge displays a message informing the user that this credential is not supported in the wallet-to-wallet verification flow.
