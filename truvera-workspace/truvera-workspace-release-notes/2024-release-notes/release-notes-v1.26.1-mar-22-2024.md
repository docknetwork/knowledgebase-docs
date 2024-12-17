# Release Notes March 2024

## v1.26.1 March 22

### **Overview**

This release addresses specific needs identified by our ecosystem administrators and enhances the overall functionality and usability of Dock Certs.

### **New Features**

#### **Ecosystem Participant Onboarding**

* **\[DCKA-2377]** Administrators can now assign relevant schemas for issuance and verification directly when inviting a new participant to an ecosystem. This streamlines the setup process, enabling participants to contribute immediately after accepting their invitation.

#### **Subscription Management**

* **\[DCKA-2379]** Introduced a "Sync with Stripe" button on the account page to manually synchronize subscription data with Stripe. This feature allows for immediate correction and update of subscription details, ensuring accurate billing and service delivery.

### **Enhancements**

#### **License Compliance**

* **\[DCKA-2358]** Implemented an action in Dock JS repositories to detect GPL/AGPL packages and reject them, reinforcing our commitment to maintaining license compliance across all JavaScript projects.

#### **Verification History Management**

* **\[DCKA-2385]** API calls have been added to allow deletion of individual entries or all history for a specific verification template. This offers more flexibility in managing verification data in compliance with privacy policies and data retention guidelines.

#### **Ecosystem Tools Access for Subscribers**

* **\[DCKA-2445]** Updated the Certs database to ensure that all existing subscribers benefit from the ecosystem tools according to the licensing rules established in the previous release. This ensures all users have appropriate access to these powerful tools.

### **Bug Fixes**

#### **Trial Account Onboarding**

* **\[DCKA-2424]** Fixed an issue where expired trial accounts were incorrectly taken through the new onboarding process, which could not be completed due to the expired status. Now, onboarding will not initiate for expired trials, and any failed issuance during onboarding will redirect users to the dashboard, avoiding any disruption.

#### **UI and Data Display**

* **\[DCKA-2451]** Addressed a UI issue where participant names overlapped field boundaries in the ecosystem section. Improved logic and UX design ensure that participant information is displayed cleanly and legibly.

## v1.26.0 March 19

### Overview

This release brings significant improvements to credential verification within ecosystems, updates documentation links across the platform, and addresses key user feedback and bug fixes to streamline the Dock Certs experience.

### **New Features**

#### **Ecosystem Credential Verification**

* **\[DCKA-2270]** Verifiers now have the ability to see an ecosystem badge during credential verification, providing immediate visibility into whether a credential is part of an ecosystem they participate in. This ensures users can easily identify credentials issued by trusted ecosystem participants.

#### **Enhanced Documentation Access**

* **\[DCKA-2390]** All links within Dock Certs have been updated to point to the new Documentation Portal. This change ensures users have direct access to the most current and comprehensive guidance available, improving ease of use and support.

#### **Ecosystem Tools Documentation**

* **\[DCKA-2317]** Comprehensive end-user documentation for Ecosystem Tools has been introduced, covering everything from ecosystem administration to participation. This documentation is designed to help users maximize the benefits of Dock Certs’ ecosystem functionalities.

### **Enhancements**

#### **Billing Plan Clarification for Ecosystem Tools**

* **\[DCKA-2363]** The billing plans for ecosystem tools have been finalized, detailing which functionalities are available for different tiers. This clarification helps administrators and participants understand their access and capabilities within the ecosystem tools feature set.

#### **Verification History Sorting**

* **\[DCKA-2407]** Verification history now prioritizes the most recent verifications, with the “Created” column displaying timestamps for precise tracking.

### **Bug Fixes**

#### **UI and Functional Improvements**

* **\[DCKA-2396]** Resolved an issue where the name of a recipient was displayed multiple times for the same schema within an ecosystem.
* **\[DCKA-2406]** Fixed a complex and broken flow in deleting schemas, ensuring a smoother schema management experience.
* **\[DCKA-2411]** Addressed a bug in the ecosystems participants table refresh and save state indication.
* **\[DCKA-2419]** Corrected team switching errors within ecosystems, preventing "cannot find trust registry" messages.
* **\[DCKA-2426]** Fixed a display issue where deleting an organization profile showed it as "unnamed" until the page was refreshed.
* **\[DCKA-2429 & DCKA-2437]** Improved UI alignment in the "assign schemas to participants" table and fixed schema issuance errors with numbers/integers.

#### **Enhanced User Experience**

* **\[DCKA-2409]** Updated all Certs links to point to the correct sections within the new documentation portal, ensuring users are directed to relevant information efficiently.
* **\[DCKA-2420]** Improved the error message when using an invitation link for a deleted ecosystem, enhancing clarity and user guidance.
* **\[DCKA-2448]** Added a "Book a Demo" Calendly link to the ecosystem empty mainpage, facilitating easy access to personalized support and demonstrations.

## v1.25.0 March 07

### Overview

This release includes significant improvements on Dock Certs, focusing on making the Ecosystem Tools feature production-ready and introducing several enhancements and fixes. This feature along with all the below mentioned improvements is currently behind a feature flag and only available to internal users and beta testers.

### **New Features**

#### **Ecosystem Landing Page**

* **\[DCKA-2258]** To help users who are not subscribed to Ecosystem Tools we have added a landing page inside certs to better understand the benefits of this feature.

#### **Ecosystem Schema Management**

* **\[DCKA-2281]** **Admin Schema Assignment**: Ecosystem admins can now add schemas to their ecosystem with ease, either from the schema table or participant view. This includes the ability to select from existing schemas, mark those already in the ecosystem, and assign them to participants. A "create new schema" option is also now available for greater flexibility.

#### **Improved Ecosystem Participation**

* **\[DCKA-2376] Participant Role Automation**: The process of setting participant roles has been automated based on assigned schemas, removing the need for manual role selection and simplifying the ecosystem management experience
* **\[DCKA-2351] Ecosystem Administrator Visibility:** On the ecosystem view, the participant will now be able to see who is the administrator of the ecosystem.
* **\[DCKA-2299] Ecosystem Admin Participation:** Ability for ecosystem admins to add their organization profiles on relevant ecosystem roles and participate.

### **Enhancements**

#### **User Experience Improvements**

* **\[DCKA-2361] UX Cleanup**: Several user experience improvements have been implemented, including UI consistency enhancements, clearer empty state prompts, and more intuitive navigation elements.

#### **Default Schemas and Templates**

* **\[DCKA-2295] Badge Markings for Defaults**: Default schemas and verification templates are now marked with a badge to distinguish them from user-created items, enhancing clarity and usability .
* **\[DCKA-2245] Ecosystem verification Templates: Verification templates inside an ecosystem are available to all ecosystem verifiers.**

### **Bug Fixes**

* **\[DCKA-2353]** **Ecosystem Creation Labeling**: Updated terminology from "Convener" to "Ecosystem Administrator" across the platform for consistency and clarity.
* **\[DCKA-2362]** **Invitation Process Streamlining**: Fixed an issue where accepting invitations required logging in twice, now allowing users to proceed directly to the invitation acceptance page after login.
* **Ecosystem Schema and Participant Management Fixes**:
  * \[DCKA-2394] 400 error fix when trying to assign schema to a participant
  * \[DCKA-2397] Fix for error on duplicated schema assignment when original was deleted
  * \[DCKA-2399] Fix for job failure error when updating participant information.

