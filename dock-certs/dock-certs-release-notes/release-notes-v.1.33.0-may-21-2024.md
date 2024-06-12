# Release Notes v.1.33.0 May 21, 2024

### **Overview:**

Certs v1.33.0 introduces a series of bug fixes and improvements aimed at enhancing the functionality and stability of the application.

### **Bug Fixes:**

* **DCKA-2288:** Fixed an issue where some fonts were missing on the PDF render server, ensuring accurate rendering of PDF documents.
* **DCKA-2589:** Resolved the "Secret key needs to be provided" error encountered when issuing a BBS+ revocable credential, ensuring smooth credential issuance.
* **DCKA-2590:** Addressed the 'Cannot add new DID key at this time of algorithm: dockbbs' error message received when attempting to create a BBS revocable credential, ensuring successful issuance without errors.
* **DCKA-2591:** Fixed the issue where proof templates were being returned multiple times in the API route, ensuring correct and consistent data retrieval.

### **Task:**

* **DCKA-2092:** Implemented bounds check in the proof presentation to validate the bounds since the cryptography library does not, ensuring data integrity and security.
* **DCKA-2542:** Ensured rejection of unsigned credentials in presentations for proof requests, enhancing security measures.
* **DCKA-2561:** Investigated and set up an autoscaling solution and AWS load balancer for the PDF render server, improving scalability and performance.
