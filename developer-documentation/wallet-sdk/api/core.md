# Wallet SDK Core API Documentation

## Modules

<dl>
<dt><a href="#module_cloud-wallet">cloud-wallet</a></dt>
<dd><p>Cloud wallet functionality for the Truvera Wallet SDK.
This module provides the main cloud wallet creation and management functions.</p></dd>
<dt><a href="#module_wallet">wallet</a></dt>
<dd><p>Core wallet functionality for the Dock Wallet SDK.
This module provides the main wallet creation and management functions.</p></dd>
</dl>

## Members

<dl>
<dt><a href="#Goals">Goals</a> ⇒</dt>
<dd></dd>
<dt><a href="#dockDocumentNetworkResolver">dockDocumentNetworkResolver</a></dt>
<dd><p>Given an Api URL, resolve the network ID
For now it will be applied for creds and certs
It can be extended to resolve other external URLs</p></dd>
</dl>

## Constants

<dl>
<dt><a href="#MessageTypes">MessageTypes</a></dt>
<dd><p>DIDComm Message helpers
Check https://identity.foundation/didcomm-messaging/spec/#out-of-band-messages for more details</p></dd>
</dl>

## Functions

<dl>
<dt><a href="#isValid">isValid(credential)</a> ⇒ <code>Promise.&lt;Object&gt;</code></dt>
<dd><p>Uses Dock SDK to verify a credential</p></dd>
<dt><a href="#syncCredentialStatus">syncCredentialStatus(param0)</a> ⇒</dt>
<dd><p>Fetch credential status from the chain and update the wallet
Store a new document <credentialId>#status in the wallet
Returns a list of CredentialStatusDocument</p></dd>
<dt><a href="#removeCredential">removeCredential(param0)</a> ⇒ <code>Promise.&lt;void&gt;</code></dt>
<dd><p>Removes a credential and its related documents from the wallet</p></dd>
<dt><a href="#buildRequestVerifiablePresentationMessage">buildRequestVerifiablePresentationMessage()</a></dt>
<dd><p>Sender: Verifier
OOB message to request a verifiable presentation from the holder</p></dd>
<dt><a href="#buildAckWalletToWalletVerificationMessage">buildAckWalletToWalletVerificationMessage()</a></dt>
<dd><p>Sender: Holder
Start a wallet to wallet verification flow</p></dd>
<dt><a href="#buildVerifiablePresentationMessage">buildVerifiablePresentationMessage()</a></dt>
<dd><p>Sender: Holder
Send a verifiable presentation to the verifier</p></dd>
<dt><a href="#buildVerifiablePresentationAckMessage">buildVerifiablePresentationAckMessage()</a></dt>
<dd><p>Sender: Verifier
Sends an the presentation result to the holder</p></dd>
<dt><a href="#handleBlockchainNetworkChange">handleBlockchainNetworkChange()</a></dt>
<dd><p>Update existing substrate network connection
Compare connected substrate connection with the current walle network
Disconnect and Establish a new connection if the network is different</p></dd>
</dl>

## Typedefs

<dl>
<dt><a href="#WalletStatus">WalletStatus</a> : <code>&#x27;closed&#x27;</code> | <code>&#x27;loading&#x27;</code> | <code>&#x27;ready&#x27;</code> | <code>&#x27;error&#x27;</code></dt>
<dd><p>Possible wallet status values</p></dd>
<dt><a href="#KeypairType">KeypairType</a> : <code>&#x27;sr25519&#x27;</code> | <code>&#x27;ed25519&#x27;</code> | <code>&#x27;ecdsa&#x27;</code></dt>
<dd><p>Supported keypair types</p></dd>
</dl>

## Interfaces

<dl>
<dt><del><a href="#IV1Wallet">IV1Wallet</a></del></dt>
<dd><p>Legacy V1 wallet interface for backward compatibility</p></dd>
<dt><a href="#IWallet">IWallet</a> ⇐ <code><a href="#IV1Wallet">IV1Wallet</a></code></dt>
<dd><p>Main wallet interface providing methods for document management, import/export, and network operations.</p></dd>
</dl>

