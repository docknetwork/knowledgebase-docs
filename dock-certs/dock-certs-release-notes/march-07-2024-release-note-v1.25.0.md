# March 07, 2024 Release Notes v1.25.0

## Overview

This release includes significant improvements on Dock Certs, focusing on making the Ecosystem Tools feature production-ready and introducing several enhancements and fixes. This feature along with all the below mentioned improvements is currently behind a feature flag and only available to internal users and beta testers.

## **New Features**

#### **Ecosystem Landing Page**

* **\[DCKA-2258]** To help users who are not subscribed to Ecosystem Tools we have added a landing page inside certs to better understand the benefits of this feature.

#### **Ecosystem Schema Management**

* **\[DCKA-2281]** **Admin Schema Assignment**: Ecosystem admins can now add schemas to their ecosystem with ease, either from the schema table or participant view. This includes the ability to select from existing schemas, mark those already in the ecosystem, and assign them to participants. A "create new schema" option is also now available for greater flexibility.

#### **Improved Ecosystem Participation**

* **\[DCKA-2376] Participant Role Automation**: The process of setting participant roles has been automated based on assigned schemas, removing the need for manual role selection and simplifying the ecosystem management experience
* **\[DCKA-2351] Ecosystem Administrator Visibility:** On the ecosystem view, the participant will now be able to see who is the administrator of the ecosystem.
* **\[DCKA-2299] Ecosystem Admin Participation:** Ability for ecosystem admins to add their organization profiles on relevant ecosystem roles and participate.

## **Enhancements**

#### **User Experience Improvements**

* **\[DCKA-2361] UX Cleanup**: Several user experience improvements have been implemented, including UI consistency enhancements, clearer empty state prompts, and more intuitive navigation elements.

#### **Default Schemas and Templates**

* **\[DCKA-2295] Badge Markings for Defaults**: Default schemas and verification templates are now marked with a badge to distinguish them from user-created items, enhancing clarity and usability .
* **\[DCKA-2245] Ecosystem verification Templates: Verification templates inside an ecosystem are available to all ecosystem verifiers.**

## **Bug Fixes**

* **\[DCKA-2353]** **Ecosystem Creation Labeling**: Updated terminology from "Convener" to "Ecosystem Administrator" across the platform for consistency and clarity.
* **\[DCKA-2362]** **Invitation Process Streamlining**: Fixed an issue where accepting invitations required logging in twice, now allowing users to proceed directly to the invitation acceptance page after login.
* **Ecosystem Schema and Participant Management Fixes**:
  * \[DCKA-2394] 400 error fix when trying to assign schema to a participant
  * \[DCKA-2397] Fix for error on duplicated schema assignment when original was deleted
  * \[DCKA-2399] Fix for job failure error when updating participant information.

