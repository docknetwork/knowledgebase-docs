# Release Notes v.0.4.23 May 02, 2024

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
