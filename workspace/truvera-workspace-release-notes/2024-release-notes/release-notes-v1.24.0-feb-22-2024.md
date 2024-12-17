# Release Notes February 2024

## v1.24.0 February 22

### **Overview**

The Dock Certs 1.24.0 release introduces a suite of Ecosystem Tools with Trust Registry integration, enhancing the platform's capabilities in managing digital credentials within ecosystems. This update emphasizes flexibility, security, and scalability, ensuring that Dock Certs remains at the forefront of digital credential management solutions.

### **New Features**

#### **Trust Registry on Blockchain**

* **\[DCKA-2090] SDK/Chain Integration**: Store trust registry on the blockchain to enhance security and verifiability. Participants now need to consent before being added to an ecosystem, strengthening trust and compliance.

#### **Ecosystem Flexibility Enhancements**

* **\[DCKA-2341] Publicly Verifiable Schemas**: Ecosystem administrators can now specify schemas that are publicly verifiable, broadening the reach and applicability of issued credentials.
* **\[DCKA-2342] Issuance and Verification Schema Assignment**: Enables assigning different schemas for issuance and verification to ecosystem participants, catering to complex credential workflows.
* **\[DCKA-2346] Verification Template for Ecosystem Issuers**: Verifiers can create verification templates that accept credentials from all trusted ecosystem issuers for specified schemas, simplifying verifier workflows.

### **Enhancements**

#### **Scalability and Reliability**

* **\[DCKA-2283] Scalability Implementation Plan**: A detailed plan and breakdown to address scalability, ensuring Dock Certs can handle increased loads and maintain reliability at scale.

#### **User Experience and Usability**

* **\[DCKA-2360] CSV Import Charset Specification**: Users can now specify their charset when importing CSV files for bulk credential issuance, enhancing data compatibility and user control.

#### **Participant Management**

* **\[DCKA-2349] Self-removal from Ecosystems**: Participants can now remove themselves from an ecosystem, offering greater control and flexibility within the platform.

#### **Development and Compliance**

* **\[DCKA-2366] NPM Module License and Optionality Fixes**: Improved compliance and customization by adjusting NPM module usage and licenses.
* **\[DCKA-2368] Open Source License Check on PRs**: Implements checks for copy-left licenses in code contributions, ensuring compliance and protecting intellectual property.

### **Bug Fixes**

* **\[DCKA-2357] "Unmaintained" Badge Display Issue**: Fixed the issue where all ecosystems were showing an "Unmaintained" badge, ensuring accurate status representation.
* **\[DCKA-2359] Ecosystem About Section Button Fix**: Resolved an issue with the "More" button in the ecosystem about section, improving user interaction and information accessibility.
* **\[DCKA-2365] Credentials "Requested" Tab Error**: Addressed a bug causing errors when viewing the "Requested" tab on the Credentials screen, enhancing functionality.
* **\[DCKA-2373] "Learn More About" Display Fix**: Corrected the placement of the "Learn more about" link on the Credentials page, improving UI consistency.

## v1.23.0 February 9

### **Overview**

This release focuses on improving verification processes, ecosystem participation, and platform reliability, alongside critical bug fixes and user experience enhancements.

### **New Features**

#### **Enhanced Verification Security**

* **\[DCKA-2248] Verification Template DID Assignment**: Ensures the security of verification templates by requiring a signed message if a DID is present, preventing unauthorized DID assignments or QR code spoofing.

#### **Ecosystem Schema Integration**

* **\[DCKA-2307] Easy Proof Request Creation**: Developers can now easily create custom verification templates for proof requests using schemas assigned by the ecosystem administrator, streamlining the process of participating in an ecosystem.

#### **Ecosystem Participant Insights**

* **\[DCKA-2343] Participant List with Descriptions**: Ecosystem participants can view detailed descriptions of other participants, facilitating informed decisions about their participation in an ecosystem.

### **Bug Fixes**

* **\[DCKA-2328] Credential Validation Issue**: Addressed a critical issue where credentials became invalid after requested attributes were put in via the wallet.
* **\[DCKA-2160] Plan Upgrade Limits**: Fixed a bug where upgrading plans did not correctly update plan limits or reflect overage charges.
* **\[DCKA-2318 & DCKA-2321] Search Sensitivity and Signup Flow**: Improved user search functionality to be case-insensitive and ensured that Google account signups correctly trigger the signup flow.

### **Enhancements**

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

