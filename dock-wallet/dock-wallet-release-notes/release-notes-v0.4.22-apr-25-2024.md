# Release Notes v0.4.22 Apr 25, 2024

### **Overview**

In this release, we focused on addressing customer-reported issues, fixing bugs, and enhancing the overall functionality and reliability of the Dock Mobile Wallet application. Additionally, we implemented tasks aimed at improving testing procedures to ensure a seamless user experience.

### **Bug Fixes**

#### **Landscape Mode Issues**

* **\[DCKM-191]**: Fixed landscape mode issues in the wallet app, including missing labels on navigation at the bottom and a mysterious blue bar that occupied half of the screen on the Scan screen. These issues no longer occur, providing a better user experience in landscape mode.

#### **Boolean Attribute Display**

* **\[DCKM-211]**: Addressed an issue where boolean attributes in verified credentials were not displayed correctly. With this fix, boolean attributes are now correctly displayed instead of just being labeled, ensuring accurate representation of credential information.

#### **PersonalData Credential Rendering**

* **\[DCKM-260]**: Fixed an error that prevented the rendering of PersonalData credentials in the wallet app. Users encountered errors when attempting to import PersonalData credentials, which are now resolved, allowing seamless rendering of custom schema credentials.

#### **Wallet VC Verification Flow**

* **\[DCKM-461]**: Resolved a critical issue where the wallet-to-wallet VC verification flow was broken. Users reported the verification process freezing at the waiting spinner stage. With this fix, the verification flow now proceeds smoothly, ensuring reliable VC verification between wallets.

#### **Export Debug Logs Issue**

* **\[DCKM-356]**: Resolved an issue where users were unable to export debug logs from the mobile app. Previously, attempting to export debug logs resulted in an error message or no action. With this fix, users can now export debug logs successfully, facilitating efficient troubleshooting and issue resolution.

#### **BBS+ Revocation Verification Error**

* **\[DCKM-453]**: Addressed a verification error encountered when verifying BBS+ credentials. Users reported receiving a VBAccumError during the verification process. The issue has been resolved, ensuring smooth verification of BBS+ credentials without errors.

#### **Android Wallet Open Badge Support**

* **\[DCKM-466]**: Resolved an issue where the Android wallet did not support Open badge functionality. Users encountered difficulties when attempting to scan QR codes. With this fix, the Android wallet now fully supports Open badge functionality, allowing users to scan QR codes seamlessly.

### **Tasks**

#### **End-to-End Test Error Prevention**

* **\[DCKM-377]**: Implemented measures to ensure that end-to-end tests do not generate errors. This enhancement improves the reliability and accuracy of testing procedures, contributing to overall system stability and performance.

#### **Integration Tests for Range Proofs**

* **\[DCKM-458]**: Added integration tests for range proofs in the wallet-sdk. These tests ensure the correctness and functionality of range proofs, providing developers with confidence in their implementation.
