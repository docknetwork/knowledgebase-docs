# Release Notes v.1.35.0 Jun 12, 2024

### Story

* **\[DCKA-1327]** - Added a "Test mode" option in Settings. Users can now enable Test mode via a toggle, which will display a badge on the top bar and a "Test mode" label on the credential card.
* **\[DCKA-1765]** - Migrated push notification service from Firebase Legacy HTTP Protocol to the more secure and scalable HTTP v1 API, in line with Google's recommendations. This ensures continued functionality post-June 20, 2024, when the legacy APIs are discontinued.
* **\[DCKA-2597]** - Implemented notifications for issuers when issuing "Ecosystem Bound" credentials, clarifying usage restrictions and pricing terms within ecosystems.

### Bug Fixes

* **\[DCKA-2532]** - Updated the label for "polygonid" to "polygonid amoy testnet" for clarity.
* **\[DCKA-2586]** - Groomed Sentry issues for better error tracking and management.
* **\[DCKA-2616]** - Ensured URL validation when inviting participants, preventing invalid URLs from being accepted.
* **\[DCKA-2618]** - Fixed the error message "Can not edit Registry" that appeared incorrectly when saving ecosystem name changes.
* **\[DCKA-2619]** - Validated links for assigning schemas to ecosystem participants, ensuring only valid links are accepted.
* **\[DCKA-2621]** - Investigated and resolved PDF render deploy failures.
* **\[DCKA-2623]** - Addressed "Job failed" errors when assigning paid schemas to ecosystems.
* **\[DCKA-2624]** - Fixed the issue where participants were removed from the first schema when assigned a new one.
* **\[DCKA-2626]** - Corrected the "Invalid Missing participant URL" error displayed during schema selection.
* **\[DCKA-2628]** - Prevented fractional cents from being displayed when adjusting verification fees, ensuring only round numbers are used.
* **\[DCKA-2629]** - Fixed schema delete errors when part of a trust registry.
* **\[DCKA-2632]** - Improved trimming of organization profile display names to avoid exceeding defined lengths.
* **\[DCKA-2635]** - Resolved download failures for billing reports after submitting verification.
* **\[DCKA-2637]** - Fixed issues with updating participant information where logo/info URL fields were unnecessarily required.
* **\[DCKA-2640]** - Addressed issues preventing schema assignment for certain combinations.
* **\[DCKA-2642]** - Ensured newly created verification templates are displayed at the top of the list.

### Task

* **\[DCKA-2412]** - Investigated Stripe Connect integration to determine its feasibility for our needs. A proof of concept was designed, evaluating integration difficulty, supported currencies, user experience, and various other aspects of the payment process.
* **\[DCKA-2488]** - Implemented a paid verification reporting service. Ecosystem administrators can now download a CSV report of verifications for billing purposes.
* **\[DCKA-2490]** - Integrated KVAC during proof presentation verification, ensuring that verifiers pay for credential verification and differentiating between valid, revoked, and fraudulent credentials.
* **\[DCKA-2496]** - Displayed the list price per schema to ecosystem participants.
* **\[DCKA-2510]** - Enabled verifiers to build verification templates using KVAC/locked schemas, showing any associated costs.
* **\[DCKA-2541]** - Auto-generated the OpenAPI YAML file for better API documentation.
* **\[DCKA-2588]** - Included the verifier DID in verification templates with paid credentials.
