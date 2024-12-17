# Release Notes July 2024

## v.1.1.0 July 4

### Story

* **\[DCKM-81]** - Evaluated range proofs presentation before submitting to certs, enhancing the accuracy and security of data shared.
* **\[DCKM-420]** - Improved user notifications for messages queued for decryption in the wallet. Users will now be notified when messages are queued for decryption, improving transparency and user experience during the DIDComm message decryption process.
* **\[DCKM-421]** - Enhanced user visibility for range proofs used in proof requests. Users can now see when a ZKP range proof is used, providing assurance that only necessary information (e.g., "over 18") is shared instead of exact details (e.g., birthdate).

### Bug Fixes

* **\[DCKM-534]** - Fixed the credential request message to specify if multiple credentials are needed. Updated text to correctly indicate that multiple pieces of information might be required.
* **\[DCKM-535]** - Resolved an issue where the "Share Anyway" ecosystem warning required multiple taps to proceed, ensuring a smoother user experience.

### Task

* **\[DCKM-540]** - Upgraded the SDK to version 8.6.0, incorporating the latest features and improvements for enhanced performance and security.

## v.1.1.1 July 18

### Bug fixes

* **\[DCKM-553]** Fixed wallet crashing when trying to do proof request with new credentials.

## v.1.1.2 July 25

#### Bug

* **\[DCKM-483]** Revoked credentials status does not remain as Revoked if the same credential gets unrevoked in Dock Certs.
* **\[DCKM-550]** Fixed the wallet backup creation.

#### Task

* **\[DCKM-541]** Excluded credentials from presentation selection if those credentials do not satisfy the range proof in the verification request.
* **\[DCKM-544]** Added support for Android 14 (API level 34).
* **\[DCKM-558]** Credential status will be refreshed before preparing a proof response, to avoid displaying credentials with the invalid status.
