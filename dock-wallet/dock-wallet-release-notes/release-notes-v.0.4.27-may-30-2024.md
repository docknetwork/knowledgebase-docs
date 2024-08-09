# Release Notes May 2024

## v.0.4.27 May 30

### **Overview:**

This update of Dock Mobile Wallet includes improvements and tasks aimed at enhancing the functionality and reliability of the application.

### **Story:**

* **DCKM-243:** Implemented an update to the credential card UI to display verifier pays issuer (VPI) support. The credential card now fetches the credential status from the wallet-sdk and updates the UI accordingly if VPI is enabled for the credential.

### **Task:**

* **DCKM-293:** Added a test to detect Subscan API changes. This integration test ensures that any changes to the Subscan fee API are promptly detected and addressed.
* **DCKM-491:** Designed the proxy service as part of the ongoing effort to create a wallet services API for making common actions more efficient.&#x20;

## v.0.4.26 May 23

### **Overview:**

This release of Dock Mobile Wallet introduces enhancements, bug fixes, and documentation updates to improve the user experience and functionality of the application.

### **Bug Fixes:**

* **DCKM-445:** Fixed an issue where white label apps were not sending Sentry events due to the build process not pulling the proper Sentry certificates from the certs repository.
* **DCKM-481:** Resolved a bug where scanning the QR code of a revoked BBS+ credential did not redirect the user to the imported VC as expected.

### **Story:**

* **DCKM-438:** Implemented a feature to disable KVAC in the wallet-to-wallet verification flow. Now, during verification, if the credential is KVAC, the checkbox is disabled, and the holder cannot select this credential. The KVAC badge is displayed, and verifiers see an error message indicating that this credential requires payment, which is not supported during wallet-to-wallet verification. Additionally, tapping the badge displays a message informing the user that this credential is not supported in the wallet-to-wallet verification flow.

## v.0.4.25 May 16

### Overview

Dock Mobile - Wallet 0.4.25 introduces several improvements and bug fixes including updates to the wallet-sdk logic for determining if a credential requires verifier pays issuer (VPI) flow, fixes for issues related to credential list updates when switching networks, and improvements in the wallet import process to ensure seamless credential display. Additionally, tasks have been completed to enhance the biometric plugin's user experience and support KVAC (verifier pays issuer) in proof presentations and proof of non-revocation.

### Bug Fixes

#### Credential List Update Issue on Network Switch

* **\[DCKM-475]**: Resolved an issue where the credential list was not updated when switching networks. Users encountered difficulties in viewing updated credential lists after switching networks, impacting the overall usability of the wallet application.

#### Redirection Issue During Wallet Removal Process

* **\[DCKM-485]**: Fixed a bug where users were not redirected to the settings menu screen after selecting the "Skip" action during the wallet removal process. This issue caused confusion and inconsistency in the user interface flow.

#### Credentials Display Issue After Fresh Wallet Import

* **\[DCKM-487]**: Addressed an issue where credentials were not displayed immediately after importing a fresh wallet backup. Users experienced difficulties in viewing imported credentials without additional effort, leading to frustration and inconvenience.

### Tasks

#### Explainer Screen for Default Biometric Plugin

* **\[DCKM-392]**: Implemented an explainer screen for the default biometric plugin, providing users with context before requesting a biometric sample. This enhancement aims to improve user understanding and transparency regarding biometric authentication processes.

#### Support for KVAC in Proof Presentations

* **\[DCKM-429]**: Added support for KVAC (verifier pays issuer) protocol in proof presentations. This task ensures that proof presentations adhere to the KVAC protocol when a credential requires payment by the verifier, enhancing the security and integrity of proof presentations.

#### Support for KVAC in Proof of Non-Revocation

* **\[DCKM-430]**: Implemented support for KVAC protocol in proof of non-revocation. This enhancement ensures that the status validation for proof of non-revocation follows the KVAC protocol when a credential requires payment by the verifier, improving the reliability of non-revocation checks.

## v.0.4.24 May 10

### Overview

This release of Dock Mobile - Wallet 0.4.24 focuses on addressing various bugs reported by users, as well as implementing enhancements to improve the functionality and user experience of the mobile wallet application.

