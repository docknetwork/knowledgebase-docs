# Release Notes April 2024

## v0.4.22 April 25

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

## v0.4.21 April 18

### **Overview**

This release focuses on improving privacy compliance, addressing customer support issues, fixing bugs, and enhancing the Mobile SDK's accessibility and reliability. Additionally, integration tests for the wallet-sdk have been refined to ensure robust performance.

### **Story**

#### **iOS Privacy Manifest Update**

* **\[DCKM-431]**: Updated the iOS privacy manifest to ensure compliance with API usage requirements. This update ensures that the app adheres to Apple's privacy policies and regulations.

### **Bug Fixes**

#### **Verification Error with Specified Credential Type**

* **\[DCKM-417]**: Resolved an issue where an error message appeared during verification when a specific credential type was specified in the template creation. The error message "Properties does not exist" no longer occurs, ensuring smooth verification processes without interruptions.

#### **Error Message During Verification with Optional Field**

* **\[DCKM-450]**: Fixed an error message issue in the iOS Wallet where "Some of the revealed message names were not found" was displayed during verification when an optional field existed. This update ensures accurate error handling during verification, providing users with clear and relevant error messages.

#### **Quotient Wallet Error - "Obj needs to be an Object"**

* **\[DCKM-452]**: Addressed an error in the Quotient wallet where users encountered the message "Obj needs to be an Object" when attempting to obtain an auto loan and select credentials for presentation. This fix eliminates the error message, enabling users to proceed with the desired actions smoothly.

#### **Quotient Wallet Biometrics Issue**

* **\[DCKM-454]**: Fixed a bug in the Quotient wallet where biometrics were not prompted upon verification. This issue occurred when a biometric credential expired, and the wallet suggested using the expired credential without requesting a new biometric. With this fix, the wallet now correctly prompts users for a new biometric credential when necessary, ensuring a seamless verification process.

### **Tasks**

#### **Mobile SDK Publication**

* **\[DCKM-393]**: Published the Mobile SDK's Git repository to facilitate evaluation, adoption, and collaboration. The repository is licensed under the Dock Labs Non-Production License (DL-NPL) and does not contain sensitive information. Additionally, it has been published to NPM for easy access and integration.

#### **Wallet-SDK Integration Tests**

* **\[DCKM-432]**: Fixed integration tests in the wallet-sdk and implemented a GitHub action to run these tests on each commit. This ensures the reliability and stability of the wallet-sdk, providing developers with confidence in its functionality.

#### **App Version Update Issue**

* **\[DCKM-335]**: Resolved an issue where the app version was not updated, causing obstacles in uploading the app to the iOS App Store.

## v0.4.20 April 15

## **Overview**

This release includes updates on improved handling of nested credentials attributes, Expiry Date Support improvements and enhancement related to ecosystem credential display in the dock wallet.

## **Bug Fixes**

#### **Nested Credential Attribute Display Issue**

* **\[DCKM-401]**: Resolved an issue where nested credential attributes were not being correctly displayed in the wallet. Values nested within the biometric context now appear under the group name, improving attribute identification and user experience.

#### **Expiry Date Support in Wallet**

* **\[DCKM-435]**: Fixed a bug where the wallet was unable to handle expiry dates present in verifiable credentials (VC) and was getting stuck on the processing which is now fixed ensuring smoother user interactions.

## **Tasks and Enhancements**

#### **Alerts and Monitoring Review**

* **\[DCKM-289]**: Conducted a review of the current alerting and monitoring system, identifying actions required to improve it. Efforts were made to ensure that the correct alerts are automatically routed to the appropriate individuals, enhancing system reliability and responsiveness.

#### **Documentation of Ecosystem APIs in Wallet SDK**

* **\[DCKM-298]**: Documented the ecosystem APIs in the Wallet SDK, providing comprehensive overview and reference documentation along with at least one example. This documentation aims to assist developers in effectively utilizing ecosystem APIs for wallet integration.

#### **Verifier Ecosystem Badge Display**

* **\[DCKM-391]**: Implemented a feature where the holder is shown applicable ecosystem information for the verifier when scanning a presentation request QR code. The ecosystem badge for the verifier is prominently displayed at the top of the credential selection screen, improving user understanding and interaction.

## v0.4.19 April 03

## **Overview**

This release includes updates to comply with iOS SDK requirements, improvements to ecosystem credential handling, and enhancements to biometric credential management.

## **New Features**

#### **Upgrade to iOS 17 SDK**

* **\[DCKM-365]**: The wallet now utilizes the iOS 17 SDK, ensuring compliance with Apple's requirements. This update enables seamless submission to the App Store Connect and ensures compatibility with the latest iOS ecosystem.

#### **Publicly Verifiable Ecosystem Credentials**

* **\[DCKM-366]**: Ecosystem administrators can now designate certain schemas as "publicly verifiable," expanding the reach of credential verification. Verifiers who are not ecosystem participants can verify presentations containing publicly verifiable schemas without requiring ecosystem membership.

#### **Short-Lived Biometric Check Credential**

* **\[DCKM-403]**: Biometric check credentials now have a short lifespan of 2 minutes, ensuring enhanced security by requiring a new credential for subsequent presentation requests.

## **Bug Fixes and Improvements**

#### **Enhanced Wallet-to-Wallet Verification**

* **\[DCKM-329]**: Resolved issues related to wallet-to-wallet verification, ensuring a seamless flow and successful verification process.

## **UI/UX Enhancements**

* **\[DCKM-396]**: Increased the clickable area for the "i" target related to ecosystem information, improving accessibility and user experience.
* **\[DCKM-398]**: Biometric check credentials now contain minimal information, optimizing privacy and security.
* **\[DCKM-404]**: Fixed issuer information for biometric credentials, ensuring consistency and accuracy in credential issuance.
* **\[DCKM-409]**: Resolved account export/import issues, ensuring smooth functionality for exporting and importing wallet accounts.
* **\[DCKM-424]**: Fixed error message display during verification, ensuring clarity and accuracy in the verification process.

## **Task and Research**

#### **Wallet API Research**

* **\[DCKM-334]**: Conducted research on Wallet APIs, exploring potential enhancements and optimizations for future releases.

#### **Biometric Service Provider Enhancement**

* **\[DCKM-394]**: Improved security by ensuring that the default biometric service provider does not have a public API key, enhancing protection against unauthorized access.
