# Release Notes v.1.32.0 May 08, 2024

### Overview

In this release of Dock Applications - Certs v1.32.0, we address several issues reported by users and introduced enhancements to improve the functionality and reliability of the platform. These updates aim to resolve PDF generation and opening issues, improve error handling for node connection failures, and ensure the default usage of BBS2023 for anonymous credentials, among other improvements.

### Bug Fixes

#### PDF Generation and Opening Issues

* **\[DCKA-2537] \[DCKA-2560]**: Fixed an issue where PDFs generated in Certs were not opening properly, as reported by users encountering errors when attempting to open PDF files. Additionally, a similar issue reported by Gravity, where PDF reports were not opening and resulted in a FUNCTION\_INVOCATION\_TIMEOUT error, has been addressed. These issues have been resolved to ensure that PDF files and reports can be generated and opened without any issues.

#### Accumulator Revocation Registries Key Pair Issue

* **\[DCKA-2513]**: Resolved an issue where accumulator revocation registries key pairs were incorrectly tied to a single DID. Now, each accumulator registry has a unique key per registry, ensuring proper functionality and security.

#### Unable to Open Downloaded VC Credentials File

* **\[DCKA-2526]**: Fixed an issue where downloaded VC credentials files could not be opened on staging using the testnet. Users encountered difficulties opening \*.pdf files after extraction. This issue has been resolved to allow seamless opening of downloaded VC credentials files.

### Tasks

#### Improved Error Handling for Node Connection Failures

* **\[DCKA-2523]**: Enhanced error handling for node connection failures to ensure that API alerts are more visible and actionable. Slack alerts now provide clearer indications of errors, and efforts have been made to trigger Zenduty alerts for enhanced monitoring and response to node connection failures.

#### Default Usage of BBS2023 for Anonymous Credentials

* **\[DCKA-2524]**: Updated the default usage of BBS2023 for anonymous credentials. With BBS formally proved in 2023, the platform now defaults to BBS2023 for anonymous credentials, ensuring alignment with industry standards and improved security.

#### Healthcheck PDF Rendering

* **\[DCKA-2544]**: Implemented improvements related to health checks of PDF rendering in the Dock API. This enhancement ensures more reliable rendering of PDF files, contributing to the overall stability and performance of the platform.
