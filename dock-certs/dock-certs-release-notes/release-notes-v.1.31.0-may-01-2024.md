# Release Notes v.1.31.0 May 01, 2024

### **Overview**

In this release of Dock Applications - Certs v1.31.0, we introduce several bug fixes and enhancements aimed at improving security, functionality, and usability of the Certs platform. These updates address various issues reported by users and enhance key features to provide a more seamless experience for our users.

### **Bug Fixes**

#### **Account Name Validation Enhancement**

* **\[DCKA-2499]**: Implemented validation for account names in Certs to prevent the inclusion of URLs. Previously, account name text fields lacked validation, allowing any characters to be used and potentially leading to malicious activities. With this fix, validation has been added to ensure that only appropriate characters are accepted, enhancing security and preventing potential vulnerabilities.

#### **Anoncreds Verification Issue with Required Fields**

* **\[DCKA-2502]**: Resolved an issue where anoncreds verification failed if a schema had required fields that were not revealed. The SDK now removes the required option during schema validation and only checks types/values, ensuring accurate and reliable verification of anoncreds credentials.

#### **Fix for publicKeyMultibase Invalid Header Bytes**

* **\[DCKA-2530]**: Addressed an issue related to publicKeyMultibase invalid header bytes for DIDComm messaging.

### **Tasks**

#### **Support for Ed25519-2020 Keys**

* **\[DCKA-2527]**: Added support for Ed25519-2020 keys for signing and verification in the Dock SDK/API. This enhancement expands the capabilities of the SDK/API, allowing users to utilize Ed25519-2020 keys for cryptographic operations.
