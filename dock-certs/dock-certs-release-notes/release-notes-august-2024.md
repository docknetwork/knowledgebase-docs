# Release Notes August 2024

## v1.40.0 August 29

### Bug fixes

* **\[DCKA-2807]** Fixed the issue where holders were unable to submit data for requested attributes during credential issuance.

### Tasks

* **\[DCKA-2732]** Added a button to delete a schema from an ecosystem table in the UI.
* **\[DCKA-2788]** Billing report of monetizable verifications include the id of verification template used.

## v1.39.0 August 20

### Bug fixes

* **\[DCKA-2735]** Fixed a logo issue in the ecosystem participants list, when  a schema was assigned to the same DIDs in two different ecosystems.
* **\[DCKA-2796]** Fixed a bug that did not allow users to login with their @gmail accounts.
* **\[DCKA-2797]** Added consistent restrictions to DIDs profile and trust registry profile logos.

### Tasks

**\[DCKA-2771] \[DCKA-2773] \[DCKA-2787] \[DCKA-2794]** Added OID4VCI API routes to authorize and issue credentials; create a credential offer; create a verification template, submit verification proof and presentation.

**\[DCKA-2790]** Submit webhook on proof request received from the holder.

**\[DCKA-2791]** Support JWT-VC verification and fix schema validation.

**\[DCKA-2793]** Support for default JWT paths in the builder in Dock Certs.

## v.1.38.0 August 07

### Story

**\[DCKA-2495]** Added monetizable credential functionality to the bank demo&#x20;

### Bug fixes

* **\[DCKA-2750]** Allowing to add a schema to an ecosystem without assigning any participants to it.&#x20;
* **\[DCKA-2775]** Schema prices will load when editing a verification template.

### Tasks

* **\[DCKA-2761]** Ran tests on OpenID implementation to prepare for updates.
* **\[DCKA-2776]** API issuance of OpenID for VC implementation with existing wallet client .
* **\[DCKA-2352]** Participants  are required to accept an invitation to join an ecosystem, when invited by modifying the on-chain trust registry directly.&#x20;

## &#x20;
