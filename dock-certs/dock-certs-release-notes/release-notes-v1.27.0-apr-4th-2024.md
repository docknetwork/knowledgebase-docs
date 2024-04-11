# Release Notes v1.27.0 Apr 4th 2024

## Overview

Dock Certs 1.27.0 introduces significant updates to our pricing plans, enhanced credential management features, and important bug fixes and optimizations. These changes aim to streamline user experience, improve flexibility, and align our offerings with market demands and best practices.

## **New Features**

#### **Pricing Plan Updates 2024**

* **\[DCKA-2374]**: This release brings comprehensive updates to our pricing plans for 2024, reflecting changes in feature availability, trial duration, and subscription terms. Notable adjustments include the inclusion of Anonymous credentials and Encrypted credential backup features in the Free Trial plan, removal of the Starter Plan, and flexibility in seat management for Business and Custom plans.

#### **Anonymous Credentials Expiration**

* **\[DCKA-2467]**: Certs now automatically adds expiration dates to verification templates for anonymous credentials, ensuring consistent enforcement of expiration policies. Users can choose to remove expiration dates for maximum privacy or comply with specific privacy requirements.

## **Enhancements**

#### **Credential Creation Defaults**

* **\[DCKA-2134]**: Default credential creation settings have been optimized to align with best practices, encouraging simplicity and privacy. Key changes include the use of anonymous credentials for enhanced privacy and avoidance of persistent credentials to simplify PII management.

#### **Organization View UX Improvement**

* **\[DCKA-2431]**: The organization profile management has been revamped to improve usability and accommodate additional fields. It is now presented as a drawer instead of a pop-up when editing, providing a more spacious and intuitive interface for managing organization details.

#### **Verifier DID Profile Exposure**

* **\[DCKA-2475]**: Verifier DID profile name and logo are now exposed to proof request messages, enhancing verification processes and providing more context to credential recipients.

## **Bug Fixes and Maintenance**

#### **UI and UX Fixes**

* **\[DCKA-2457]**: Fixed button styling inconsistencies on the settings page, ensuring a symmetrical design and improved visual consistency.
* **\[DCKA-2477]**: Corrected the style of the cancel button and warning icon when declining invitations, ensuring a cohesive and intuitive user experience.

#### **Database Certificate Updates**

* **\[DCKA-2332]**: Updated certificates for RDS instances to comply with AWS requirements, ensuring secure connections and preventing connectivity issues.

## **API and Backend Improvements**

#### **Blockchain Transaction Fee Tracking**

* **\[DCKA-2476]**: Implemented tracking of blockchain transaction fees in the database, facilitating easier monitoring and analysis of transaction costs.

#### **KVAC Credential Issuance**

* **\[DCKA-2491]**: Introduced KVAC (Key Verified Anonymous Credential) issuance and verification capabilities via the API, enabling secure and privacy-preserving credential management.

### **Documentation and Infrastructure**

* **\[DCKA-2416]: Onboarding Form Update**: The job title field is now required in the onboarding form, ensuring completeness and accuracy of user profiles.
