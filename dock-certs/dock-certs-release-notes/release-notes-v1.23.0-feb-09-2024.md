# Feb 09, 2024 Release Notes v1.23.0

## **Overview**

This release focuses on improving verification processes, ecosystem participation, and platform reliability, alongside critical bug fixes and user experience enhancements.

## **New Features**

#### **Enhanced Verification Security**

* **\[DCKA-2248] Verification Template DID Assignment**: Ensures the security of verification templates by requiring a signed message if a DID is present, preventing unauthorized DID assignments or QR code spoofing.

#### **Ecosystem Schema Integration**

* **\[DCKA-2307] Easy Proof Request Creation**: Developers can now easily create custom verification templates for proof requests using schemas assigned by the ecosystem administrator, streamlining the process of participating in an ecosystem.

#### **Ecosystem Participant Insights**

* **\[DCKA-2343] Participant List with Descriptions**: Ecosystem participants can view detailed descriptions of other participants, facilitating informed decisions about their participation in an ecosystem.

## **Bug Fixes**

* **\[DCKA-2328] Credential Validation Issue**: Addressed a critical issue where credentials became invalid after requested attributes were put in via the wallet.
* **\[DCKA-2160] Plan Upgrade Limits**: Fixed a bug where upgrading plans did not correctly update plan limits or reflect overage charges.
* **\[DCKA-2318 & DCKA-2321] Search Sensitivity and Signup Flow**: Improved user search functionality to be case-insensitive and ensured that Google account signups correctly trigger the signup flow.

## **Enhancements**

#### **Documentation and Support**

* **\[DCKA-2179] Common Issue Resolution Documentation**: Provided detailed documentation on common issue resolutions, enhancing the support process for users and administrators.

#### **User Experience Improvements**

* **\[DCKA-2265 & DCKA-2271] UX and Dashboard Consistency**: Implemented a series of small UX improvements and ensured visual consistency across all Certs dashboards, enhancing the user experience.

#### **Ecosystem Integration and Usability**

* **\[DCKA-2282 & DCKA-2296] Team Management and Ecosystem Invites**: Enhanced email notifications regarding ecosystem changes and improved the UX for accepting ecosystem invites, allowing users to change teams more seamlessly.

#### **Platform Reliability and Testing**

* **\[DCKA-2326 & DCKA-2331] Improved Critical Failure Handling and Automated Testing**: Introduced better handling for critical failures and implemented automated tests for Certs ecosystem tools, increasing platform reliability.

#### **Ecosystem Tools and Management**

* **\[DCKA-2344] Ecosystem Defaulting**: For users part of multiple ecosystems, Certs now defaults to the most recently used ecosystem, streamlining the user experience.

#### **Menu and Tagging Adjustments**

* **\[DCKA-2293] Menu Tag Update**: Moved the "new" tag from Schemas to Ecosystems in the Certs menu, better highlighting the introduction of new features.

##
