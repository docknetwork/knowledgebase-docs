# Release Notes April 2024

## v1.30.0 April 24

### Overview:

The release 1.30.0 includes improvements related to error message handling within ecosystem along with fixes related to plan upgrade popup and proof requests. Additionally, as part of this release, we have continued on the performance improvement initiative for anonymous credentials issuance.

### **Enhancements**

#### **Clear Error for Verifiers of Locked Credentials**

* **\[DCKA-2493]**: Implemented a feature to provide clear error messages to verifiers attempting to access locked credentials from ecosystems they are not members of. When a verifier outside of the ecosystem attempts to verify a locked credential, they now receive a message stating: "This credential can only be verified by participants in the \[ecosystem name] ecosystem. You can learn about the ecosystem by visiting this website: \[ecosystem website]". This enhancement aims to improve transparency and guidance for verifiers encountering locked credentials.

### **Bug Fixes**

#### **Upgrade Pop-up Issue**

* **\[DCKA-2518]**: Resolved an issue where the upgrade pop-up sometimes appeared when inviting team members, without displaying the close button. Users encountered difficulty closing the pop-up, impacting user experience. With this fix, the upgrade pop-up behaves as expected, ensuring smoother interaction when inviting team members.

#### **Proof Requests Missing ID**

* **\[DCKA-2521]**: Fixed a bug where proof requests did not contain an ID required by the latest PEX library. This issue prevented seamless processing of proof requests, leading to errors and inconsistencies. By addressing this bug, proof requests now include the necessary ID, ensuring compatibility with the latest PEX library.

### **Tasks**

#### **Anonymous Credential Issuance Performance Investigation**

* **\[DCKA-2459]**: Conducted an investigation into the performance of anonymous credential issuance. Test results revealed that issuing an anonymous credential took approximately 3 seconds on average, highlighting potential performance improvements. To address this, debug tracing was enhanced to identify slow points, and further investigation into the efficiency of BBS 2023 compared to BBS+ was initiated. This investigation aims to optimize the performance of anonymous credential issuance for enhanced user experience.

#### **URL Connectivity for PolkadotJS**

* **\[DCKA-2522]**: Provided a list of URLs to connect with PolkadotJS, enabling fallback connectivity. Users can now connect to a private API node and fallback to another URL if the primary connection fails. This enhancement ensures robust connectivity and resilience when interacting with PolkadotJS.

## v1.29.0 April 18

### Overview:

This release includes fixes for revocation registries, certs UX for create organization profile flow and enhancements related to ecosystems tools along with content updates for certs plans as per our revised offerings.

### **Bug Fixes**

#### **Update DID Drawer Issue**

* **\[DCKA-2507]**: Resolved an issue where clicking "Create Organization Profile" after editing a DID opened the same drawer instead of a new pop-up to create a new DID. This bug caused confusion and inconsistency in the user interface. With this fix, users can now seamlessly create new DIDs without encountering unexpected behavior.

#### **Registries Filtering Issue**

* **\[DCKA-2514]**: Addressed a bug where Certs failed to find a registry to use due to an issue with filtering registries. This bug affected the functionality of Certs, preventing users from effectively managing registries. By fixing the registry filtering API route, Certs can now accurately identify and utilize registries as intended.

#### **Incorrect Revocation Status for Anoncreds**

* **\[DCKA-2515]**: Fixed a bug where issuing revocable anoncreds with a previously used DID incorrectly showed as revoked when it wasn't. This issue stemmed from using the wrong public/private keypair, leading to inaccurate revocation status. With this fix, Certs now accurately reflects the revocation status of anoncreds, ensuring data integrity and reliability.

#### **New Registry Creation at Each Issuance**

* **\[DCKA-2516]**: Resolved an issue where a new registry was created at each issuance if not using BBS+. This behavior resulted in unnecessary proliferation of registries, leading to inefficiency and clutter. By fixing this issue, Certs now creates registries appropriately, optimizing resource utilization and improving system performance.

### **Tasks**

#### **Prompt Admin to Create Schemas Before Inviting Participants**

* **\[DCKA-2462]**: Implemented a feature to prompt ecosystem administrators to create schemas before inviting participants. This enhancement ensures that administrators have the necessary schemas prepared for participants, streamlining the onboarding process and avoiding potential delays or errors.

#### **Update Subscription Plan Names and Features**

* **\[DCKA-2508]**: Updated the names and feature lists for subscription plans in Certs to reflect recent pricing changes. The Business plan has been renamed to the Build plan, with corresponding feature adjustments. Additionally, the Custom Plan has been renamed to Scale, with updated features to align with the new plan structure. These updates provide clarity and accuracy regarding subscription offerings in Certs.

