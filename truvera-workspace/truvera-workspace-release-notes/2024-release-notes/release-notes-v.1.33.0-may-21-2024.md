# Release Notes May 2024

## v.1.33.0 May 21

### **Overview:**

Certs v1.33.0 introduces a series of bug fixes and improvements aimed at enhancing the functionality and stability of the application.

### **Bug Fixes:**

* **DCKA-2288:** Fixed an issue where some fonts were missing on the PDF render server, ensuring accurate rendering of PDF documents.
* **DCKA-2589:** Resolved the "Secret key needs to be provided" error encountered when issuing a BBS+ revocable credential, ensuring smooth credential issuance.
* **DCKA-2590:** Addressed the 'Cannot add new DID key at this time of algorithm: dockbbs' error message received when attempting to create a BBS revocable credential, ensuring successful issuance without errors.
* **DCKA-2591:** Fixed the issue where proof templates were being returned multiple times in the API route, ensuring correct and consistent data retrieval.

### **Task:**

* **DCKA-2092:** Implemented bounds check in the proof presentation to validate the bounds since the cryptography library does not, ensuring data integrity and security.
* **DCKA-2542:** Ensured rejection of unsigned credentials in presentations for proof requests, enhancing security measures.
* **DCKA-2561:** Investigated and set up an autoscaling solution and AWS load balancer for the PDF render server, improving scalability and performance.

## v.1.32.0 May 08

### Overview

In this release of Dock Applications - Certs v1.32.0, we address several issues reported by users and introduced enhancements to improve the functionality and reliability of the platform. These updates aim to resolve PDF generation and opening issues, improve error handling for node connection failures, and ensure the default usage of BBS2023 for anonymous credentials, among other improvements.

### Bug Fixes

#### PDF Generation and Opening Issues

* **\[DCKA-2537] \[DCKA-2560]**: Fixed an issue where PDFs generated in Certs were not opening properly, as reported by users encountering errors when attempting to open PDF files. Additionally, a similar issue reported by Gravity, where PDF reports were not opening and resulted in a FUNCTION\_INVOCATION\_TIMEOUT error, has been addressed. These issues have been resolved to ensure that PDF files and reports can be generated and opened without any issues.

#### Accumulator Revocation Registries Key Pair Issue

* **\[DCKA-2513]**: Resolved an issue where accumulator revocation registries key pairs were incorrectly tied to a single DID. Now, each accumulator registry has a unique key per registry, ensuring proper functionality and security.

#### Unable to Open Downloaded VC Credentials File

* **\[DCKA-2526]**: Fixed an issue where downloaded VC credentials files could not be opened on staging using the testnet. Users encountered difficulties opening \*.pdf files after extraction. This issue has been resolved to allow seamless opening of downloaded VC credentials files.

### Tasks

#### Improved Error Handling for Node Connection Failures

* **\[DCKA-2523]**: Enhanced error handling for node connection failures to ensure that API alerts are more visible and actionable. Slack alerts now provide clearer indications of errors, and efforts have been made to trigger Zenduty alerts for enhanced monitoring and response to node connection failures.

#### Default Usage of BBS2023 for Anonymous Credentials

* **\[DCKA-2524]**: Updated the default usage of BBS2023 for anonymous credentials. With BBS formally proved in 2023, the platform now defaults to BBS2023 for anonymous credentials, ensuring alignment with industry standards and improved security.

#### Healthcheck PDF Rendering

* **\[DCKA-2544]**: Implemented improvements related to health checks of PDF rendering in the Dock API. This enhancement ensures more reliable rendering of PDF files, contributing to the overall stability and performance of the platform.

## v.1.31.0 May 01

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
