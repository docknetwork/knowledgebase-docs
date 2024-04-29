# Release Notes v1.29.0 Apr 18, 2024

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
