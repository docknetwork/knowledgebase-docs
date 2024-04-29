# Release Notes v1.30.0 Apr 24, 2024

### Overview:

The release 1.30.0 includes improvements related to error message handling within ecosystem along with fixes related to plan upgrade popup and proof requests. Additionally, as part of this release, we have continued on the performance improvement initiative for anonymous credentials issuance.

### **Enhancements**

#### **Clear Error for Verifiers of Locked Credentials**

* **\[DCKA-2493]**: Implemented a feature to provide clear error messages to verifiers attempting to access locked credentials from ecosystems they are not members of. When a verifier outside of the ecosystem attempts to verify a locked credential, they now receive a message stating: "This credential can only be verified by participants in the \[ecosystem name] ecosystem. You can learn about the ecosystem by visiting this website: \[ecosystem website]". This enhancement aims to improve transparency and guidance for verifiers encountering locked credentials.

### **Bug Fixes**

#### **Upgrade Pop-up Issue**

* **\[DCKA-2518]**: Resolved an issue where the upgrade pop-up sometimes appeared when inviting team members, without displaying the close button. Users encountered difficulty closing the pop-up, impacting user experience. With this fix, the upgrade pop-up behaves as expected, ensuring smoother interaction when inviting team members.

#### **Proof Requests Missing ID**

* **\[DCKA-2521]**: Fixed a bug where proof requests did not contain an ID required by the latest PEX library. This issue prevented seamless processing of proof requests, leading to errors and inconsistencies. By addressing this bug, proof requests now include the necessary ID, ensuring compatibility with the latest PEX library.

### **Tasks**

#### **Anonymous Credential Issuance Performance Investigation**

* **\[DCKA-2459]**: Conducted an investigation into the performance of anonymous credential issuance. Test results revealed that issuing an anonymous credential took approximately 3 seconds on average, highlighting potential performance improvements. To address this, debug tracing was enhanced to identify slow points, and further investigation into the efficiency of BBS 2023 compared to BBS+ was initiated. This investigation aims to optimize the performance of anonymous credential issuance for enhanced user experience.

#### **URL Connectivity for PolkadotJS**

* **\[DCKA-2522]**: Provided a list of URLs to connect with PolkadotJS, enabling fallback connectivity. Users can now connect to a private API node and fallback to another URL if the primary connection fails. This enhancement ensures robust connectivity and resilience when interacting with PolkadotJS.
