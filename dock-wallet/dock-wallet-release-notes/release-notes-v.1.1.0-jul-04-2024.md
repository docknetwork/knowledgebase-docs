# Release Notes v.1.1.0 Jul 04, 2024

### Story

* **\[DCKM-81]** - Evaluated range proofs presentation before submitting to certs, enhancing the accuracy and security of data shared.
* **\[DCKM-420]** - Improved user notifications for messages queued for decryption in the wallet. Users will now be notified when messages are queued for decryption, improving transparency and user experience during the DIDComm message decryption process.
* **\[DCKM-421]** - Enhanced user visibility for range proofs used in proof requests. Users can now see when a ZKP range proof is used, providing assurance that only necessary information (e.g., "over 18") is shared instead of exact details (e.g., birthdate).

### Bug Fixes

* **\[DCKM-534]** - Fixed the credential request message to specify if multiple credentials are needed. Updated text to correctly indicate that multiple pieces of information might be required.
* **\[DCKM-535]** - Resolved an issue where the "Share Anyway" ecosystem warning required multiple taps to proceed, ensuring a smoother user experience.

### Task

* **\[DCKM-540]** - Upgraded the SDK to version 8.6.0, incorporating the latest features and improvements for enhanced performance and security.
