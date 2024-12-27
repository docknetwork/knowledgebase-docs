# Enabling and Disabling Features

The white label wallet can have a subset of the available features enabled.

To enable or disable a feature update the entries in the features\_config.json file

### Features you can enable or disable

* **Accounts**: The `Tokens` tab allows users to buy, send and receive DOCK tokens. This tab will be hidden if this feature is disabled.
* **Credentials**: The `Credentials` tab will be hidden and no credentials will be able to be imported into the wallet if this feature is disabled.
* **DID Management**: Disabling this feature will mean that the user can not add or delete Decentralized Identifiers (DIDs). The `DIDs` tab is controlled by this feature flag.
* **Credential Verifier**: Allows the user to act as a Verifier and initiate verification flows from their device.
* **Credential URLs**: Detects URLs in credential details. It allows users to click the detected links which are then opened in a browser on the user's device.
