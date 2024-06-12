# Release Notes v.0.4.28 Jun 06, 2024

### **Overview:**

This version of Dock Mobile Wallet brings several improvements, updates, and new features aimed at enhancing the functionality and usability of the application.

### **Story:**

* **DCKM-67:** Wallet-sdk has been configured to run with Expo, providing users with examples for easier experimentation in the Expo console.
* **DCKM-78:** Implemented cross-platform data storage for wallet-sdk by replacing Realm.js with TypeORM, enabling seamless functionality across different platforms.
* **DCKM-222 & DCKM-223:** Added "Login with Dock" support and built deployment pipelines with Github actions for deploying to Chrome and Firefox extension stores, as part of the browser plugin epic (DCKM-221).

### **Task:**

* **DCKM-318:** Updated the relay service API to require acknowledgment for messages fetched in did-batch, ensuring compatibility with old wallets.
* **DCKM-399:** Moved documentation to the knowledge base for better accessibility and searchability. The mobile SDK Readme now directs users to the correct section of the documentation portal.
* **DCKM-456:** Made the react-native repository public and updated the Github repo link in the Open Wallet Foundation repo, ensuring accessibility and transparency.
* **DCKM-474:** Reviewed resources from the Open Wallet Foundation and EUDI, evaluating libraries for features, maturity, test coverage, and potential integration with Dock Wallet.
* **DCKM-491:** Designed the proxy service with a breakdown of routes and assigned story points for initial implementation, as part of creating a wallet services API for common actions efficiency.
