# Release Notes v.0.4.24 May 10, 2024

### Overview

This release of Dock Mobile - Wallet 0.4.24 focuses on addressing various bugs reported by users, as well as implementing enhancements to improve the functionality and user experience of the mobile wallet application.

### Bug Fixes

#### Android Notifications Missing Icon

* **\[DCKM-201]**: Fixed an issue where Android notifications were missing the app icon in the notification tray. Users reported that notifications did not include the app icon, impacting the visibility and recognition of notifications on Android devices.

#### Transaction History Entries Not Updated

* **\[DCKM-387]**: Addressed an issue where entries for "Sent" and "Received" transactions were not updated in the transaction history. While token reduction and addition were functioning correctly, the counts for sent and received entries remained the same in the transaction history. This issue has been resolved to ensure accurate tracking of transaction history.

#### Wallet Notification Not Received for VC Distribution via DID

* **\[DCKM-426]**: Resolved an issue where wallet notifications were not received when a verifiable credential (VC) was sent via DID distribution. Users did not receive notifications on their phone screens after successful issuance of VCs. This issue has been fixed to ensure that users receive notifications for VC distribution via DID.

### Tasks

#### Supply List of URLs for Connectivity with Polkadotjs

* **\[DCKM-463]**: Completed the task of providing a list of URLs to connect with polkadotjs. This enhancement allows users to have fallback options for connectivity, ensuring seamless interaction with the polkadotjs ecosystem. The [mainnet-node.dock.io](http://mainnet-node.dock.io) and [mainnet-node-2.dock.io](http://mainnet-node-2.dock.io) URLs have been provided for users' convenience.
