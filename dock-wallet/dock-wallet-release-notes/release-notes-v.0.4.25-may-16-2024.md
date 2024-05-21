# Release Notes v.0.4.25 May 16, 2024

### Overview

Dock Mobile - Wallet 0.4.25 introduces several improvements and bug fixes including updates to the wallet-sdk logic for determining if a credential requires verifier pays issuer (VPI) flow, fixes for issues related to credential list updates when switching networks, and improvements in the wallet import process to ensure seamless credential display. Additionally, tasks have been completed to enhance the biometric plugin's user experience and support KVAC (verifier pays issuer) in proof presentations and proof of non-revocation.

### Bug Fixes

#### Credential List Update Issue on Network Switch

* **\[DCKM-475]**: Resolved an issue where the credential list was not updated when switching networks. Users encountered difficulties in viewing updated credential lists after switching networks, impacting the overall usability of the wallet application.

#### Redirection Issue During Wallet Removal Process

* **\[DCKM-485]**: Fixed a bug where users were not redirected to the settings menu screen after selecting the "Skip" action during the wallet removal process. This issue caused confusion and inconsistency in the user interface flow.

#### Credentials Display Issue After Fresh Wallet Import

* **\[DCKM-487]**: Addressed an issue where credentials were not displayed immediately after importing a fresh wallet backup. Users experienced difficulties in viewing imported credentials without additional effort, leading to frustration and inconvenience.

### Tasks

#### Explainer Screen for Default Biometric Plugin

* **\[DCKM-392]**: Implemented an explainer screen for the default biometric plugin, providing users with context before requesting a biometric sample. This enhancement aims to improve user understanding and transparency regarding biometric authentication processes.

#### Support for KVAC in Proof Presentations

* **\[DCKM-429]**: Added support for KVAC (verifier pays issuer) protocol in proof presentations. This task ensures that proof presentations adhere to the KVAC protocol when a credential requires payment by the verifier, enhancing the security and integrity of proof presentations.

#### Support for KVAC in Proof of Non-Revocation

* **\[DCKM-430]**: Implemented support for KVAC protocol in proof of non-revocation. This enhancement ensures that the status validation for proof of non-revocation follows the KVAC protocol when a credential requires payment by the verifier, improving the reliability of non-revocation checks.
