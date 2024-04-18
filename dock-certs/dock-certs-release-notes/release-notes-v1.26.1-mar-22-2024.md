# Release Notes v1.26.1 Mar 22nd 2024

## **Overview**

This release addresses specific needs identified by our ecosystem administrators and enhances the overall functionality and usability of Dock Certs.

## **New Features**

#### **Ecosystem Participant Onboarding**

* **\[DCKA-2377]** Administrators can now assign relevant schemas for issuance and verification directly when inviting a new participant to an ecosystem. This streamlines the setup process, enabling participants to contribute immediately after accepting their invitation.

#### **Subscription Management**

* **\[DCKA-2379]** Introduced a "Sync with Stripe" button on the account page to manually synchronize subscription data with Stripe. This feature allows for immediate correction and update of subscription details, ensuring accurate billing and service delivery.

## **Enhancements**

#### **License Compliance**

* **\[DCKA-2358]** Implemented an action in Dock JS repositories to detect GPL/AGPL packages and reject them, reinforcing our commitment to maintaining license compliance across all JavaScript projects.

#### **Verification History Management**

* **\[DCKA-2385]** API calls have been added to allow deletion of individual entries or all history for a specific verification template. This offers more flexibility in managing verification data in compliance with privacy policies and data retention guidelines.

#### **Ecosystem Tools Access for Subscribers**

* **\[DCKA-2445]** Updated the Certs database to ensure that all existing subscribers benefit from the ecosystem tools according to the licensing rules established in the previous release. This ensures all users have appropriate access to these powerful tools.

## **Bug Fixes**

#### **Trial Account Onboarding**

* **\[DCKA-2424]** Fixed an issue where expired trial accounts were incorrectly taken through the new onboarding process, which could not be completed due to the expired status. Now, onboarding will not initiate for expired trials, and any failed issuance during onboarding will redirect users to the dashboard, avoiding any disruption.

#### **UI and Data Display**

* **\[DCKA-2451]** Addressed a UI issue where participant names overlapped field boundaries in the ecosystem section. Improved logic and UX design ensure that participant information is displayed cleanly and legibly.
