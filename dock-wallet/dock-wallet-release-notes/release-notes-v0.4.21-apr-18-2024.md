# Release Notes v0.4.21 Apr 18, 2024

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

