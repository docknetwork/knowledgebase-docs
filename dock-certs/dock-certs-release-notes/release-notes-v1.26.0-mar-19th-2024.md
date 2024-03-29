# Release Notes v1.26.0 Mar 19th 2024

## Overview

This release brings significant improvements to credential verification within ecosystems, updates documentation links across the platform, and addresses key user feedback and bug fixes to streamline the Dock Certs experience.

## **New Features**

#### **Ecosystem Credential Verification**

* **\[DCKA-2270]** Verifiers now have the ability to see an ecosystem badge during credential verification, providing immediate visibility into whether a credential is part of an ecosystem they participate in. This ensures users can easily identify credentials issued by trusted ecosystem participants.

#### **Enhanced Documentation Access**

* **\[DCKA-2390]** All links within Dock Certs have been updated to point to the new Documentation Portal. This change ensures users have direct access to the most current and comprehensive guidance available, improving ease of use and support.

#### **Ecosystem Tools Documentation**

* **\[DCKA-2317]** Comprehensive end-user documentation for Ecosystem Tools has been introduced, covering everything from ecosystem administration to participation. This documentation is designed to help users maximize the benefits of Dock Certs’ ecosystem functionalities.

## **Enhancements**

#### **Billing Plan Clarification for Ecosystem Tools**

* **\[DCKA-2363]** The billing plans for ecosystem tools have been finalized, detailing which functionalities are available for different tiers. This clarification helps administrators and participants understand their access and capabilities within the ecosystem tools feature set.

#### **Verification History Sorting**

* **\[DCKA-2407]** Verification history now prioritizes the most recent verifications, with the “Created” column displaying timestamps for precise tracking.

## **Bug Fixes**

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
