# Feb 22, 2024 Release Notes v.1.24.0

## **Overview:**

The Dock Certs 1.24.0 release introduces a suite of Ecosystem Tools with Trust Registry integration, enhancing the platform's capabilities in managing digital credentials within ecosystems. This update emphasizes flexibility, security, and scalability, ensuring that Dock Certs remains at the forefront of digital credential management solutions.

## **New Features**

#### **Trust Registry on Blockchain**

* **\[DCKA-2090] SDK/Chain Integration**: Store trust registry on the blockchain to enhance security and verifiability. Participants now need to consent before being added to an ecosystem, strengthening trust and compliance.

#### **Ecosystem Flexibility Enhancements**

* **\[DCKA-2341] Publicly Verifiable Schemas**: Ecosystem administrators can now specify schemas that are publicly verifiable, broadening the reach and applicability of issued credentials.
* **\[DCKA-2342] Issuance and Verification Schema Assignment**: Enables assigning different schemas for issuance and verification to ecosystem participants, catering to complex credential workflows.
* **\[DCKA-2346] Verification Template for Ecosystem Issuers**: Verifiers can create verification templates that accept credentials from all trusted ecosystem issuers for specified schemas, simplifying verifier workflows.

## **Enhancements**

#### **Scalability and Reliability**

* **\[DCKA-2283] Scalability Implementation Plan**: A detailed plan and breakdown to address scalability, ensuring Dock Certs can handle increased loads and maintain reliability at scale.

#### **User Experience and Usability**

* **\[DCKA-2360] CSV Import Charset Specification**: Users can now specify their charset when importing CSV files for bulk credential issuance, enhancing data compatibility and user control.

#### **Participant Management**

* **\[DCKA-2349] Self-removal from Ecosystems**: Participants can now remove themselves from an ecosystem, offering greater control and flexibility within the platform.

#### **Development and Compliance**

* **\[DCKA-2366] NPM Module License and Optionality Fixes**: Improved compliance and customization by adjusting NPM module usage and licenses.
* **\[DCKA-2368] Open Source License Check on PRs**: Implements checks for copy-left licenses in code contributions, ensuring compliance and protecting intellectual property.

## **Bug Fixes**

* **\[DCKA-2357] "Unmaintained" Badge Display Issue**: Fixed the issue where all ecosystems were showing an "Unmaintained" badge, ensuring accurate status representation.
* **\[DCKA-2359] Ecosystem About Section Button Fix**: Resolved an issue with the "More" button in the ecosystem about section, improving user interaction and information accessibility.
* **\[DCKA-2365] Credentials "Requested" Tab Error**: Addressed a bug causing errors when viewing the "Requested" tab on the Credentials screen, enhancing functionality.
* **\[DCKA-2373] "Learn More About" Display Fix**: Corrected the placement of the "Learn more about" link on the Credentials page, improving UI consistency.

