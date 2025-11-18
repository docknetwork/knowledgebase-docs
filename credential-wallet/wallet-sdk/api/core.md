# Wallet SDK Core

## Modules

[biometric-provider](core.md#module_biometric-provider)

Biometric plugin for the Truvera Wallet SDK. This module provides functions for biometric enrollment, matching, and identity verification processes.

[cloud-wallet](core.md#module_cloud-wallet)

Cloud wallet functionality for the Truvera Wallet SDK. This module provides the main cloud wallet creation and management functions.

[credential-provider](core.md#module_credential-provider)

Verifiable credential management functionality for the Truvera Wallet SDK. This module provides functions for importing, verifying, storing, and managing verifiable credentials.

[did-provider](core.md#module_did-provider)

DID (Decentralized Identifier) management functionality for the Truvera Wallet SDK. This module provides functions for creating, importing, exporting, and managing DIDs.

[message-provider](core.md#module_message-provider)

DIDComm message management functionality for the Truvera Wallet SDK. This module provides functions for sending, receiving, and processing DIDComm messages.

[wallet](core.md#module_wallet)

Core wallet functionality for the Dock Wallet SDK. This module provides the main wallet creation and management functions.

## Classes

[DefaultQRCodeProcessor](core.md#DefaultQRCodeProcessor)

Default implementation of QRCodeProcessor

This processor manages a registry of QR code handlers and executes them in priority order to process scanned QR codes. It provides a flexible, extensible system for handling various types of QR codes in a wallet application.

[OID4VCHandler](core.md#OID4VCHandler)

Built-in handler for OID4VC (OpenID for Verifiable Credentials) URIs

This is a generic handler that can be configured with app-specific callbacks for importing credentials. The handler itself only handles protocol detection and delegates the actual import logic to the configured callback.

### Example Usage

```
import { OID4VCHandler } from '@docknetwork/wallet-sdk-core/src/qr-handlers/builtin';
import { getCredentialProvider } from '@docknetwork/wallet-sdk-react-native';
const handler = new OID4VCHandler({
  onImportCredential: async (uri, context) => {
    try {
      // Use SDK to import credential
      await getCredentialProvider().importCredentialFromURI({
        uri,
        didProvider: getDIDProvider(),
        getAuthCode: async (authUrl) => {
          // App-specific auth handling
          return await showAuthWebView(authUrl);
        },
      });
  return { success: true };} catch (error) {  return {    success: false,    error: error instanceof Error ? error : new Error(String(error)),  };}
  },
});
processor.registerHandler(handler);
```

### Handler Priority

Default priority: 5 (very high) This ensures OID4VC URIs are checked before other credential handlers.

## Members

[Goals](core.md#Goals) ⇒[dockDocumentNetworkResolver](core.md#dockDocumentNetworkResolver)

Given an Api URL, resolve the network ID For now it will be applied for creds and certs It can be extended to resolve other external URLs

[OID4VCHandler](core.md#OID4VCHandler) ⇒

Create an OID4VC handler with custom configuration

This is a convenience factory function for creating an OID4VC handler.

[DefaultQRCodeProcessor](core.md#DefaultQRCodeProcessor) ⇒

Create a new QR code processor instance

This is a convenience factory function for creating a processor.

## Constants

[MessageTypes](core.md#MessageTypes)

DIDComm Message helpers Check https://identity.foundation/didcomm-messaging/spec/#out-of-band-messages for more details

## Functions

[buildRequestVerifiablePresentationMessage()](core.md#buildRequestVerifiablePresentationMessage)

Sender: Verifier OOB message to request a verifiable presentation from the holder

[buildAckWalletToWalletVerificationMessage()](core.md#buildAckWalletToWalletVerificationMessage)

Sender: Holder Start a wallet to wallet verification flow

[buildVerifiablePresentationMessage()](core.md#buildVerifiablePresentationMessage)

Sender: Holder Send a verifiable presentation to the verifier

[buildVerifiablePresentationAckMessage()](core.md#buildVerifiablePresentationAckMessage)

Sender: Verifier Sends an the presentation result to the holder

[handleBlockchainNetworkChange()](core.md#handleBlockchainNetworkChange)

Update existing substrate network connection Compare connected substrate connection with the current walle network Disconnect and Establish a new connection if the network is different

## Typedefs

[WalletStatus](core.md#WalletStatus) : `'closed'` | `'loading'` | `'ready'` | `'error'`

Possible wallet status values

[KeypairType](core.md#KeypairType) : `'sr25519'` | `'ed25519'` | `'ecdsa'`

Supported keypair types

[BiometricsProviderConfigs](core.md#BiometricsProviderConfigs) : `Object`

Configuration options for biometric provider operations

## Interfaces

[~~IV1Wallet~~](core.md#IV1Wallet)

Legacy V1 wallet interface for backward compatibility

[IWallet](core.md#IWallet) ⇐ [`IV1Wallet`](core.md#IV1Wallet)

Main wallet interface providing methods for document management, import/export, and network operations.

[IDIDProvider](core.md#IDIDProvider)

Provides a high-level API for DID management operations

[IMessageProvider](core.md#IMessageProvider)

Provides a high-level API for DIDComm message management operations

[ICredentialProvider](core.md#ICredentialProvider)

Provides a high-level API for verifiable credential management operations

[IDVProcessOptions](core.md#IDVProcessOptions)

Callback functions for handling different stages of the identity verification process

[BiometricPlugin](core.md#BiometricPlugin)

Defines the contract for biometric enrollment and matching operations

[IDVProvider](core.md#IDVProvider)

Defines the contract for identity verification operations

[IDVProviderFactory](core.md#IDVProviderFactory)

Creates IDV provider instances with proper event handling and wallet integration

[IBiometricProvider](core.md#IBiometricProvider)

Provides a high-level API for biometric identity verification operations

## biometric-provider

Biometric plugin for the Truvera Wallet SDK. This module provides functions for biometric enrollment, matching, and identity verification processes.

* [biometric-provider](core.md#module_biometric-provider)
  * _static_
    * [.IDV\_EVENTS](core.md#module_biometric-provider.IDV_EVENTS) ⇒ [`IBiometricProvider`](core.md#IBiometricProvider)
  * _inner_
    * [\~setConfigs(configs)](core.md#module_biometric-provider..setConfigs)
    * [\~isBiometricPluginEnabled()](core.md#module_biometric-provider..isBiometricPluginEnabled) ⇒ `boolean`
    * [\~assertConfigs()](core.md#module_biometric-provider..assertConfigs)
    * [\~getBiometricConfigs()](core.md#module_biometric-provider..getBiometricConfigs) ⇒ `BiometricsProviderConfigs.<unknown>`
    * [\~hasProofOfBiometrics(proofRequest)](core.md#module_biometric-provider..hasProofOfBiometrics) ⇒ `boolean`

### biometric-provider.IDV\_EVENTS ⇒ [`IBiometricProvider`](core.md#IBiometricProvider)

Creates a biometric provider instance for identity verification and biometric credential management

**Kind**: static property of [`biometric-provider`](core.md#module_biometric-provider)\
**Returns**: [`IBiometricProvider`](core.md#IBiometricProvider) -

A biometric provider instance with identity verification methods

\
**Throws**:

*   `Error`

    If wallet or idvProviderFactory is not provided

**See**: [IBiometricProvider](core.md#IBiometricProvider) - The interface defining all available biometric provider methods

| Param                     | Type                                               | Description                                       |
| ------------------------- | -------------------------------------------------- | ------------------------------------------------- |
| params                    | `Object`                                           | Provider configuration                            |
| params.wallet             | [`IWallet`](core.md#IWallet)                       | The wallet instance to use for credential storage |
| params.idvProviderFactory | [`IDVProviderFactory`](core.md#IDVProviderFactory) | Factory for creating IDV provider instances       |

**Example**

```js
import { createBiometricProvider } from '@docknetwork/wallet-sdk-core';

const biometricProvider = createBiometricProvider({
  wallet,
  idvProviderFactory: myIDVFactory
});

// Start identity verification process
const result = await biometricProvider.startIDV(proofRequest);
console.log('Enrollment credential:', result.enrollmentCredential);
console.log('Match credential:', result.matchCredential);

// Listen for IDV events
biometricProvider.eventEmitter.on('onComplete', (data) => {
  console.log('IDV process completed:', data);
});
```

### biometric-provider\~setConfigs(configs)

Sets the global biometric provider configurations for the SDK

**Kind**: inner method of [`biometric-provider`](core.md#module_biometric-provider)

| Param                                | Type                                  | Description                                  |
| ------------------------------------ | ------------------------------------- | -------------------------------------------- |
| configs                              | `BiometricsProviderConfigs.<unknown>` | The biometric provider configurations to set |
| configs.enrollmentCredentialType     | `string`                              | The credential type for enrollment           |
| configs.biometricMatchCredentialType | `string`                              | The credential type for biometric matching   |
| \[configs.idvProvider]               | `any`                                 | Optional IDV provider configuration          |

**Example**

```js
import { setConfigs } from '@docknetwork/wallet-sdk-core/biometric-provider';

setConfigs({
  enrollmentCredentialType: 'BiometricEnrollment',
  biometricMatchCredentialType: 'BiometricMatch',
  idvProvider: myIDVProviderConfig
});
```

### biometric-provider\~isBiometricPluginEnabled() ⇒ `boolean`

Checks if the biometric plugin is enabled by verifying if biometric match credential type is configured

**Kind**: inner method of [`biometric-provider`](core.md#module_biometric-provider)\
**Returns**: `boolean` -

True if biometric match credential type is configured, false otherwise

\
**Example**

```js
import { isBiometricPluginEnabled, setConfigs } from '@docknetwork/wallet-sdk-core/biometric-provider';

// Before configuration
console.log(isBiometricPluginEnabled()); // false

// After configuration
setConfigs({
  enrollmentCredentialType: 'BiometricEnrollment',
  biometricMatchCredentialType: 'BiometricMatch'
});
console.log(isBiometricPluginEnabled()); // true
```

### biometric-provider\~assertConfigs()

Asserts that biometric provider configurations are available

**Kind**: inner method of [`biometric-provider`](core.md#module_biometric-provider)\
**Throws**:

*   `Error`

    If biometric provider configs are not set

**Example**

```js
import { assertConfigs } from '@docknetwork/wallet-sdk-core/biometric-provider';

try {
  assertConfigs();
  console.log('Biometric configs are available');
} catch (error) {
  console.error('Biometric configs missing:', error.message);
}
```

### biometric-provider\~getBiometricConfigs() ⇒ `BiometricsProviderConfigs.<unknown>`

Gets the current biometric provider configurations

**Kind**: inner method of [`biometric-provider`](core.md#module_biometric-provider)\
**Returns**: `BiometricsProviderConfigs.<unknown>` -

The current biometric provider configurations

\
**Throws**:

*   `Error`

    If biometric provider configs are not set

**Example**

```js
import { getBiometricConfigs } from '@docknetwork/wallet-sdk-core/biometric-provider';

try {
  const configs = getBiometricConfigs();
  console.log('Enrollment credential type:', configs.enrollmentCredentialType);
  console.log('Match credential type:', configs.biometricMatchCredentialType);
} catch (error) {
  console.error('Failed to get configs:', error.message);
}
```

### biometric-provider\~hasProofOfBiometrics(proofRequest) ⇒ `boolean`

Checks if a proof request requires biometric credentials

**Kind**: inner method of [`biometric-provider`](core.md#module_biometric-provider)\
**Returns**: `boolean` -

True if the proof request requires biometric credentials

| Param        | Type  | Description                  |
| ------------ | ----- | ---------------------------- |
| proofRequest | `any` | The proof request to analyze |

**Example**

```js
import { hasProofOfBiometrics } from '@docknetwork/wallet-sdk-core/biometric-provider';

const proofRequest = {
  input_descriptors: [{
    constraints: {
      fields: [{
        path: ['$.credentialSubject.biometric.id']
      }, {
        path: ['$.credentialSubject.biometric.created']
      }]
    }
  }]
};

if (hasProofOfBiometrics(proofRequest)) {
  console.log('This proof request requires biometric verification');
}
```

## cloud-wallet

Cloud wallet functionality for the Truvera Wallet SDK. This module provides the main cloud wallet creation and management functions.

* [cloud-wallet](core.md#module_cloud-wallet)
  * [\~deriveBiometricKey(biometricData, identifier)](core.md#module_cloud-wallet..deriveBiometricKey) ⇒
  * [\~deriveKeyMappingVaultKeys(biometricData, identifier)](core.md#module_cloud-wallet..deriveKeyMappingVaultKeys) ⇒
  * [\~deriveBiometricEncryptionKey(biometricData, identifier)](core.md#module_cloud-wallet..deriveBiometricEncryptionKey) ⇒
  * [\~encryptMasterKey(masterKey, encryptionKey, iv)](core.md#module_cloud-wallet..encryptMasterKey) ⇒
  * [\~decryptMasterKey(encryptedKey, decryptionKey, iv)](core.md#module_cloud-wallet..decryptMasterKey) ⇒
  * [\~initializeKeyMappingVault(edvUrl, authKey, biometricData, identifier)](core.md#module_cloud-wallet..initializeKeyMappingVault) ⇒
  * [\~enrollUserWithBiometrics(edvUrl, authKey, biometricData, identifier)](core.md#module_cloud-wallet..enrollUserWithBiometrics) ⇒
  * [\~getKeyMappingMasterKey(keyMappingEdv, identifier, decryptionKey, iv)](core.md#module_cloud-wallet..getKeyMappingMasterKey) ⇒
  * [\~authenticateWithBiometrics(edvUrl, authKey, biometricData, identifier)](core.md#module_cloud-wallet..authenticateWithBiometrics) ⇒
  * [\~initializeCloudWalletWithBiometrics(edvUrl, authKey, biometricData, identifier, dataStore)](core.md#module_cloud-wallet..initializeCloudWalletWithBiometrics) ⇒

### cloud-wallet\~deriveBiometricKey(biometricData, identifier) ⇒

Derives a key from biometric data using HKDF

**Kind**: inner method of [`cloud-wallet`](core.md#module_cloud-wallet)\
**Returns**:

Derived key

| Param         | Description                                           |
| ------------- | ----------------------------------------------------- |
| biometricData | Biometric data from provider                          |
| identifier    | User's identifier as salt (email, phone number, etc.) |

### cloud-wallet\~deriveKeyMappingVaultKeys(biometricData, identifier) ⇒

Derives EDV keys from biometric data for the KeyMappingVault

**Kind**: inner method of [`cloud-wallet`](core.md#module_cloud-wallet)\
**Returns**:

Keys for accessing the KeyMappingVault

| Param         | Description                                                         |
| ------------- | ------------------------------------------------------------------- |
| biometricData | Biometric data from the provider                                    |
| identifier    | User's identifier as additional entropy (email, phone number, etc.) |

### cloud-wallet\~deriveBiometricEncryptionKey(biometricData, identifier) ⇒

Generates a key for encrypting/decrypting the master key

**Kind**: inner method of [`cloud-wallet`](core.md#module_cloud-wallet)\
**Returns**:

Encryption key and IV for AES encryption

| Param         | Description                                           |
| ------------- | ----------------------------------------------------- |
| biometricData | Biometric data from provider                          |
| identifier    | User's identifier as salt (email, phone number, etc.) |

### cloud-wallet\~encryptMasterKey(masterKey, encryptionKey, iv) ⇒

Encrypts the master key using a key derived from biometric data

**Kind**: inner method of [`cloud-wallet`](core.md#module_cloud-wallet)\
**Returns**:

Encrypted master key

| Param         | Description                                |
| ------------- | ------------------------------------------ |
| masterKey     | The CloudWalletVault master key to encrypt |
| encryptionKey | Key derived from biometric data            |
| iv            | Initialization vector                      |

### cloud-wallet\~decryptMasterKey(encryptedKey, decryptionKey, iv) ⇒

Decrypts the master key using biometric-derived key

**Kind**: inner method of [`cloud-wallet`](core.md#module_cloud-wallet)\
**Returns**:

The decrypted master key

| Param         | Description                     |
| ------------- | ------------------------------- |
| encryptedKey  | The encrypted master key        |
| decryptionKey | Key derived from biometric data |
| iv            | Initialization vector           |

### cloud-wallet\~initializeKeyMappingVault(edvUrl, authKey, biometricData, identifier) ⇒

Initializes the KeyMappingVault using biometric data

**Kind**: inner method of [`cloud-wallet`](core.md#module_cloud-wallet)\
**Returns**:

Initialized EDV service

| Param         | Description                                   |
| ------------- | --------------------------------------------- |
| edvUrl        | URL for the edv                               |
| authKey       | Auth key for the edv                          |
| biometricData | User's biometric data                         |
| identifier    | User's identifier (email, phone number, etc.) |

### cloud-wallet\~enrollUserWithBiometrics(edvUrl, authKey, biometricData, identifier) ⇒

Enrolls a user by creating necessary vaults and keys

**Kind**: inner method of [`cloud-wallet`](core.md#module_cloud-wallet)\
**Returns**:

The master key and mnemonic for backup

| Param         | Description                                   |
| ------------- | --------------------------------------------- |
| edvUrl        | URL for the edv                               |
| authKey       | Auth key for the edv                          |
| biometricData | Biometric data from provider                  |
| identifier    | User's identifier (email, phone number, etc.) |

### cloud-wallet\~getKeyMappingMasterKey(keyMappingEdv, identifier, decryptionKey, iv) ⇒

Gets the master key from the key mapping vault using provided decryption keys

**Kind**: inner method of [`cloud-wallet`](core.md#module_cloud-wallet)\
**Returns**:

The decrypted master key for CloudWalletVault

| Param         | Description                                   |
| ------------- | --------------------------------------------- |
| keyMappingEdv | Initialized key mapping vault service         |
| identifier    | User's identifier (email, phone number, etc.) |
| decryptionKey | Key for decrypting the master key             |
| iv            | Initialization vector for decryption          |

### cloud-wallet\~authenticateWithBiometrics(edvUrl, authKey, biometricData, identifier) ⇒

Authenticates a user with biometric data and identifier

**Kind**: inner method of [`cloud-wallet`](core.md#module_cloud-wallet)\
**Returns**:

The decrypted master key for CloudWalletVault

| Param         | Description                                   |
| ------------- | --------------------------------------------- |
| edvUrl        | URL for the edv                               |
| authKey       | Auth key for the edv                          |
| biometricData | Biometric data from the provider              |
| identifier    | User's identifier (email, phone number, etc.) |

### cloud-wallet\~initializeCloudWalletWithBiometrics(edvUrl, authKey, biometricData, identifier, dataStore) ⇒

Initializes the Cloud Wallet using biometric authentication

**Kind**: inner method of [`cloud-wallet`](core.md#module_cloud-wallet)\
**Returns**:

Initialized cloud wallet

| Param         | Description                                   |
| ------------- | --------------------------------------------- |
| edvUrl        | Cloud wallet vault URL                        |
| authKey       | Cloud wallet auth key                         |
| biometricData | User's biometric data                         |
| identifier    | User's identifier (email, phone number, etc.) |
| dataStore     | Optional data store for the wallet            |

## credential-provider

Verifiable credential management functionality for the Truvera Wallet SDK. This module provides functions for importing, verifying, storing, and managing verifiable credentials.

* [credential-provider](core.md#module_credential-provider)
  * [\~isValid(credential)](core.md#module_credential-provider..isValid) ⇒ `Promise.<Object>`
  * [\~createCredentialProvider(params)](core.md#module_credential-provider..createCredentialProvider) ⇒ [`ICredentialProvider`](core.md#ICredentialProvider)

### credential-provider\~isValid(credential) ⇒ `Promise.<Object>`

Uses Dock SDK to verify a credential

**Kind**: inner method of [`credential-provider`](core.md#module_credential-provider)\
**Returns**: `Promise.<Object>` -

Verification result with status and optional error/warning messages

| Param      |
| ---------- |
| credential |

### credential-provider\~createCredentialProvider(params) ⇒ [`ICredentialProvider`](core.md#ICredentialProvider)

Creates a credential provider instance bound to a wallet

**Kind**: inner method of [`credential-provider`](core.md#module_credential-provider)\
**Returns**: [`ICredentialProvider`](core.md#ICredentialProvider) -

A credential provider instance with all verifiable credential management methods

\
**See**: [ICredentialProvider](core.md#ICredentialProvider) - The interface defining all available credential provider methods

| Param         | Type                         | Description                                       |
| ------------- | ---------------------------- | ------------------------------------------------- |
| params        | `Object`                     | Provider configuration                            |
| params.wallet | [`IWallet`](core.md#IWallet) | The wallet instance to use for credential storage |

**Example**

```js
import { createCredentialProvider } from '@docknetwork/wallet-sdk-core';

const credentialProvider = createCredentialProvider({wallet});

// Add a credential
const addedCredential = await credentialProvider.addCredential(myCredential);

// Validate a credential
const result = await credentialProvider.isValid(credential);
if (result.status === 'verified') {
  console.log('Credential is valid');
}

// Get all credentials
const allCredentials = credentialProvider.getCredentials();

// Import from URI
await credentialProvider.importCredentialFromURI({
  uri: 'https://example.com/credential-offer',
  didProvider
});
```

## did-provider

DID (Decentralized Identifier) management functionality for the Truvera Wallet SDK. This module provides functions for creating, importing, exporting, and managing DIDs.

### did-provider\~createDIDProvider(params) ⇒ [`IDIDProvider`](core.md#IDIDProvider)

Creates a DID provider instance bound to a wallet

**Kind**: inner method of [`did-provider`](core.md#module_did-provider)\
**Returns**: [`IDIDProvider`](core.md#IDIDProvider) -

A DID provider instance with all DID management methods

\
**See**: [IDIDProvider](core.md#IDIDProvider) - The interface defining all available DID provider methods

| Param         | Type                         | Description                                 |
| ------------- | ---------------------------- | ------------------------------------------- |
| params        | `Object`                     | Provider configuration                      |
| params.wallet | [`IWallet`](core.md#IWallet) | The wallet instance to bind the provider to |

**Example**

```js
import { createDIDProvider } from '@docknetwork/wallet-sdk-core';

const didProvider = createDIDProvider({wallet});

// Create a new DID
const {keyDoc, didDocumentResolution} = await didProvider.createDIDKey({
  name: 'My DID'
});

// Get all DIDs
const allDIDs = await didProvider.getAll();

// Export a DID
const exportedDID = await didProvider.exportDID({
  id: didDocumentResolution.id,
  password: 'mypassword'
});
```

## message-provider

DIDComm message management functionality for the Truvera Wallet SDK. This module provides functions for sending, receiving, and processing DIDComm messages.

### message-provider\~createMessageProvider(params) ⇒ [`IMessageProvider`](core.md#IMessageProvider)

Creates a message provider instance bound to a wallet and DID provider

**Kind**: inner method of [`message-provider`](core.md#module_message-provider)\
**Returns**: [`IMessageProvider`](core.md#IMessageProvider) -

A message provider instance with all DIDComm message management methods

\
**See**: [IMessageProvider](core.md#IMessageProvider) - The interface defining all available message provider methods

| Param                  | Type                                   | Description                                                          |
| ---------------------- | -------------------------------------- | -------------------------------------------------------------------- |
| params                 | `Object`                               | Provider configuration                                               |
| params.wallet          | [`IWallet`](core.md#IWallet)           | The wallet instance to use for message storage                       |
| params.didProvider     | [`IDIDProvider`](core.md#IDIDProvider) | The DID provider instance to use for key management                  |
| \[params.relayService] | `any`                                  | Optional relay service implementation (defaults to built-in service) |

**Example**

```js
import { createMessageProvider } from '@docknetwork/wallet-sdk-core';

const messageProvider = createMessageProvider({
  wallet,
  didProvider
});

// Send a message
await messageProvider.sendMessage({
  did: 'did:key:sender123',
  recipientDid: 'did:key:recipient456',
  message: { hello: 'world' }
});

// Start auto-fetching messages
const stopAutoFetch = messageProvider.startAutoFetch(5000);

// Add message listener
const removeListener = messageProvider.addMessageListener((message) => {
  console.log('Received message:', message);
});
```

## wallet

Core wallet functionality for the Dock Wallet SDK. This module provides the main wallet creation and management functions.

### wallet\~createWallet(props) ⇒ [`Promise.<IWallet>`](core.md#IWallet)

Creates a new wallet instance with the provided data store. The wallet provides secure storage and management of DIDs, credentials, keys, and other documents.

**Kind**: inner method of [`wallet`](core.md#module_wallet)\
**Returns**: [`Promise.<IWallet>`](core.md#IWallet) -

A promise that resolves to the created wallet instance

\
**Throws**:

*   `Error`

    If the data store is not properly initialized

**See**: [IWallet](core.md#IWallet) - The interface defining all available wallet methods

| Param           | Type                | Description                                          |
| --------------- | ------------------- | ---------------------------------------------------- |
| props           | `CreateWalletProps` | Configuration options for wallet creation            |
| props.dataStore | `DataStore`         | The data store implementation to use for persistence |

**Example**

```js
import { createWallet } from '@docknetwork/wallet-sdk-core';
import { createDataStore } from '@docknetwork/wallet-sdk-data-store';

const dataStore = await createDataStore();
const wallet = await createWallet({ dataStore });

// The wallet implements the IWallet interface
await wallet.addDocument(myCredential);
const documents = await wallet.getAllDocuments();
```

## ~~IV1Wallet~~

_**This interface is obsolete and should not be used for new implementations. Use IWallet instead.**_

Legacy V1 wallet interface for backward compatibility

**Kind**: global interface\


## IWallet ⇐ [`IV1Wallet`](core.md#IV1Wallet)

Main wallet interface providing methods for document management, import/export, and network operations.

**Kind**: global interface\
**Extends**: [`IV1Wallet`](core.md#IV1Wallet)

* [IWallet](core.md#IWallet) ⇐ [`IV1Wallet`](core.md#IV1Wallet)
  * [.deleteWallet()](core.md#IWallet.deleteWallet) ⇒ `Promise.<void>`
  * [.setStatus(newStatus)](core.md#IWallet.setStatus)
  * [.setNetwork(networkId)](core.md#IWallet.setNetwork) ⇒ `Promise.<void>`
  * [.getNetworkId()](core.md#IWallet.getNetworkId) ⇒ `string`
  * [.getDocumentById(id)](core.md#IWallet.getDocumentById) ⇒ `Promise.<WalletDocument>`
  * [.getAllDocuments()](core.md#IWallet.getAllDocuments) ⇒ `Promise.<Array.<WalletDocument>>`
  * [.getDocumentsById(idList)](core.md#IWallet.getDocumentsById) ⇒ `Promise.<Array.<WalletDocument>>`
  * [.getDocumentsByType(type)](core.md#IWallet.getDocumentsByType) ⇒ `Promise.<Array.<WalletDocument>>`
  * [.addDocument(json, \[options\])](core.md#IWallet.addDocument) ⇒ `Promise.<WalletDocument>`
  * [.updateDocument(document, \[options\])](core.md#IWallet.updateDocument) ⇒ `Promise.<WalletDocument>`
  * [.removeDocument(id, \[options\])](core.md#IWallet.removeDocument) ⇒ `Promise.<void>`
  * [.getDocumentCorrelations(documentId)](core.md#IWallet.getDocumentCorrelations) ⇒ `Promise.<Array.<WalletDocument>>`
  * [.getAccountKeyPair(accountId)](core.md#IWallet.getAccountKeyPair) ⇒ `Promise.<any>`
  * [.getDocumentsFromEncryptedWallet(json, password)](core.md#IWallet.getDocumentsFromEncryptedWallet) ⇒ `Promise.<any>`
  * [.importUniversalWalletJSON(json, password)](core.md#IWallet.importUniversalWalletJSON) ⇒ `Promise.<void>`
  * [.exportDocuments(params)](core.md#IWallet.exportDocuments) ⇒ `Promise.<any>`
  * [.exportUniversalWalletJSON(password)](core.md#IWallet.exportUniversalWalletJSON) ⇒ `any`

### IWallet.deleteWallet() ⇒ `Promise.<void>`

Deletes the entire wallet and all its documents

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Emits**: `WalletEvents.event:walletDeleted`\


### IWallet.setStatus(newStatus)

Sets the wallet status

**Kind**: static method of [`IWallet`](core.md#IWallet)

| Param     | Type     | Description           |
| --------- | -------- | --------------------- |
| newStatus | `string` | The new status to set |

### IWallet.setNetwork(networkId) ⇒ `Promise.<void>`

Sets the active network for the wallet

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Emits**: `WalletEvents.event:networkUpdated`

| Param     | Type     | Description                         |
| --------- | -------- | ----------------------------------- |
| networkId | `string` | The network identifier to switch to |

### IWallet.getNetworkId() ⇒ `string`

Gets the current network ID

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `string` -

The current network identifier

\


### IWallet.getDocumentById(id) ⇒ `Promise.<WalletDocument>`

Retrieves a document by its ID

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `Promise.<WalletDocument>` -

The document with the specified ID

\
**Throws**:

*   `Error`

    If document is not found

| Param | Type     | Description                           |
| ----- | -------- | ------------------------------------- |
| id    | `string` | The unique identifier of the document |

### IWallet.getAllDocuments() ⇒ `Promise.<Array.<WalletDocument>>`

Retrieves all documents stored in the wallet

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `Promise.<Array.<WalletDocument>>` -

Array of all documents in the wallet

\


### IWallet.getDocumentsById(idList) ⇒ `Promise.<Array.<WalletDocument>>`

Retrieves multiple documents by their IDs

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `Promise.<Array.<WalletDocument>>` -

Array of documents matching the provided IDs

| Param  | Type             | Description                       |
| ------ | ---------------- | --------------------------------- |
| idList | `Array.<string>` | Array of document IDs to retrieve |

### IWallet.getDocumentsByType(type) ⇒ `Promise.<Array.<WalletDocument>>`

Retrieves all documents of a specific type

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `Promise.<Array.<WalletDocument>>` -

Array of documents matching the specified type

| Param | Type     | Description                                                                  |
| ----- | -------- | ---------------------------------------------------------------------------- |
| type  | `string` | The document type to filter by (e.g., 'VerifiableCredential', 'DIDDocument') |

### IWallet.addDocument(json, \[options]) ⇒ `Promise.<WalletDocument>`

Adds a new document to the wallet

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `Promise.<WalletDocument>` -

The created document with generated metadata

\
**Emits**: `WalletEvents.event:documentAdded`

| Param      | Type  | Description                                             |
| ---------- | ----- | ------------------------------------------------------- |
| json       | `any` | The document to add (must have valid JSON-LD structure) |
| \[options] | `any` | Optional parameters for document creation               |

**Example**

```js
const credential = {
  "@context": ["https://www.w3.org/2018/credentials/v1"],
  "type": ["VerifiableCredential"],
  "issuer": "did:dock:123",
  "credentialSubject": { "name": "John Doe" }
};
const addedDoc = await wallet.addDocument(credential);
```

### IWallet.updateDocument(document, \[options]) ⇒ `Promise.<WalletDocument>`

Updates an existing document

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `Promise.<WalletDocument>` -

The updated document

\
**Throws**:

*   `Error`

    If document doesn't exist

**Emits**: `WalletEvents.event:documentUpdated`

| Param      | Type  | Description                                      |
| ---------- | ----- | ------------------------------------------------ |
| document   | `any` | The document with updated data (must include ID) |
| \[options] | `any` | Optional parameters for document update          |

### IWallet.removeDocument(id, \[options]) ⇒ `Promise.<void>`

Removes a document from the wallet

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Throws**:

*   `Error`

    If document is not found

**Emits**: `WalletEvents.event:documentRemoved`

| Param      | Type     | Description                              |
| ---------- | -------- | ---------------------------------------- |
| id         | `string` | The ID of the document to remove         |
| \[options] | `any`    | Optional parameters for document removal |

### IWallet.getDocumentCorrelations(documentId) ⇒ `Promise.<Array.<WalletDocument>>`

Gets all documents correlated to a specific document

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `Promise.<Array.<WalletDocument>>` -

Array of correlated documents

| Param      | Type     | Description                                     |
| ---------- | -------- | ----------------------------------------------- |
| documentId | `string` | The ID of the document to find correlations for |

### IWallet.getAccountKeyPair(accountId) ⇒ `Promise.<any>`

Retrieves the keypair associated with an account

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `Promise.<any>` -

The keypair associated with the account

| Param     | Type     | Description                           |
| --------- | -------- | ------------------------------------- |
| accountId | `string` | The account ID to get the keypair for |

### IWallet.getDocumentsFromEncryptedWallet(json, password) ⇒ `Promise.<any>`

Decrypts and retrieves documents from an encrypted wallet without importing

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `Promise.<any>` -

Array of decrypted documents

| Param    | Type     | Description                    |
| -------- | -------- | ------------------------------ |
| json     | `any`    | The encrypted wallet JSON      |
| password | `string` | Password to decrypt the wallet |

### IWallet.importUniversalWalletJSON(json, password) ⇒ `Promise.<void>`

Imports documents from an encrypted Universal Wallet 2020 JSON

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**See**: [https://w3c-ccg.github.io/universal-wallet-interop-spec/](https://w3c-ccg.github.io/universal-wallet-interop-spec/)

| Param    | Type     | Description                    |
| -------- | -------- | ------------------------------ |
| json     | `any`    | The encrypted wallet JSON      |
| password | `string` | Password to decrypt the wallet |

**Example**

```js
// Import from encrypted wallet backup
const walletBackup = { ... }; // encrypted wallet JSON
await wallet.importUniversalWalletJSON(walletBackup, 'mypassword');
```

### IWallet.exportDocuments(params) ⇒ `Promise.<any>`

Exports specified documents as an encrypted JSON (test)

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `Promise.<any>` -

Encrypted wallet JSON

| Param            | Type          | Description             |
| ---------------- | ------------- | ----------------------- |
| params           | `Object`      | Export parameters       |
| params.documents | `Array.<any>` | Documents to export     |
| params.password  | `string`      | Password for encryption |

### IWallet.exportUniversalWalletJSON(password) ⇒ `any`

Exports the entire wallet as an encrypted Universal Wallet 2020 JSON

**Kind**: static method of [`IWallet`](core.md#IWallet)\
**Returns**: `any` -

Encrypted Universal Wallet JSON representation

\
**See**: [https://w3c-ccg.github.io/universal-wallet-interop-spec/](https://w3c-ccg.github.io/universal-wallet-interop-spec/)

| Param    | Type     | Description             |
| -------- | -------- | ----------------------- |
| password | `string` | Password for encryption |

**Example**

```js
// Create encrypted backup of entire wallet
const backup = await wallet.exportUniversalWalletJSON('mypassword');
// Save backup to file or cloud storage
```

## IDIDProvider

Provides a high-level API for DID management operations

**Kind**: global interface

* [IDIDProvider](core.md#IDIDProvider)
  * [.importDID(params)](core.md#IDIDProvider.importDID) ⇒ `Promise.<Array.<any>>`
  * [.createDIDKey(params)](core.md#IDIDProvider.createDIDKey) ⇒ `Promise.<{keyDoc: any, didDocumentResolution: any}>`
  * [.editDID(params)](core.md#IDIDProvider.editDID) ⇒ `Promise.<void>`
  * [.deleteDID(params)](core.md#IDIDProvider.deleteDID) ⇒ `Promise.<void>`
  * [.exportDID(params)](core.md#IDIDProvider.exportDID) ⇒ `Promise.<any>`
  * [.getAll()](core.md#IDIDProvider.getAll) ⇒ `Promise.<Array.<any>>`
  * [.getDIDKeyPairs()](core.md#IDIDProvider.getDIDKeyPairs) ⇒ `Promise.<Array.<any>>`
  * [.ensureDID()](core.md#IDIDProvider.ensureDID) ⇒ `Promise.<({keyDoc: any, didDocumentResolution: any}|void)>`
  * [.getDefaultDID()](core.md#IDIDProvider.getDefaultDID) ⇒ `Promise.<(string|undefined)>`

### IDIDProvider.importDID(params) ⇒ `Promise.<Array.<any>>`

Imports a DID from an encrypted wallet JSON

**Kind**: static method of [`IDIDProvider`](core.md#IDIDProvider)\
**Returns**: `Promise.<Array.<any>>` -

Array of imported documents

\
**Throws**:

*   `Error`

    If password is incorrect or DID already exists in wallet

| Param                      | Type     | Description                                  |
| -------------------------- | -------- | -------------------------------------------- |
| params                     | `Object` | Import parameters                            |
| params.encryptedJSONWallet | `any`    | The encrypted wallet JSON containing the DID |
| params.password            | `string` | Password to decrypt the wallet               |

**Example**

```js
const importedDocs = await didProvider.importDID({
  encryptedJSONWallet: encryptedBackup,
  password: 'mypassword'
});
```

### IDIDProvider.createDIDKey(params) ⇒ `Promise.<{keyDoc: any, didDocumentResolution: any}>`

Creates a new DID:key with an associated keypair

**Kind**: static method of [`IDIDProvider`](core.md#IDIDProvider)\
**Returns**: `Promise.<{keyDoc: any, didDocumentResolution: any}>` -

The created keypair and DID document

\
**Throws**:

*   `Error`

    If name is not provided

| Param                | Type     | Description                              |
| -------------------- | -------- | ---------------------------------------- |
| params               | `Object` | Creation parameters                      |
| params.name          | `string` | The name for the new DID                 |
| \[params.derivePath] | `string` | Optional derivation path for the keypair |
| \[params.type]       | `string` | Optional key type specification          |

**Example**

```js
const {keyDoc, didDocumentResolution} = await didProvider.createDIDKey({
  name: 'My Identity DID',
  derivePath: "m/44'/60'/0'/0/0"
});
```

### IDIDProvider.editDID(params) ⇒ `Promise.<void>`

Edits a DID document's name

**Kind**: static method of [`IDIDProvider`](core.md#IDIDProvider)\
**Throws**:

*   `Error`

    If document ID is not set or document not found

| Param       | Type     | Description                        |
| ----------- | -------- | ---------------------------------- |
| params      | `Object` | Edit parameters                    |
| params.id   | `string` | The ID of the DID document to edit |
| params.name | `string` | The new name for the DID           |

**Example**

```js
await didProvider.editDID({
  id: 'did:key:z6MkhaXgBZDvotDkL5257faiztiGiC2QtKLGpbnnEGta2doK',
  name: 'Updated DID Name'
});
```

### IDIDProvider.deleteDID(params) ⇒ `Promise.<void>`

Deletes a DID from the wallet

**Kind**: static method of [`IDIDProvider`](core.md#IDIDProvider)\
**Throws**:

*   `Error`

    If document ID is not set

| Param     | Type     | Description                          |
| --------- | -------- | ------------------------------------ |
| params    | `Object` | Delete parameters                    |
| params.id | `string` | The ID of the DID document to delete |

**Example**

```js
await didProvider.deleteDID({
  id: 'did:key:z6MkhaXgBZDvotDkL5257faiztiGiC2QtKLGpbnnEGta2doK'
});
```

### IDIDProvider.exportDID(params) ⇒ `Promise.<any>`

Exports a DID and its correlated documents as an encrypted JSON

**Kind**: static method of [`IDIDProvider`](core.md#IDIDProvider)\
**Returns**: `Promise.<any>` -

Encrypted wallet JSON containing the DID and correlations

\
**Throws**:

*   `Error`

    If DID document or keypair not found

| Param           | Type     | Description                          |
| --------------- | -------- | ------------------------------------ |
| params          | `Object` | Export parameters                    |
| params.id       | `string` | The ID of the DID document to export |
| params.password | `string` | Password for encryption              |

**Example**

```js
const exportedDID = await didProvider.exportDID({
  id: 'did:key:z6MkhaXgBZDvotDkL5257faiztiGiC2QtKLGpbnnEGta2doK',
  password: 'mypassword'
});
```

### IDIDProvider.getAll() ⇒ `Promise.<Array.<any>>`

Retrieves all DIDs stored in the wallet

**Kind**: static method of [`IDIDProvider`](core.md#IDIDProvider)\
**Returns**: `Promise.<Array.<any>>` -

Array of DID resolution response documents

\
**Example**

```js
const allDIDs = await didProvider.getAll();
console.log(`Found ${allDIDs.length} DIDs in wallet`);
```

### IDIDProvider.getDIDKeyPairs() ⇒ `Promise.<Array.<any>>`

Retrieves all keypairs associated with DIDs in the wallet

**Kind**: static method of [`IDIDProvider`](core.md#IDIDProvider)\
**Returns**: `Promise.<Array.<any>>` -

Array of keypair documents

\
**Example**

```js
const keyPairs = await didProvider.getDIDKeyPairs();
console.log(`Found ${keyPairs.length} DID keypairs`);
```

### IDIDProvider.ensureDID() ⇒ `Promise.<({keyDoc: any, didDocumentResolution: any}|void)>`

Ensures at least one DID exists in the wallet, creating a default if none exist

**Kind**: static method of [`IDIDProvider`](core.md#IDIDProvider)\
**Returns**: `Promise.<({keyDoc: any, didDocumentResolution: any}|void)>` -

The created DID if one was created, undefined otherwise

\
**Example**

```js
// Ensure wallet has at least one DID
await didProvider.ensureDID();
```

### IDIDProvider.getDefaultDID() ⇒ `Promise.<(string|undefined)>`

Gets the default DID from the wallet (first DID if exists)

**Kind**: static method of [`IDIDProvider`](core.md#IDIDProvider)\
**Returns**: `Promise.<(string|undefined)>` -

The default DID identifier or undefined if no DIDs exist

\
**Example**

```js
const defaultDID = await didProvider.getDefaultDID();
if (defaultDID) {
  console.log(`Default DID: ${defaultDID}`);
}
```

## IMessageProvider

Provides a high-level API for DIDComm message management operations

**Kind**: global interface

* [IMessageProvider](core.md#IMessageProvider)
  * [.fetchMessages](core.md#IMessageProvider.fetchMessages) ⇒ `Promise.<void>`
  * [.addMessageListener](core.md#IMessageProvider.addMessageListener) ⇒ `function`
  * [.processDIDCommMessages](core.md#IMessageProvider.processDIDCommMessages) ⇒ `Promise.<void>`
  * [.processMessageRecurrentJob](core.md#IMessageProvider.processMessageRecurrentJob) ⇒ `Promise.<void>`
  * [.markMessageAsRead](core.md#IMessageProvider.markMessageAsRead) ⇒ `Promise.<void>`
  * [.sendMessage(params)](core.md#IMessageProvider.sendMessage) ⇒ `Promise.<any>`
  * [.waitForMessage()](core.md#IMessageProvider.waitForMessage) ⇒ `Promise.<any>`
  * [.startAutoFetch(\[timeout\])](core.md#IMessageProvider.startAutoFetch) ⇒ `function`
  * [.clearCache()](core.md#IMessageProvider.clearCache) ⇒ `Promise.<void>`

### IMessageProvider.fetchMessages ⇒ `Promise.<void>`

Fetches new messages from the relay service

**Kind**: static property of [`IMessageProvider`](core.md#IMessageProvider)\
**Throws**:

*   `Error`

    If message fetching fails

**Example**

```js
await messageProvider.fetchMessages();
console.log('Messages fetched successfully');
```

### IMessageProvider.addMessageListener ⇒ `function`

Adds a listener for when messages are decrypted

**Kind**: static property of [`IMessageProvider`](core.md#IMessageProvider)\
**Returns**: `function` -

Function to remove the listener

| Param   | Type       | Description                                    |
| ------- | ---------- | ---------------------------------------------- |
| handler | `function` | Callback function to handle decrypted messages |

**Example**

```js
const removeListener = messageProvider.addMessageListener((message) => {
  console.log('New message received:', message);
});
// Later, remove the listener
removeListener();
```

### IMessageProvider.processDIDCommMessages ⇒ `Promise.<void>`

Processes stored DIDComm messages and decrypts them

**Kind**: static property of [`IMessageProvider`](core.md#IMessageProvider)\
**Throws**:

*   `Error`

    If message processing fails

**Example**

```js
await messageProvider.processDIDCommMessages();
console.log('Messages processed successfully');
```

### IMessageProvider.processMessageRecurrentJob ⇒ `Promise.<void>`

Starts the recurrent message processing job

**Kind**: static property of [`IMessageProvider`](core.md#IMessageProvider)\
**Example**

```js
await messageProvider.processMessageRecurrentJob();
```

### IMessageProvider.markMessageAsRead ⇒ `Promise.<void>`

Marks a message as read and removes it from storage

**Kind**: static property of [`IMessageProvider`](core.md#IMessageProvider)\
**Throws**:

*   `Error`

    If message is not found or not a DIDComm message

| Param     | Type     | Description                           |
| --------- | -------- | ------------------------------------- |
| messageId | `string` | The ID of the message to mark as read |

**Example**

```js
await messageProvider.markMessageAsRead('message-id-123');
console.log('Message marked as read');
```

### IMessageProvider.sendMessage(params) ⇒ `Promise.<any>`

Sends a DIDComm message to a recipient

**Kind**: static method of [`IMessageProvider`](core.md#IMessageProvider)\
**Returns**: `Promise.<any>` -

Result of sending the message

\
**Throws**:

*   `Error`

    If sender DID not found or message sending fails

| Param                  | Type     | Description                                                 |
| ---------------------- | -------- | ----------------------------------------------------------- |
| params                 | `Object` | Message parameters                                          |
| \[params.from]         | `string` | Sender DID identifier                                       |
| \[params.to]           | `string` | Recipient DID identifier                                    |
| \[params.message]      | `any`    | Message payload to send                                     |
| \[params.type]         | `string` | DIDComm message type                                        |
| \[params.did]          | `string` | @deprecated Use 'from' instead - Sender DID identifier      |
| \[params.recipientDid] | `string` | @deprecated Use 'to' instead - Recipient DID identifier     |
| \[params.body]         | `any`    | @deprecated Use 'message' instead - Message payload to send |

**Example**

```js
await messageProvider.sendMessage({
  from: 'did:key:sender123',
  to: 'did:key:recipient456',
  message: { hello: 'world' },
  type: 'basic-message'
});
```

### IMessageProvider.waitForMessage() ⇒ `Promise.<any>`

Waits for the next incoming message

**Kind**: static method of [`IMessageProvider`](core.md#IMessageProvider)\
**Returns**: `Promise.<any>` -

Promise that resolves with the next received message

\
**Example**

```js
const nextMessage = await messageProvider.waitForMessage();
console.log('Received message:', nextMessage);
```

### IMessageProvider.startAutoFetch(\[timeout]) ⇒ `function`

Starts automatic message fetching at regular intervals

**Kind**: static method of [`IMessageProvider`](core.md#IMessageProvider)\
**Returns**: `function` -

Function to stop the auto-fetch process

| Param      | Type     | Default | Description                                       |
| ---------- | -------- | ------- | ------------------------------------------------- |
| \[timeout] | `number` | `2000`  | Interval in milliseconds between fetch operations |

**Example**

```js
const stopAutoFetch = messageProvider.startAutoFetch(5000);
// Later, stop auto-fetching
stopAutoFetch();
```

### IMessageProvider.clearCache() ⇒ `Promise.<void>`

Clears all cached messages from the wallet

**Kind**: static method of [`IMessageProvider`](core.md#IMessageProvider)\
**Example**

```js
await messageProvider.clearCache();
console.log('All messages cleared');
```

## ICredentialProvider

Provides a high-level API for verifiable credential management operations

**Kind**: global interface

* [ICredentialProvider](core.md#ICredentialProvider)
  * [.getCredentials](core.md#ICredentialProvider.getCredentials) ⇒ `Array.<any>`
  * [.isBBSPlusCredential](core.md#ICredentialProvider.isBBSPlusCredential) ⇒ `boolean`
  * [.importCredentialFromURI(params)](core.md#ICredentialProvider.importCredentialFromURI) ⇒ `Promise.<any>`
  * [.getMembershipWitness(credentialId)](core.md#ICredentialProvider.getMembershipWitness) ⇒ `Promise.<any>`
  * [.getById(id)](core.md#ICredentialProvider.getById) ⇒ `any`
  * [.isValid(credential, \[forceFetch\])](core.md#ICredentialProvider.isValid) ⇒ `Promise.<Object>` | `string` | `string` | `string`
  * [.getCredentialStatus(credential)](core.md#ICredentialProvider.getCredentialStatus) ⇒ `Promise.<Object>` | `string` | `string`
  * [.syncCredentialStatus(params)](core.md#ICredentialProvider.syncCredentialStatus) ⇒ `Promise.<Array.<any>>`
  * [.addCredential(credential)](core.md#ICredentialProvider.addCredential) ⇒ `Promise.<any>`
  * [.removeCredential(credential)](core.md#ICredentialProvider.removeCredential) ⇒ `Promise.<void>`

### ICredentialProvider.getCredentials ⇒ `Array.<any>`

Retrieves credentials from the wallet, optionally filtered by type

**Kind**: static property of [`ICredentialProvider`](core.md#ICredentialProvider)\
**Returns**: `Array.<any>` -

Array of credentials matching the specified type

| Param   | Type     | Default                    | Description                      |
| ------- | -------- | -------------------------- | -------------------------------- |
| \[type] | `string` | `"'VerifiableCredential'"` | The credential type to filter by |

**Example**

```js
const allCredentials = credentialProvider.getCredentials();
const certificates = credentialProvider.getCredentials('Certificate');
```

### ICredentialProvider.isBBSPlusCredential ⇒ `boolean`

Checks if a credential uses BBS+ signature

**Kind**: static property of [`ICredentialProvider`](core.md#ICredentialProvider)\
**Returns**: `boolean` -

True if the credential uses BBS+ signature

| Param      | Type  | Description             |
| ---------- | ----- | ----------------------- |
| credential | `any` | The credential to check |

**Example**

```js
const isBBS = credentialProvider.isBBSPlusCredential(credential);
if (isBBS) {
  console.log('This credential uses BBS+ signatures');
}
```

### ICredentialProvider.importCredentialFromURI(params) ⇒ `Promise.<any>`

Imports a credential from a URI (supports OpenID credential offers)

**Kind**: static method of [`ICredentialProvider`](core.md#ICredentialProvider)\
**Returns**: `Promise.<any>` -

The imported credential

\
**Throws**:

*   `Error`

    If import fails

| Param                 | Type       | Description                               |
| --------------------- | ---------- | ----------------------------------------- |
| params                | `Object`   | Import parameters                         |
| params.uri            | `string`   | The URI containing the credential offer   |
| params.didProvider    | `any`      | DID provider instance for key management  |
| \[params.getAuthCode] | `function` | Optional callback to handle authorization |

**Example**

```js
const credential = await credentialProvider.importCredentialFromURI({
  uri: 'https://issuer.example.com/credential-offer',
  didProvider,
  getAuthCode: async (url) => getUserAuthCode(url)
});
```

### ICredentialProvider.getMembershipWitness(credentialId) ⇒ `Promise.<any>`

Gets the membership witness for a credential (used for BBS+ credentials)

**Kind**: static method of [`ICredentialProvider`](core.md#ICredentialProvider)\
**Returns**: `Promise.<any>` -

The membership witness data

| Param        | Type     | Description                              |
| ------------ | -------- | ---------------------------------------- |
| credentialId | `string` | The credential ID to get the witness for |

**Example**

```js
const witness = await credentialProvider.getMembershipWitness('credential-123');
```

### ICredentialProvider.getById(id) ⇒ `any`

Retrieves a credential by its ID

**Kind**: static method of [`ICredentialProvider`](core.md#ICredentialProvider)\
**Returns**: `any` -

The credential document

\
**Throws**:

*   `Error`

    If credential is not found

| Param | Type     | Description                             |
| ----- | -------- | --------------------------------------- |
| id    | `string` | The unique identifier of the credential |

**Example**

```js
const credential = await credentialProvider.getById('credential-123');
```

### ICredentialProvider.isValid(credential, \[forceFetch]) ⇒ `Promise.<Object>` | `string` | `string` | `string`

Validates a credential by verifying its cryptographic proof and status

**Kind**: static method of [`ICredentialProvider`](core.md#ICredentialProvider)\
**Returns**: `Promise.<Object>` -

Validation result

`string` -

returns.status - Validation status (verified, revoked, expired, invalid, pending)

`string` -

\[returns.error] - Error message if validation failed

`string` -

\[returns.warning] - Warning message if any

\
**Throws**:

*   `Error`

    If validation fails

| Param         | Type      | Default | Description                                    |
| ------------- | --------- | ------- | ---------------------------------------------- |
| credential    | `any`     |         | The credential to validate                     |
| \[forceFetch] | `boolean` | `false` | Whether to force refresh the credential status |

**Example**

```js
const result = await credentialProvider.isValid(credential);
if (result.status === 'verified') {
  console.log('Credential is valid');
} else if (result.status === 'revoked') {
  console.log('Credential has been revoked');
}
```

### ICredentialProvider.getCredentialStatus(credential) ⇒ `Promise.<Object>` | `string` | `string`

Gets the current status of a credential (cached, fast operation)

**Kind**: static method of [`ICredentialProvider`](core.md#ICredentialProvider)\
**Returns**: `Promise.<Object>` -

Current credential status

`string` -

returns.status - Current status of the credential

`string` -

\[returns.error] - Error message if any

| Param      | Type  | Description             |
| ---------- | ----- | ----------------------- |
| credential | `any` | The credential to check |

**Example**

```js
const status = await credentialProvider.getCredentialStatus(credential);
console.log(`Credential status: ${status.status}`);
```

### ICredentialProvider.syncCredentialStatus(params) ⇒ `Promise.<Array.<any>>`

Synchronizes credential status from the blockchain

**Kind**: static method of [`ICredentialProvider`](core.md#ICredentialProvider)\
**Returns**: `Promise.<Array.<any>>` -

Array of credential status documents

| Param                   | Type             | Default | Description                              |
| ----------------------- | ---------------- | ------- | ---------------------------------------- |
| params                  | `Object`         |         | Sync parameters                          |
| \[params.credentialIds] | `Array.<string>` |         | Optional list of credential IDs to sync  |
| \[params.forceFetch]    | `boolean`        | `false` | Whether to force refresh from blockchain |

**Example**

```js
// Sync all credentials
await credentialProvider.syncCredentialStatus({});

// Sync specific credentials
await credentialProvider.syncCredentialStatus({
  credentialIds: ['cred-1', 'cred-2'],
  forceFetch: true
});
```

### ICredentialProvider.addCredential(credential) ⇒ `Promise.<any>`

Adds a credential to the wallet

**Kind**: static method of [`ICredentialProvider`](core.md#ICredentialProvider)\
**Returns**: `Promise.<any>` -

The added credential document

| Param      | Type  | Description           |
| ---------- | ----- | --------------------- |
| credential | `any` | The credential to add |

**Example**

```js
const addedCredential = await credentialProvider.addCredential({
  '@context': ['https://www.w3.org/2018/credentials/v1'],
  type: ['VerifiableCredential'],
  issuer: 'did:dock:issuer123',
  credentialSubject: { name: 'Alice' }
});
```

### ICredentialProvider.removeCredential(credential) ⇒ `Promise.<void>`

Removes a credential and all its related documents from the wallet

**Kind**: static method of [`ICredentialProvider`](core.md#ICredentialProvider)\
**Throws**:

*   `Error`

    If credential is not found

| Param      | Type  | Description              |
| ---------- | ----- | ------------------------ |
| credential | `any` | The credential to remove |

**Example**

```js
await credentialProvider.removeCredential(credential);
// Or by ID
await credentialProvider.removeCredential('credential-123');
```

## IDVProcessOptions

Callback functions for handling different stages of the identity verification process

**Kind**: global interface\


## BiometricPlugin

Defines the contract for biometric enrollment and matching operations

**Kind**: global interface\


## IDVProvider

Defines the contract for identity verification operations

**Kind**: global interface\


## IDVProviderFactory

Creates IDV provider instances with proper event handling and wallet integration

**Kind**: global interface\


## IBiometricProvider

Provides a high-level API for biometric identity verification operations

**Kind**: global interface

* [IBiometricProvider](core.md#IBiometricProvider)
  * [.startIDV](core.md#IBiometricProvider.startIDV)
  * [.eventEmitter](core.md#IBiometricProvider.eventEmitter)
  * [.startIDV(proofRequest)](core.md#IBiometricProvider.startIDV) ⇒ `Promise.<{enrollmentCredential: Credential, matchCredential: Credential}>`

### IBiometricProvider.startIDV

Starts the identity verification process using biometric credentials

**Kind**: static property of [`IBiometricProvider`](core.md#IBiometricProvider)\


### IBiometricProvider.eventEmitter

Event emitter for IDV process events (onDeepLink, onMessage, onError, onCancel, onComplete)

**Kind**: static property of [`IBiometricProvider`](core.md#IBiometricProvider)\


### IBiometricProvider.startIDV(proofRequest) ⇒ `Promise.<{enrollmentCredential: Credential, matchCredential: Credential}>`

Starts the identity verification process using biometric credentials

**Kind**: static method of [`IBiometricProvider`](core.md#IBiometricProvider)\
**Returns**: `Promise.<{enrollmentCredential: Credential, matchCredential: Credential}>` -

The enrollment and match credentials

\
**Throws**:

*   `Error`

    If IDV process fails or biometric configs are missing

| Param        | Type  | Description                                         |
| ------------ | ----- | --------------------------------------------------- |
| proofRequest | `any` | The proof request containing biometric requirements |

**Example**

```js
const result = await biometricProvider.startIDV({
  input_descriptors: [{
    constraints: {
      fields: [{
        path: ['$.credentialSubject.biometric.id'],
        purpose: 'Biometric ID verification'
      }]
    }
  }]
});
```

## DefaultQRCodeProcessor

Default implementation of QRCodeProcessor

This processor manages a registry of QR code handlers and executes them in priority order to process scanned QR codes. It provides a flexible, extensible system for handling various types of QR codes in a wallet application.

**Kind**: global class

* [DefaultQRCodeProcessor](core.md#DefaultQRCodeProcessor)
  * [new DefaultQRCodeProcessor()](core.md#new_DefaultQRCodeProcessor_new)
  * [.registerHandler(handler)](core.md#DefaultQRCodeProcessor+registerHandler)
  * [.unregisterHandler(id)](core.md#DefaultQRCodeProcessor+unregisterHandler) ⇒
  * [.getHandlers()](core.md#DefaultQRCodeProcessor+getHandlers) ⇒
  * [.getHandler(id)](core.md#DefaultQRCodeProcessor+getHandler) ⇒
  * [.clearHandlers()](core.md#DefaultQRCodeProcessor+clearHandlers)
  * [.process(data, options)](core.md#DefaultQRCodeProcessor+process) ⇒
  * [.defaultPrepareContext(data)](core.md#DefaultQRCodeProcessor+defaultPrepareContext) ⇒
  * [.withTimeout(promise, timeoutMs)](core.md#DefaultQRCodeProcessor+withTimeout) ⇒

### new DefaultQRCodeProcessor()

**Example**

```typescript
const processor = new DefaultQRCodeProcessor();

// Register handlers
processor.registerHandler(new OID4VCHandler());
processor.registerHandler(new CredentialHandler());

// Process QR code
const result = await processor.process(scannedData);
if (result.success) {
  console.log('QR code processed:', result.data);
} else {
  console.error('Failed to process QR code:', result.error);
}
```

### defaultQRCodeProcessor.registerHandler(handler)

Register a new QR code handler

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Throws**:

* Error if a handler with the same ID is already registered

| Param   | Description             |
| ------- | ----------------------- |
| handler | The handler to register |

### defaultQRCodeProcessor.unregisterHandler(id) ⇒

Unregister a QR code handler by its ID

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

True if the handler was found and removed, false otherwise

| Param | Description                         |
| ----- | ----------------------------------- |
| id    | The ID of the handler to unregister |

### defaultQRCodeProcessor.getHandlers() ⇒

Get all registered handlers sorted by priority

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

Array of registered handlers sorted by priority (lowest first)

\


### defaultQRCodeProcessor.getHandler(id) ⇒

Get a specific handler by its ID

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

The handler if found, undefined otherwise

| Param | Description                       |
| ----- | --------------------------------- |
| id    | The ID of the handler to retrieve |

### defaultQRCodeProcessor.clearHandlers()

Clear all registered handlers

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\


### defaultQRCodeProcessor.process(data, options) ⇒

Process QR code data through registered handlers

This method:

1. Prepares the context from raw QR data
2. Executes handlers in priority order
3. Returns the first successful result (or continues if stopOnFirstSuccess is false)
4. Returns an error result if no handler can process the data

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

Result of the processing

| Param   | Description             |
| ------- | ----------------------- |
| data    | Raw QR code data string |
| options | Processing options      |

### defaultQRCodeProcessor.defaultPrepareContext(data) ⇒

Default context preparation function

This method attempts to parse the raw QR data as JSON or URL. Override this by providing a custom prepareContext function in ProcessOptions.

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

Prepared context object

| Param | Description             |
| ----- | ----------------------- |
| data  | Raw QR code data string |

### defaultQRCodeProcessor.withTimeout(promise, timeoutMs) ⇒

Execute a promise with a timeout

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

Result of the promise

\
**Throws**:

* Error if the promise times out

| Param     | Description             |
| --------- | ----------------------- |
| promise   | Promise to execute      |
| timeoutMs | Timeout in milliseconds |

## Goals ⇒

**Kind**: global variable\
**Returns**:

OOB message to start a wallet to wallet verification flow The holder will scan it as QR code and should have the context to start the verification flow

\


## dockDocumentNetworkResolver

Given an Api URL, resolve the network ID For now it will be applied for creds and certs It can be extended to resolve other external URLs

**Kind**: global variable\


## OID4VCHandler ⇒

Create an OID4VC handler with custom configuration

This is a convenience factory function for creating an OID4VC handler.

**Kind**: global variable\
**Returns**:

Configured OID4VC handler

| Param  | Description           |
| ------ | --------------------- |
| config | Handler configuration |

**Example**

```typescript
const handler = createOID4VCHandler({
  onImportCredential: async (uri) => {
    // Your import logic
    return { success: true };
  },
});
```

* [OID4VCHandler](core.md#OID4VCHandler) ⇒
  * [.canHandle(context)](core.md#OID4VCHandler+canHandle) ⇒
  * [.handle(context)](core.md#OID4VCHandler+handle) ⇒

### oiD4VCHandler.canHandle(context) ⇒

Check if this is an OID4VC URI

Matches URIs that start with any of the configured prefixes. By default, matches: openid-credential-offer://

**Kind**: instance method of [`OID4VCHandler`](core.md#OID4VCHandler)\
**Returns**:

True if this handler can process the URI

| Param   | Description         |
| ------- | ------------------- |
| context | The QR code context |

### oiD4VCHandler.handle(context) ⇒

Process the OID4VC credential offer URI

Delegates to the configured onImportCredential callback for actual processing. This allows apps to implement their own navigation, UI, and error handling.

**Kind**: instance method of [`OID4VCHandler`](core.md#OID4VCHandler)\
**Returns**:

Result of the processing

| Param   | Description         |
| ------- | ------------------- |
| context | The QR code context |

## DefaultQRCodeProcessor ⇒

Create a new QR code processor instance

This is a convenience factory function for creating a processor.

**Kind**: global variable\
**Returns**:

New processor instance with handlers registered

| Param    | Description                                        |
| -------- | -------------------------------------------------- |
| handlers | Optional array of handlers to register immediately |

**Example**

```typescript
const processor = createQRCodeProcessor([
  new OID4VCHandler(),
  new CredentialHandler(),
]);
```

* [DefaultQRCodeProcessor](core.md#DefaultQRCodeProcessor) ⇒
  * [new DefaultQRCodeProcessor()](core.md#new_DefaultQRCodeProcessor_new)
  * [.registerHandler(handler)](core.md#DefaultQRCodeProcessor+registerHandler)
  * [.unregisterHandler(id)](core.md#DefaultQRCodeProcessor+unregisterHandler) ⇒
  * [.getHandlers()](core.md#DefaultQRCodeProcessor+getHandlers) ⇒
  * [.getHandler(id)](core.md#DefaultQRCodeProcessor+getHandler) ⇒
  * [.clearHandlers()](core.md#DefaultQRCodeProcessor+clearHandlers)
  * [.process(data, options)](core.md#DefaultQRCodeProcessor+process) ⇒
  * [.defaultPrepareContext(data)](core.md#DefaultQRCodeProcessor+defaultPrepareContext) ⇒
  * [.withTimeout(promise, timeoutMs)](core.md#DefaultQRCodeProcessor+withTimeout) ⇒

### new DefaultQRCodeProcessor()

**Example**

```typescript
const processor = new DefaultQRCodeProcessor();

// Register handlers
processor.registerHandler(new OID4VCHandler());
processor.registerHandler(new CredentialHandler());

// Process QR code
const result = await processor.process(scannedData);
if (result.success) {
  console.log('QR code processed:', result.data);
} else {
  console.error('Failed to process QR code:', result.error);
}
```

### defaultQRCodeProcessor.registerHandler(handler)

Register a new QR code handler

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Throws**:

* Error if a handler with the same ID is already registered

| Param   | Description             |
| ------- | ----------------------- |
| handler | The handler to register |

### defaultQRCodeProcessor.unregisterHandler(id) ⇒

Unregister a QR code handler by its ID

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

True if the handler was found and removed, false otherwise

| Param | Description                         |
| ----- | ----------------------------------- |
| id    | The ID of the handler to unregister |

### defaultQRCodeProcessor.getHandlers() ⇒

Get all registered handlers sorted by priority

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

Array of registered handlers sorted by priority (lowest first)

\


### defaultQRCodeProcessor.getHandler(id) ⇒

Get a specific handler by its ID

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

The handler if found, undefined otherwise

| Param | Description                       |
| ----- | --------------------------------- |
| id    | The ID of the handler to retrieve |

### defaultQRCodeProcessor.clearHandlers()

Clear all registered handlers

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\


### defaultQRCodeProcessor.process(data, options) ⇒

Process QR code data through registered handlers

This method:

1. Prepares the context from raw QR data
2. Executes handlers in priority order
3. Returns the first successful result (or continues if stopOnFirstSuccess is false)
4. Returns an error result if no handler can process the data

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

Result of the processing

| Param   | Description             |
| ------- | ----------------------- |
| data    | Raw QR code data string |
| options | Processing options      |

### defaultQRCodeProcessor.defaultPrepareContext(data) ⇒

Default context preparation function

This method attempts to parse the raw QR data as JSON or URL. Override this by providing a custom prepareContext function in ProcessOptions.

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

Prepared context object

| Param | Description             |
| ----- | ----------------------- |
| data  | Raw QR code data string |

### defaultQRCodeProcessor.withTimeout(promise, timeoutMs) ⇒

Execute a promise with a timeout

**Kind**: instance method of [`DefaultQRCodeProcessor`](core.md#DefaultQRCodeProcessor)\
**Returns**:

Result of the promise

\
**Throws**:

* Error if the promise times out

| Param     | Description             |
| --------- | ----------------------- |
| promise   | Promise to execute      |
| timeoutMs | Timeout in milliseconds |

## MessageTypes

DIDComm Message helpers Check https://identity.foundation/didcomm-messaging/spec/#out-of-band-messages for more details

**Kind**: global constant\


## buildRequestVerifiablePresentationMessage()

Sender: Verifier OOB message to request a verifiable presentation from the holder

**Kind**: global function\


## buildAckWalletToWalletVerificationMessage()

Sender: Holder Start a wallet to wallet verification flow

**Kind**: global function\


## buildVerifiablePresentationMessage()

Sender: Holder Send a verifiable presentation to the verifier

**Kind**: global function\


## buildVerifiablePresentationAckMessage()

Sender: Verifier Sends an the presentation result to the holder

**Kind**: global function\


## handleBlockchainNetworkChange()

Update existing substrate network connection Compare connected substrate connection with the current walle network Disconnect and Establish a new connection if the network is different

**Kind**: global function\


## WalletStatus : `'closed'` | `'loading'` | `'ready'` | `'error'`

Possible wallet status values

**Kind**: global typedef\


## KeypairType : `'sr25519'` | `'ed25519'` | `'ecdsa'`

Supported keypair types

**Kind**: global typedef\


## BiometricsProviderConfigs : `Object`

Configuration options for biometric provider operations

**Kind**: global typedef\
**Properties**

| Name                         | Type     | Description                                       |
| ---------------------------- | -------- | ------------------------------------------------- |
| enrollmentCredentialType     | `string` | The credential type used for biometric enrollment |
| biometricMatchCredentialType | `string` | The credential type used for biometric matching   |
| idvConfigs                   | `E`      | IDV provider-specific configuration options       |

## OID4VCHandler

Built-in handler for OID4VC (OpenID for Verifiable Credentials) URIs

This is a generic handler that can be configured with app-specific callbacks for importing credentials. The handler itself only handles protocol detection and delegates the actual import logic to the configured callback.

## Example Usage

```
import { OID4VCHandler } from '@docknetwork/wallet-sdk-core/src/qr-handlers/builtin';
import { getCredentialProvider } from '@docknetwork/wallet-sdk-react-native';
const handler = new OID4VCHandler({
onImportCredential: async (uri, context) => {
try {
// Use SDK to import credential
await getCredentialProvider().importCredentialFromURI({
uri,
didProvider: getDIDProvider(),
getAuthCode: async (authUrl) => {
// App-specific auth handling
return await showAuthWebView(authUrl);
},
});
  return { success: true };} catch (error) {  return {    success: false,    error: error instanceof Error ? error : new Error(String(error)),  };}
},
});
processor.registerHandler(handler);
```

## Handler Priority

Default priority: 5 (very high) This ensures OID4VC URIs are checked before other credential handlers.

**Kind**: global class\
**Category**: Built-in Handlers

* [OID4VCHandler](core.md#OID4VCHandler)
  * [.canHandle(context)](core.md#OID4VCHandler+canHandle) ⇒
  * [.handle(context)](core.md#OID4VCHandler+handle) ⇒

### oiD4VCHandler.canHandle(context) ⇒

Check if this is an OID4VC URI

Matches URIs that start with any of the configured prefixes. By default, matches: openid-credential-offer://

**Kind**: instance method of [`OID4VCHandler`](core.md#OID4VCHandler)\
**Returns**:

True if this handler can process the URI

| Param   | Description         |
| ------- | ------------------- |
| context | The QR code context |

### oiD4VCHandler.handle(context) ⇒

Process the OID4VC credential offer URI

Delegates to the configured onImportCredential callback for actual processing. This allows apps to implement their own navigation, UI, and error handling.

**Kind**: instance method of [`OID4VCHandler`](core.md#OID4VCHandler)\
**Returns**:

Result of the processing

| Param   | Description         |
| ------- | ------------------- |
| context | The QR code context |