### Bug Fixes

#### Android Notifications Missing Icon

* **\[DCKM-201]**: Fixed an issue where Android notifications were missing the app icon in the notification tray. Users reported that notifications did not include the app icon, impacting the visibility and recognition of notifications on Android devices.

#### Transaction History Entries Not Updated

* **\[DCKM-387]**: Addressed an issue where entries for "Sent" and "Received" transactions were not updated in the transaction history. While token reduction and addition were functioning correctly, the counts for sent and received entries remained the same in the transaction history. This issue has been resolved to ensure accurate tracking of transaction history.

#### Wallet Notification Not Received for VC Distribution via DID

* **\[DCKM-426]**: Resolved an issue where wallet notifications were not received when a verifiable credential (VC) was sent via DID distribution. Users did not receive notifications on their phone screens after successful issuance of VCs. This issue has been fixed to ensure that users receive notifications for VC distribution via DID.

### Tasks

#### Supply List of URLs for Connectivity with Polkadotjs

* **\[DCKM-463]**: Completed the task of providing a list of URLs to connect with polkadotjs. This enhancement allows users to have fallback options for connectivity, ensuring seamless interaction with the polkadotjs ecosystem. The [mainnet-node.dock.io](http://mainnet-node.dock.io) and [mainnet-node-2.dock.io](http://mainnet-node-2.dock.io) URLs have been provided for users' convenience.

## v.0.4.23 May 02

### **Overview**

In this release, we focused on fixing bugs related to Quotient Wallet, Credentials Revoked Status display, and transaction history enhancing the overall functionality and reliability of the Dock Mobile Wallet application. Additionally, we implemented tasks aimed at improving wallet built process and upgrading SDK to support Open Badges credentials.

### **Story**

#### **Quotient Wallet Default to Testnet**

* **\[DCKM-448]**: Implemented a solution to set the testnet as the default mode when Quotient wallet is installed. This change aims to address issues encountered when testing the sales demo app on mainnet. The default setting can be configured in the white label configs, ensuring seamless operation for various white label solutions.

### **Bug Fixes**

#### **Revoked Status Display Issue**

* **\[DCKM-345]**: Resolved an issue where the revoked status of credentials was not displayed correctly in the Wallet. Previously, even after revoking a credential, the Wallet continued to display it as "Verified". With this fix, the Wallet now accurately reflects the revoked status of credentials, enhancing transparency and security.

#### **Restriction Warning for Mainnet Biometric Flow**

* **\[DCKM-385]**: Implemented a warning to restrict users from scanning the "Verification" of Biometric flow if they are on mainnet. This precautionary measure helps prevent issues as the Biometric flow is intended for testnet use only, ensuring a smoother user experience.

#### **Error Prompt for Test Mode in Quotient Wallet**

* **\[DCKM-442]**: Fixed an issue where users were not prompted with an error message when attempting to scan a proof request in live mode without enabling test mode in the Quotient wallet. Now, users receive a clear error message indicating the need to switch to test mode, facilitating quick resolution of the issue.

#### **Transaction History Fetching Issue**

* **\[DCKM-468]**: Addressed a problem where transaction history was not fetched in mainnet. With this fix, the transaction history retrieval process now functions correctly, providing users with accurate and up-to-date transaction records.

### **Tasks**

#### **Update Subscan APIs Deprecated**

* **\[DCKM-354]**: Updated Subscan APIs that are being deprecated to ensure continued compatibility and functionality of the wallet. This update is related to the Subscan APIs being consumed within Dock  wallet and does not impact the end users.

#### **Network Configurations Build Step Enhancement**

* **\[DCKM-455]**: Enhanced the build process by injecting network configurations as a build step rather than hard-coding them in the react-native codebase. This improvement allows for easier support of different networks in various builds and removes hard-coded URLs from the codebase.

#### **SDK Upgrade After Open Badge Changes**

* **\[DCKM-472]**: Upgraded the SDK after Open Badge changes to ensure compatibility and smooth operation of the Wallet. This upgrade ensures that credentials can be imported without errors and remain valid within the Wallet.

