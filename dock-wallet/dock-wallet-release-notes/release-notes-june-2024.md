# Release Notes June 2024

## v.1.0.2 June 28

### Bug Fixes

* **\[DCKM-508]** - Fixed an issue in the verification flow to validate if the user has selected the required number of credentials before clicking submit, preventing errors when the proof request criteria are not met.
* **\[DCKM-519]** - Resolved a failure in compound proof verification involving range proofs templates.

### Tasks

* **\[DCKM-532]** - Documented improvements and their results for better clarity and reference.
* **\[DCKM-539]** - Added support for the new witness JSON format, enhancing compatibility and functionality.

## v.1.0.1 June 20

### Story

* **\[DCKM-116]** - Improved QR Handling performance by optimizing the process of iterating over handlers, reducing delays caused by the lack of shared state between them.

### Tasks

* **\[DCKM-415]** - Investigated causes of slowness in credential distribution flows, identifying areas for potential optimization.
* **\[DCKM-416]** - Investigated causes of slowness in verification flows.

## v.1.0.0 June 14

### Bugs

* **\[DCKM-517]** - Fixed an issue where the Android wallet version 0.4.28 would not open.

### Tasks

* **\[DCKM-413]** - Implemented measurement of credential distribution timing, including retrieval from the relay service and rendering in the UI.
* **\[DCKM-414]** - Added functionality to measure the performance of verification flows.
* **\[DCKM-415]** - Investigated and identified causes of slowness in credential distribution flows to inform future optimizations.

## v.0.4.28 June 6

### **Overview:**

This version of Dock Mobile Wallet brings several improvements, updates, and new features aimed at enhancing the functionality and usability of the application.

### **Story:**

* **DCKM-67:** Wallet-sdk has been configured to run with Expo, providing users with examples for easier experimentation in the Expo console.
* **DCKM-78:** Implemented cross-platform data storage for wallet-sdk by replacing Realm.js with TypeORM, enabling seamless functionality across different platforms.

### **Task:**

* **DCKM-318:** Updated the relay service API to require acknowledgment for messages fetched in did-batch, ensuring compatibility with old wallets.
* **DCKM-399:** Moved documentation to the knowledge base for better accessibility and searchability. The mobile SDK Readme now directs users to the correct section of the documentation portal.
* **DCKM-456:** Made the react-native repository public and updated the Github repo link in the Open Wallet Foundation repo, ensuring accessibility and transparency.
* **DCKM-474:** Reviewed resources from the Open Wallet Foundation and EUDI, evaluating libraries for features, maturity, test coverage, and potential integration with Dock Wallet.
* **DCKM-491:** Designed the proxy service with a breakdown of routes and assigned story points for initial implementation, as part of creating a wallet services API for common actions efficiency.
