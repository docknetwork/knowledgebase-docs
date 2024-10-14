# Release Notes August 2024

## v1.2.0 August 28

* \[DCKM-579]  Adding the ability to import OID4VC credentials for the wallet holders.
* \[DCKM-583]  Added a loading screen and better feedback for OID4VC issuance flow

## v1.1.3 August 8

* **\[DCKM-418]** Performed refactoring on ShareBBSCredentialScreen
* **\[DCKM-493]** Benchmarked performance of React webview in Flutter
  *

      Performance Review

      * Webview Performance: Flutter demonstrates webview performance comparable to React Native.
      * Data-Intensive Operations: In scenarios involving substantial data processing, Flutter often exhibits superior response times. For example, it handles range proofs presentations more efficiently.

      Security

      * Flutter's webview restricts fetch operations and redirections to external services, offering enhanced security for integrations. While it provides an extra security layer, it could require some updates in some sdk actions in case it requires external fetches (which should be done outside the webview)

      Debugging

      * In Flutter, it is possible to view logs and errors emitted by the webview, a capability that is not available in the React Native app in an easy way. This feature significantly enhances the development experience and provides much better debugging methods.
* **\[DCKM-559]** Mark credentials with status "unknown" if the exact status is not known and added a tooltip with additional information as to the cause and resolution.
