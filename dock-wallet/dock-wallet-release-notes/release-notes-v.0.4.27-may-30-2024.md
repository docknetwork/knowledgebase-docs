# Release Notes v.0.4.27 May 30, 2024

### **Overview:**

This update of Dock Mobile Wallet includes improvements and tasks aimed at enhancing the functionality and reliability of the application.

### **Story:**

* **DCKM-243:** Implemented an update to the credential card UI to display verifier pays issuer (VPI) support. The credential card now fetches the credential status from the wallet-sdk and updates the UI accordingly if VPI is enabled for the credential.

### **Task:**

* **DCKM-293:** Added a Subscan test to detect fee API changes. This integration test ensures that any changes to the Subscan fee API are promptly detected and addressed.
* **DCKM-491:** Designed the proxy service as part of the ongoing effort to create a wallet services API for making common actions more efficient. Issues for this work have been created in the epic DCKM-406, and the breakdown is being done one route at a time, starting with the transaction history route. Story points have been assigned for the first route.