#### **Sales Demo Registry Optimization**

* **\[DCKA-2517]**: Optimized the sales demo to prevent the creation of a new revocation registry for each issuance. This enhancement reduces unnecessary registry creation, improving system efficiency and resource management.

## v1.28.0 April 14

### Overview:

This release includes updates to the user interface, improvements to verification template handling, bug fixes related to credential issuance, and tasks aimed at defining architecture for future features.

### **New Features**

#### **Optional Fields in Verification Templates**

* **\[DCKA-2468]**: Verification templates in Certs now support optional fields. Administrators can designate attributes as optional, enhancing flexibility in proof presentation responses.

#### **Ecosystem Membership Display in Organization Profiles**

* **\[DCKA-2417]**: Organization profiles now display the ecosystems where the organization profile is used. Additionally, ecosystem badges are included in the organization profile details, providing easy access to ecosystem information.

### **Bug Fixes and Improvements**

#### **BBS+ Credential Issuance Error**

* **\[DCKA-2501]**: Resolved an error where issuing BBS+ credentials resulted in a "Schema properties did not contain top-level key" error, ensuring smooth credential issuance processes.

#### **Revocation Status Error with did:polygonid Creation**

* **\[DCKA-2509]**: Fixed an issue where creating a new organization profile with a did:polygonid DID resulted in a "can't fetch revocation status" error, ensuring successful profile creation without errors.

### **Tasks and Research**

#### **Architecture Definition for Verifier Pays Issuer**

* **\[DCKA-2263]**: Defined the architecture for Verifier Pays Issuer, laying the groundwork for future implementation and facilitating transactions within the ecosystem.

#### **Wallet Cache Management Solution**

* **\[DCKA-2474]**: Introduced a basic key/value map for wallet cache management, with plans to expand functionality to include limiting cached wallets, clearing old values, and improving the interface for setting/getting values.

## v1.27.0 Apr 04

### Overview

Dock Certs 1.27.0 introduces significant updates to our pricing plans, enhanced credential management features, and important bug fixes and optimizations. These changes aim to streamline user experience, improve flexibility, and align our offerings with market demands and best practices.

### **New Features**

#### **Pricing Plan Updates 2024**

* **\[DCKA-2374]**: This release brings comprehensive updates to our pricing plans for 2024, reflecting changes in feature availability, trial duration, and subscription terms. Notable adjustments include the inclusion of Anonymous credentials and Encrypted credential backup features in the Free Trial plan, removal of the Starter Plan, and flexibility in seat management for Business and Custom plans.

#### **Anonymous Credentials Expiration**

* **\[DCKA-2467]**: Certs now automatically adds expiration dates to verification templates for anonymous credentials, ensuring consistent enforcement of expiration policies. Users can choose to remove expiration dates for maximum privacy or comply with specific privacy requirements.

### **Enhancements**

#### **Credential Creation Defaults**

* **\[DCKA-2134]**: Default credential creation settings have been optimized to align with best practices, encouraging simplicity and privacy. Key changes include the use of anonymous credentials for enhanced privacy and avoidance of persistent credentials to simplify PII management.

#### **Organization View UX Improvement**

* **\[DCKA-2431]**: The organization profile management has been revamped to improve usability and accommodate additional fields. It is now presented as a drawer instead of a pop-up when editing, providing a more spacious and intuitive interface for managing organization details.

#### **Verifier DID Profile Exposure**

* **\[DCKA-2475]**: Verifier DID profile name and logo are now exposed to proof request messages, enhancing verification processes and providing more context to credential recipients.

### **Bug Fixes and Maintenance**

#### **UI and UX Fixes**

* **\[DCKA-2457]**: Fixed button styling inconsistencies on the settings page, ensuring a symmetrical design and improved visual consistency.
* **\[DCKA-2477]**: Corrected the style of the cancel button and warning icon when declining invitations, ensuring a cohesive and intuitive user experience.

#### **Database Certificate Updates**

* **\[DCKA-2332]**: Updated certificates for RDS instances to comply with AWS requirements, ensuring secure connections and preventing connectivity issues.

### **API and Backend Improvements**

#### **Blockchain Transaction Fee Tracking**

* **\[DCKA-2476]**: Implemented tracking of blockchain transaction fees in the database, facilitating easier monitoring and analysis of transaction costs.

#### **KVAC Credential Issuance**

* **\[DCKA-2491]**: Introduced KVAC (Key Verified Anonymous Credential) issuance and verification capabilities via the API, enabling secure and privacy-preserving credential management.

### **Documentation and Infrastructure**

* **\[DCKA-2416]: Onboarding Form Update**: The job title field is now required in the onboarding form, ensuring completeness and accuracy of user profiles.
