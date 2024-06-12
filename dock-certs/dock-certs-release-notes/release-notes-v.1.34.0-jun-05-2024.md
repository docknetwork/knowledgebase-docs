# Release Notes v.1.34.0 Jun 05, 2024

### **Overview:**

Certs v1.34.0 introduces several enhancements and bug fixes aimed at improving user experience and system functionality.

### **Story:**

* **DCKA-2330:** Implemented the ability to delete user data from Captains Quarters (CQ) without logging into the user account. This feature enables customer success representatives to efficiently manage user data deletion requests while minimizing the potential for errors. Safeguards have been implemented to prevent accidental deletions, and deleted data is marked for irreversible deletion after 48 hours.

### **Bug Fixes:**

* **DCKA-2599:** Addressed issues with the ecosystem invitation API, including resolving errors related to missing participant details and ensuring consistency between the provided name and organization profile. Additionally, improvements were made to the handling of authentication tokens and documentation clarity.
* **DCKA-2601:** Fixed an issue where assigning a schema to a participant would cause the form to become unresponsive, ensuring smooth operation and usability.
* **DCKA-2594:** Resolved problems with the ecosystem invitation API, including errors related to missing participant details and inconsistencies between provided and expected data.

**Task:**

* **DCKA-2441:** Updated technical documentation to explain how revocation works, enhancing understanding and transparency for users and developers.
* **DCKA-2529:** Created a staging relay service to facilitate load testing and ensure system reliability under various conditions.
* **DCKA-2585:** Changed the "Talk to Expert" meeting URL to the latest url for improved accessibility.
* **DCKA-2596:** Enhanced the user interface by hiding back and next buttons and the stepper when only one credential is requested, reducing visual clutter and improving usability.
