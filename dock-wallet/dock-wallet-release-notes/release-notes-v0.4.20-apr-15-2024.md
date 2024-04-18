# Release Notes v0.4.20 Apr 15, 2024

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
