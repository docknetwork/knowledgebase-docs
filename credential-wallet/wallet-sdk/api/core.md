# Wallet SDK Core API Documentation

## Modules

[cloud-wallet](core.md#module_cloud-wallet)

Cloud wallet functionality for the Truvera Wallet SDK. This module provides the main cloud wallet creation and management functions.

[wallet](core.md#module_wallet)

Core wallet functionality for the Dock Wallet SDK. This module provides the main wallet creation and management functions.

## Members

[Goals](core.md#Goals) ⇒[dockDocumentNetworkResolver](core.md#dockDocumentNetworkResolver)

Given an Api URL, resolve the network ID For now it will be applied for creds and certs It can be extended to resolve other external URLs

## Constants

[MessageTypes](core.md#MessageTypes)

DIDComm Message helpers Check https://identity.foundation/didcomm-messaging/spec/#out-of-band-messages for more details

## Functions

[isValid(credential)](core.md#isValid) ⇒ `Promise.<Object>`

Uses Dock SDK to verify a credential

[syncCredentialStatus(param0)](core.md#syncCredentialStatus) ⇒

Fetch credential status from the chain and update the wallet Store a new document #status in the wallet Returns a list of CredentialStatusDocument

[removeCredential(param0)](core.md#removeCredential) ⇒ `Promise.<void>`

Removes a credential and its related documents from the wallet

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

## Interfaces

[~~IV1Wallet~~](core.md#IV1Wallet)

Legacy V1 wallet interface for backward compatibility

[IWallet](core.md#IWallet) ⇐ [`IV1Wallet`](core.md#IV1Wallet)

Main wallet interface providing methods for document management, import/export, and network operations.

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

## Goals ⇒

**Kind**: global variable\
**Returns**:

OOB message to start a wallet to wallet verification flow The holder will scan it as QR code and should have the context to start the verification flow

\


## dockDocumentNetworkResolver

Given an Api URL, resolve the network ID For now it will be applied for creds and certs It can be extended to resolve other external URLs

**Kind**: global variable\


## MessageTypes

DIDComm Message helpers Check https://identity.foundation/didcomm-messaging/spec/#out-of-band-messages for more details

**Kind**: global constant\


## isValid(credential) ⇒ `Promise.<Object>`

Uses Dock SDK to verify a credential

**Kind**: global function\
**Returns**: `Promise.<Object>` -

Verification result with status and optional error/warning messages

| Param      |
| ---------- |
| credential |

## syncCredentialStatus(param0) ⇒

Fetch credential status from the chain and update the wallet Store a new document #status in the wallet Returns a list of CredentialStatusDocument

**Kind**: global function\
**Returns**:

CredentialStatusDocument\[]

| Param  |
| ------ |
| param0 |

## removeCredential(param0) ⇒ `Promise.<void>`

Removes a credential and its related documents from the wallet

**Kind**: global function

| Param  |
| ------ |
| param0 |

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

**Kind**: global typedef
