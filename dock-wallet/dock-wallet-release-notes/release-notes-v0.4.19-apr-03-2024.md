# Release Notes v0.4.19 Apr 03, 2024

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
