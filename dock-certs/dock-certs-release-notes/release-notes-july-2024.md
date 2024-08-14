# Release Notes July 2024

## v.1.36.0 July 11

### Story

* **\[DCKA-2059]** - Improved the visibility of custom attributes in verification templates. Custom attributes are now instantly visible under the "custom attribute" heading and sorted alphabetically upon selection.

### Tasks

* **\[DCKA-2253]** - Moved onboarding submission logic to the API, allowing Certs session tokens for authorization.
* **\[DCKA-2486]** - Updated UX for setting prices per schema in an ecosystem to align with current VPI design.
* **\[DCKA-2503]** - Applied the ElasticCache update to improve security and performance.
* **\[DCKA-2543]** - Integrated uniresolver status checks in healthcheck AWS.
* **\[DCKA-2583]** - Enhanced PEX validation error messages for better clarity.
* **\[DCKA-2593]** - Updated SSL/TLS certificates for dockusers RDS instance to prevent connectivity failures.
* **\[DCKA-2602]** - Created a wallet API skeleton for Dock Web.
* **\[DCKA-2604]** - Conducted end-to-end testing for the VPI feature in Certs and Wallet.
* **\[DCKA-2634]** - Improved performance for sales demo verification, reducing the average verification time.
* **\[DCKA-2645]** - Added batch-DIDs relay service get messages test.
* **\[DCKA-2652]** - Ensured verification fees are displayed with two decimal points.
* **\[DCKA-2653]** - Added pagination to the participant list table in the ecosystem view.
* **\[DCKA-2656]** - Showed only issuer DIDs belonging to the ecosystem during schema issuance.
* **\[DCKA-2658]** - Enabled default and optional DID selection during verification template creation.
* **\[DCKA-2659]** - Sorted verification templates by date created, displaying the newest first.
* **\[DCKA-2660]** - Changed the "edit" button to "copy" for shared verification templates not owned by the user.
* **\[DCKA-2663]** - Improved the credentials issuance flow feedback.
* **\[DCKA-2664]** - Allowed trial users to accept ecosystem invitations in test mode.
* **\[DCKA-2671]** - Restricted sign-up to valid company emails to improve marketing scoring.
* **\[DCKA-2673]** - Enforced a minimum verification fee for ecosystem-bound credentials.
* **\[DCKA-2674]** - Prevented public schemas from having a verification fee.
* **\[DCKA-2683]** - Renamed columns in the billing report for clarity.
* **\[DCKA-2684]** - Displayed the verifier DID in the verification history.
* **\[DCKA-2686]** - Ensured proper DID selection when generating a verification QR code.
* **\[DCKA-2689]** - Implemented automatic detection of Certs sign-up outages and triggered alerts/support.
* **\[DCKA-2692]** - Applied KVAC logic and reporting for the same issuer/verifier accounts.
* **\[DCKA-2693]** - Enforced a minimum platform fee for ecosystem-bound credential verification to ensure revenue.
* **\[DCKA-2694]** - Added basic ecosystem list and editing functionality to Dock CQ.
* **\[DCKA-2699]** - Switched to Vitest for end-to-end testing to improve test performance and reliability.

### Bug Fixes

* **\[DCKA-2698]** - Fixed an issue where team invitations were not working after sign-up. Invited users can now successfully join the team after completing the sign-up process.
* **\[DCKA-2584]** - Fixed credential status to include statusPurpose properties, ensuring compatibility and proper functioning.
* **\[DCKA-2638]** - Reduced the clickable area when assigning fees to avoid unintended selection.
* **\[DCKA-2644]** - Updated Certs links to developer documentation to point to the new docs portal.
* **\[DCKA-2646]** - Enabled verifiers to change the DID on verification templates, fixing issues with incorrect DID handling.
* **\[DCKA-2650]** - Ensured attributes appear correctly when creating verification templates.
* **\[DCKA-2655]** - Updated empty table text for verification templates in ecosystems, clarifying that participants cannot add templates.
* **\[DCKA-2657]** - Fixed an issue where credentials issued outside an ecosystem incorrectly showed as ecosystem-bound.
* **\[DCKA-2669]** - Addressed issues with the "Open in Wallet" link not working when no wallet is installed on Android devices.
* **\[DCKA-2672]** - Corrected the participant count for ecosystem schemas.
* **\[DCKA-2677]** - Fixed the date order of ecosystem-assigned verification templates.
* **\[DCKA-2678]** - Included KVAC verifications in the ecosystem report to ensure accurate billing.
* **\[DCKA-2680]** - Resolved schema removal issues in verification templates.
* **\[DCKA-2682]** - Enabled ecosystem admins to delete verification templates.
* **\[DCKA-2687]** - Addressed issues with saving verification templates without storing the DID.
* **\[DCKA-2688]** - Fixed onboarding issues for new users in Certs production.
* **\[DCKA-2701]** - Removed additional error notifications when deleting ecosystems.
* **\[DCKA-2703]** - Fixed the duplicate display of DID missing error messages.
* **\[DCKA-2705]** - Resolved errors when issuing VPI credentials with assigned prices.

## v1.37.0 July 24

### Story

* **DCKA-2603** Indicate Last Block for Accumulator Update When Sharing Witness. Credential will indicate last block where accumulator was updated when sharing the witness.

### Bug fixes

**DCKA-2651** Members and administrators of a team that has a paid plan will  be able to see that another team has a paid plan enabled and also how many credentials are left on that plan.

**DCKA-2666** Users can join more than 2 teams.

**DCKA-2721 DCKA-2728** Fixed errors that occurred when verifying a KVAC credential.

**DCKA-2724** Fixed the verification template issues when adding schema specific attributes.

**DCKA-2727** Fixed the credential schema view, that sometimes did not load completely. \


### Task

**DCKA-2252** Created API endpoints to create keys and manage them, allow using a certs session token to access these API routes.

**DCKA-2630** Added cypress tests for onboarding flow

**DCKA-2675** "My Plan: Free trial" shows the expiration date

**DCKA-2696** Stress tested add batch-did relay service&#x20;

**DCKA-2718** Disabled the possibility for new users to sign up using non-work emails

**DCKA-2738** \[Dock API] Fixed race condition when creating credential immediately after creating a DID.