<a name="module_cloud-wallet"></a>

## cloud-wallet
<p>Cloud wallet functionality for the Truvera Wallet SDK.
This module provides the main cloud wallet creation and management functions.</p>


* [cloud-wallet](#module_cloud-wallet)
    * [~deriveBiometricKey(biometricData, identifier)](#module_cloud-wallet..deriveBiometricKey) ⇒
    * [~deriveKeyMappingVaultKeys(biometricData, identifier)](#module_cloud-wallet..deriveKeyMappingVaultKeys) ⇒
    * [~deriveBiometricEncryptionKey(biometricData, identifier)](#module_cloud-wallet..deriveBiometricEncryptionKey) ⇒
    * [~encryptMasterKey(masterKey, encryptionKey, iv)](#module_cloud-wallet..encryptMasterKey) ⇒
    * [~decryptMasterKey(encryptedKey, decryptionKey, iv)](#module_cloud-wallet..decryptMasterKey) ⇒
    * [~initializeKeyMappingVault(edvUrl, authKey, biometricData, identifier)](#module_cloud-wallet..initializeKeyMappingVault) ⇒
    * [~enrollUserWithBiometrics(edvUrl, authKey, biometricData, identifier)](#module_cloud-wallet..enrollUserWithBiometrics) ⇒
    * [~getKeyMappingMasterKey(keyMappingEdv, identifier, decryptionKey, iv)](#module_cloud-wallet..getKeyMappingMasterKey) ⇒
    * [~authenticateWithBiometrics(edvUrl, authKey, biometricData, identifier)](#module_cloud-wallet..authenticateWithBiometrics) ⇒
    * [~initializeCloudWalletWithBiometrics(edvUrl, authKey, biometricData, identifier, dataStore)](#module_cloud-wallet..initializeCloudWalletWithBiometrics) ⇒

<a name="module_cloud-wallet..deriveBiometricKey"></a>

### cloud-wallet~deriveBiometricKey(biometricData, identifier) ⇒
<p>Derives a key from biometric data using HKDF</p>

**Kind**: inner method of [<code>cloud-wallet</code>](#module_cloud-wallet)  
**Returns**: <p>Derived key</p>  

| Param | Description |
| --- | --- |
| biometricData | <p>Biometric data from provider</p> |
| identifier | <p>User's identifier as salt (email, phone number, etc.)</p> |

<a name="module_cloud-wallet..deriveKeyMappingVaultKeys"></a>

### cloud-wallet~deriveKeyMappingVaultKeys(biometricData, identifier) ⇒
<p>Derives EDV keys from biometric data for the KeyMappingVault</p>

**Kind**: inner method of [<code>cloud-wallet</code>](#module_cloud-wallet)  
**Returns**: <p>Keys for accessing the KeyMappingVault</p>  

| Param | Description |
| --- | --- |
| biometricData | <p>Biometric data from the provider</p> |
| identifier | <p>User's identifier as additional entropy (email, phone number, etc.)</p> |

<a name="module_cloud-wallet..deriveBiometricEncryptionKey"></a>

### cloud-wallet~deriveBiometricEncryptionKey(biometricData, identifier) ⇒
<p>Generates a key for encrypting/decrypting the master key</p>

**Kind**: inner method of [<code>cloud-wallet</code>](#module_cloud-wallet)  
**Returns**: <p>Encryption key and IV for AES encryption</p>  

| Param | Description |
| --- | --- |
| biometricData | <p>Biometric data from provider</p> |
| identifier | <p>User's identifier as salt (email, phone number, etc.)</p> |

<a name="module_cloud-wallet..encryptMasterKey"></a>

### cloud-wallet~encryptMasterKey(masterKey, encryptionKey, iv) ⇒
<p>Encrypts the master key using a key derived from biometric data</p>

**Kind**: inner method of [<code>cloud-wallet</code>](#module_cloud-wallet)  
**Returns**: <p>Encrypted master key</p>  

| Param | Description |
| --- | --- |
| masterKey | <p>The CloudWalletVault master key to encrypt</p> |
| encryptionKey | <p>Key derived from biometric data</p> |
| iv | <p>Initialization vector</p> |

<a name="module_cloud-wallet..decryptMasterKey"></a>

### cloud-wallet~decryptMasterKey(encryptedKey, decryptionKey, iv) ⇒
<p>Decrypts the master key using biometric-derived key</p>

**Kind**: inner method of [<code>cloud-wallet</code>](#module_cloud-wallet)  
**Returns**: <p>The decrypted master key</p>  

| Param | Description |
| --- | --- |
| encryptedKey | <p>The encrypted master key</p> |
| decryptionKey | <p>Key derived from biometric data</p> |
| iv | <p>Initialization vector</p> |

<a name="module_cloud-wallet..initializeKeyMappingVault"></a>

### cloud-wallet~initializeKeyMappingVault(edvUrl, authKey, biometricData, identifier) ⇒
<p>Initializes the KeyMappingVault using biometric data</p>

**Kind**: inner method of [<code>cloud-wallet</code>](#module_cloud-wallet)  
**Returns**: <p>Initialized EDV service</p>  

| Param | Description |
| --- | --- |
| edvUrl | <p>URL for the edv</p> |
| authKey | <p>Auth key for the edv</p> |
| biometricData | <p>User's biometric data</p> |
| identifier | <p>User's identifier (email, phone number, etc.)</p> |

<a name="module_cloud-wallet..enrollUserWithBiometrics"></a>

### cloud-wallet~enrollUserWithBiometrics(edvUrl, authKey, biometricData, identifier) ⇒
<p>Enrolls a user by creating necessary vaults and keys</p>

**Kind**: inner method of [<code>cloud-wallet</code>](#module_cloud-wallet)  
**Returns**: <p>The master key and mnemonic for backup</p>  

| Param | Description |
| --- | --- |
| edvUrl | <p>URL for the edv</p> |
| authKey | <p>Auth key for the edv</p> |
| biometricData | <p>Biometric data from provider</p> |
| identifier | <p>User's identifier (email, phone number, etc.)</p> |

<a name="module_cloud-wallet..getKeyMappingMasterKey"></a>

### cloud-wallet~getKeyMappingMasterKey(keyMappingEdv, identifier, decryptionKey, iv) ⇒
<p>Gets the master key from the key mapping vault using provided decryption keys</p>

**Kind**: inner method of [<code>cloud-wallet</code>](#module_cloud-wallet)  
**Returns**: <p>The decrypted master key for CloudWalletVault</p>  

| Param | Description |
| --- | --- |
| keyMappingEdv | <p>Initialized key mapping vault service</p> |
| identifier | <p>User's identifier (email, phone number, etc.)</p> |
| decryptionKey | <p>Key for decrypting the master key</p> |
| iv | <p>Initialization vector for decryption</p> |

<a name="module_cloud-wallet..authenticateWithBiometrics"></a>

### cloud-wallet~authenticateWithBiometrics(edvUrl, authKey, biometricData, identifier) ⇒
<p>Authenticates a user with biometric data and identifier</p>

**Kind**: inner method of [<code>cloud-wallet</code>](#module_cloud-wallet)  
**Returns**: <p>The decrypted master key for CloudWalletVault</p>  

| Param | Description |
| --- | --- |
| edvUrl | <p>URL for the edv</p> |
| authKey | <p>Auth key for the edv</p> |
| biometricData | <p>Biometric data from the provider</p> |
| identifier | <p>User's identifier (email, phone number, etc.)</p> |

<a name="module_cloud-wallet..initializeCloudWalletWithBiometrics"></a>

### cloud-wallet~initializeCloudWalletWithBiometrics(edvUrl, authKey, biometricData, identifier, dataStore) ⇒
<p>Initializes the Cloud Wallet using biometric authentication</p>

**Kind**: inner method of [<code>cloud-wallet</code>](#module_cloud-wallet)  
**Returns**: <p>Initialized cloud wallet</p>  

| Param | Description |
| --- | --- |
| edvUrl | <p>Cloud wallet vault URL</p> |
| authKey | <p>Cloud wallet auth key</p> |
| biometricData | <p>User's biometric data</p> |
| identifier | <p>User's identifier (email, phone number, etc.)</p> |
| dataStore | <p>Optional data store for the wallet</p> |

<a name="module_wallet"></a>

## wallet
<p>Core wallet functionality for the Dock Wallet SDK.
This module provides the main wallet creation and management functions.</p>

<a name="module_wallet..createWallet"></a>

### wallet~createWallet(props) ⇒ [<code>Promise.&lt;IWallet&gt;</code>](#IWallet)
<p>Creates a new wallet instance with the provided data store.
The wallet provides secure storage and management of DIDs, credentials, keys, and other documents.</p>

**Kind**: inner method of [<code>wallet</code>](#module_wallet)  
**Returns**: [<code>Promise.&lt;IWallet&gt;</code>](#IWallet) - <p>A promise that resolves to the created wallet instance</p>  
**Throws**:

- <code>Error</code> <p>If the data store is not properly initialized</p>

**See**: [IWallet](#IWallet) - The interface defining all available wallet methods  

| Param | Type | Description |
| --- | --- | --- |
| props | <code>CreateWalletProps</code> | <p>Configuration options for wallet creation</p> |
| props.dataStore | <code>DataStore</code> | <p>The data store implementation to use for persistence</p> |

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
<a name="IV1Wallet"></a>

## ~~IV1Wallet~~
***This interface is obsolete and should not be used for new implementations. Use IWallet instead.***

<p>Legacy V1 wallet interface for backward compatibility</p>

**Kind**: global interface  
<a name="IWallet"></a>

## IWallet ⇐ [<code>IV1Wallet</code>](#IV1Wallet)
<p>Main wallet interface providing methods for document management, import/export, and network operations.</p>

**Kind**: global interface  
**Extends**: [<code>IV1Wallet</code>](#IV1Wallet)  

* [IWallet](#IWallet) ⇐ [<code>IV1Wallet</code>](#IV1Wallet)
    * [.deleteWallet()](#IWallet.deleteWallet) ⇒ <code>Promise.&lt;void&gt;</code>
    * [.setStatus(newStatus)](#IWallet.setStatus)
    * [.setNetwork(networkId)](#IWallet.setNetwork) ⇒ <code>Promise.&lt;void&gt;</code>
    * [.getNetworkId()](#IWallet.getNetworkId) ⇒ <code>string</code>
    * [.getDocumentById(id)](#IWallet.getDocumentById) ⇒ <code>Promise.&lt;WalletDocument&gt;</code>
    * [.getAllDocuments()](#IWallet.getAllDocuments) ⇒ <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code>
    * [.getDocumentsById(idList)](#IWallet.getDocumentsById) ⇒ <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code>
    * [.getDocumentsByType(type)](#IWallet.getDocumentsByType) ⇒ <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code>
    * [.addDocument(json, [options])](#IWallet.addDocument) ⇒ <code>Promise.&lt;WalletDocument&gt;</code>
    * [.updateDocument(document, [options])](#IWallet.updateDocument) ⇒ <code>Promise.&lt;WalletDocument&gt;</code>
    * [.removeDocument(id, [options])](#IWallet.removeDocument) ⇒ <code>Promise.&lt;void&gt;</code>
    * [.getDocumentCorrelations(documentId)](#IWallet.getDocumentCorrelations) ⇒ <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code>
    * [.getAccountKeyPair(accountId)](#IWallet.getAccountKeyPair) ⇒ <code>Promise.&lt;any&gt;</code>
    * [.getDocumentsFromEncryptedWallet(json, password)](#IWallet.getDocumentsFromEncryptedWallet) ⇒ <code>Promise.&lt;any&gt;</code>
    * [.importUniversalWalletJSON(json, password)](#IWallet.importUniversalWalletJSON) ⇒ <code>Promise.&lt;void&gt;</code>
    * [.exportDocuments(params)](#IWallet.exportDocuments) ⇒ <code>Promise.&lt;any&gt;</code>
    * [.exportUniversalWalletJSON(password)](#IWallet.exportUniversalWalletJSON) ⇒ <code>any</code>

<a name="IWallet.deleteWallet"></a>

### IWallet.deleteWallet() ⇒ <code>Promise.&lt;void&gt;</code>
<p>Deletes the entire wallet and all its documents</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Emits**: <code>WalletEvents.event:walletDeleted</code>  
<a name="IWallet.setStatus"></a>

### IWallet.setStatus(newStatus)
<p>Sets the wallet status</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  

| Param | Type | Description |
| --- | --- | --- |
| newStatus | <code>string</code> | <p>The new status to set</p> |

<a name="IWallet.setNetwork"></a>

### IWallet.setNetwork(networkId) ⇒ <code>Promise.&lt;void&gt;</code>
<p>Sets the active network for the wallet</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Emits**: <code>WalletEvents.event:networkUpdated</code>  

| Param | Type | Description |
| --- | --- | --- |
| networkId | <code>string</code> | <p>The network identifier to switch to</p> |

<a name="IWallet.getNetworkId"></a>

### IWallet.getNetworkId() ⇒ <code>string</code>
<p>Gets the current network ID</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>string</code> - <p>The current network identifier</p>  
<a name="IWallet.getDocumentById"></a>

### IWallet.getDocumentById(id) ⇒ <code>Promise.&lt;WalletDocument&gt;</code>
<p>Retrieves a document by its ID</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>Promise.&lt;WalletDocument&gt;</code> - <p>The document with the specified ID</p>  
**Throws**:

- <code>Error</code> <p>If document is not found</p>


| Param | Type | Description |
| --- | --- | --- |
| id | <code>string</code> | <p>The unique identifier of the document</p> |

<a name="IWallet.getAllDocuments"></a>

### IWallet.getAllDocuments() ⇒ <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code>
<p>Retrieves all documents stored in the wallet</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code> - <p>Array of all documents in the wallet</p>  
<a name="IWallet.getDocumentsById"></a>

### IWallet.getDocumentsById(idList) ⇒ <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code>
<p>Retrieves multiple documents by their IDs</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code> - <p>Array of documents matching the provided IDs</p>  

| Param | Type | Description |
| --- | --- | --- |
| idList | <code>Array.&lt;string&gt;</code> | <p>Array of document IDs to retrieve</p> |

<a name="IWallet.getDocumentsByType"></a>

### IWallet.getDocumentsByType(type) ⇒ <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code>
<p>Retrieves all documents of a specific type</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code> - <p>Array of documents matching the specified type</p>  

| Param | Type | Description |
| --- | --- | --- |
| type | <code>string</code> | <p>The document type to filter by (e.g., 'VerifiableCredential', 'DIDDocument')</p> |

<a name="IWallet.addDocument"></a>

### IWallet.addDocument(json, [options]) ⇒ <code>Promise.&lt;WalletDocument&gt;</code>
<p>Adds a new document to the wallet</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>Promise.&lt;WalletDocument&gt;</code> - <p>The created document with generated metadata</p>  
**Emits**: <code>WalletEvents.event:documentAdded</code>  

| Param | Type | Description |
| --- | --- | --- |
| json | <code>any</code> | <p>The document to add (must have valid JSON-LD structure)</p> |
| [options] | <code>any</code> | <p>Optional parameters for document creation</p> |

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
<a name="IWallet.updateDocument"></a>

### IWallet.updateDocument(document, [options]) ⇒ <code>Promise.&lt;WalletDocument&gt;</code>
<p>Updates an existing document</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>Promise.&lt;WalletDocument&gt;</code> - <p>The updated document</p>  
**Throws**:

- <code>Error</code> <p>If document doesn't exist</p>

**Emits**: <code>WalletEvents.event:documentUpdated</code>  

| Param | Type | Description |
| --- | --- | --- |
| document | <code>any</code> | <p>The document with updated data (must include ID)</p> |
| [options] | <code>any</code> | <p>Optional parameters for document update</p> |

<a name="IWallet.removeDocument"></a>

### IWallet.removeDocument(id, [options]) ⇒ <code>Promise.&lt;void&gt;</code>
<p>Removes a document from the wallet</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Throws**:

- <code>Error</code> <p>If document is not found</p>

**Emits**: <code>WalletEvents.event:documentRemoved</code>  

| Param | Type | Description |
| --- | --- | --- |
| id | <code>string</code> | <p>The ID of the document to remove</p> |
| [options] | <code>any</code> | <p>Optional parameters for document removal</p> |

<a name="IWallet.getDocumentCorrelations"></a>

### IWallet.getDocumentCorrelations(documentId) ⇒ <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code>
<p>Gets all documents correlated to a specific document</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>Promise.&lt;Array.&lt;WalletDocument&gt;&gt;</code> - <p>Array of correlated documents</p>  

| Param | Type | Description |
| --- | --- | --- |
| documentId | <code>string</code> | <p>The ID of the document to find correlations for</p> |

<a name="IWallet.getAccountKeyPair"></a>

### IWallet.getAccountKeyPair(accountId) ⇒ <code>Promise.&lt;any&gt;</code>
<p>Retrieves the keypair associated with an account</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>Promise.&lt;any&gt;</code> - <p>The keypair associated with the account</p>  

| Param | Type | Description |
| --- | --- | --- |
| accountId | <code>string</code> | <p>The account ID to get the keypair for</p> |

<a name="IWallet.getDocumentsFromEncryptedWallet"></a>

### IWallet.getDocumentsFromEncryptedWallet(json, password) ⇒ <code>Promise.&lt;any&gt;</code>
<p>Decrypts and retrieves documents from an encrypted wallet without importing</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>Promise.&lt;any&gt;</code> - <p>Array of decrypted documents</p>  

| Param | Type | Description |
| --- | --- | --- |
| json | <code>any</code> | <p>The encrypted wallet JSON</p> |
| password | <code>string</code> | <p>Password to decrypt the wallet</p> |

<a name="IWallet.importUniversalWalletJSON"></a>

### IWallet.importUniversalWalletJSON(json, password) ⇒ <code>Promise.&lt;void&gt;</code>
<p>Imports documents from an encrypted Universal Wallet 2020 JSON</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**See**: [https://w3c-ccg.github.io/universal-wallet-interop-spec/](https://w3c-ccg.github.io/universal-wallet-interop-spec/)  

| Param | Type | Description |
| --- | --- | --- |
| json | <code>any</code> | <p>The encrypted wallet JSON</p> |
| password | <code>string</code> | <p>Password to decrypt the wallet</p> |

**Example**  
```js
// Import from encrypted wallet backup
const walletBackup = { ... }; // encrypted wallet JSON
await wallet.importUniversalWalletJSON(walletBackup, 'mypassword');
```
<a name="IWallet.exportDocuments"></a>

### IWallet.exportDocuments(params) ⇒ <code>Promise.&lt;any&gt;</code>
<p>Exports specified documents as an encrypted JSON (test)</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>Promise.&lt;any&gt;</code> - <p>Encrypted wallet JSON</p>  

| Param | Type | Description |
| --- | --- | --- |
| params | <code>Object</code> | <p>Export parameters</p> |
| params.documents | <code>Array.&lt;any&gt;</code> | <p>Documents to export</p> |
| params.password | <code>string</code> | <p>Password for encryption</p> |

<a name="IWallet.exportUniversalWalletJSON"></a>

### IWallet.exportUniversalWalletJSON(password) ⇒ <code>any</code>
<p>Exports the entire wallet as an encrypted Universal Wallet 2020 JSON</p>

**Kind**: static method of [<code>IWallet</code>](#IWallet)  
**Returns**: <code>any</code> - <p>Encrypted Universal Wallet JSON representation</p>  
**See**: [https://w3c-ccg.github.io/universal-wallet-interop-spec/](https://w3c-ccg.github.io/universal-wallet-interop-spec/)  

| Param | Type | Description |
| --- | --- | --- |
| password | <code>string</code> | <p>Password for encryption</p> |

**Example**  
```js
// Create encrypted backup of entire wallet
const backup = await wallet.exportUniversalWalletJSON('mypassword');
// Save backup to file or cloud storage
```
<a name="Goals"></a>

## Goals ⇒
**Kind**: global variable  
**Returns**: <p>OOB message to start a wallet to wallet verification flow
The holder will scan it as QR code and should have the context to start the verification flow</p>  
<a name="dockDocumentNetworkResolver"></a>

## dockDocumentNetworkResolver
<p>Given an Api URL, resolve the network ID
For now it will be applied for creds and certs
It can be extended to resolve other external URLs</p>

**Kind**: global variable  
<a name="MessageTypes"></a>

## MessageTypes
<p>DIDComm Message helpers
Check https://identity.foundation/didcomm-messaging/spec/#out-of-band-messages for more details</p>

**Kind**: global constant  
<a name="isValid"></a>

## isValid(credential) ⇒ <code>Promise.&lt;Object&gt;</code>
<p>Uses Dock SDK to verify a credential</p>

**Kind**: global function  
**Returns**: <code>Promise.&lt;Object&gt;</code> - <p>Verification result with status and optional error/warning messages</p>  

| Param |
| --- |
| credential | 

<a name="syncCredentialStatus"></a>

## syncCredentialStatus(param0) ⇒
<p>Fetch credential status from the chain and update the wallet
Store a new document <credentialId>#status in the wallet
Returns a list of CredentialStatusDocument</p>

**Kind**: global function  
**Returns**: <p>CredentialStatusDocument[]</p>  

| Param |
| --- |
| param0 | 

<a name="removeCredential"></a>

## removeCredential(param0) ⇒ <code>Promise.&lt;void&gt;</code>
<p>Removes a credential and its related documents from the wallet</p>

**Kind**: global function  

| Param |
| --- |
| param0 | 

<a name="buildRequestVerifiablePresentationMessage"></a>

## buildRequestVerifiablePresentationMessage()
<p>Sender: Verifier
OOB message to request a verifiable presentation from the holder</p>

**Kind**: global function  
<a name="buildAckWalletToWalletVerificationMessage"></a>

## buildAckWalletToWalletVerificationMessage()
<p>Sender: Holder
Start a wallet to wallet verification flow</p>

**Kind**: global function  
<a name="buildVerifiablePresentationMessage"></a>

## buildVerifiablePresentationMessage()
<p>Sender: Holder
Send a verifiable presentation to the verifier</p>

**Kind**: global function  
<a name="buildVerifiablePresentationAckMessage"></a>

## buildVerifiablePresentationAckMessage()
<p>Sender: Verifier
Sends an the presentation result to the holder</p>

**Kind**: global function  
<a name="handleBlockchainNetworkChange"></a>

## handleBlockchainNetworkChange()
<p>Update existing substrate network connection
Compare connected substrate connection with the current walle network
Disconnect and Establish a new connection if the network is different</p>

**Kind**: global function  
<a name="WalletStatus"></a>

## WalletStatus : <code>&#x27;closed&#x27;</code> \| <code>&#x27;loading&#x27;</code> \| <code>&#x27;ready&#x27;</code> \| <code>&#x27;error&#x27;</code>
<p>Possible wallet status values</p>

**Kind**: global typedef  
<a name="KeypairType"></a>

## KeypairType : <code>&#x27;sr25519&#x27;</code> \| <code>&#x27;ed25519&#x27;</code> \| <code>&#x27;ecdsa&#x27;</code>
<p>Supported keypair types</p>

**Kind**: global typedef  
