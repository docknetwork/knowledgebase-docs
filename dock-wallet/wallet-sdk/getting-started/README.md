# Getting Started

This guide walks you through the process of setting up the Dock Wallet SDK, creating a wallet, managing decentralized identifiers (DIDs), adding credentials, and verifying them.

## Installation

To start, you need to install the necessary packages for the wallet SDK and the data store. Open your terminal and run the following command:

```bash
yarn add @docknetwork/wallet-sdk-core @docknetwork/wallet-sdk-data-store-typeorm
```

The `@docknetwork/wallet-sdk-core` provides the core wallet functionality, while `@docknetwork/wallet-sdk-data-store-typeorm` handles data persistence using a local SQLite database.

## Usage Example

### 1. Initialize the Data Store

Before creating a wallet, you need to set up a data store to manage the persistence of wallet data such as DIDs and credentials. Here’s how to create a data store:

```ts
import {createDataStore} from '@docknetwork/wallet-sdk-data-store-typeorm/lib';

const dataStore = await createDataStore({
  databasePath: 'dock-wallet',
  dbType: 'sqlite',
  defaultNetwork: 'testnet',
});
```

This code initializes a SQLite database to store wallet data. You can adjust the `databasePath` and `defaultNetwork` based on your needs.

If you want to use the cloud wallet solution, please refer to the [Cloud Wallet Documentation](../../../developer-documentation/wallet-sdk/cloud-wallet.md) for detailed instructions and configuration options.

### 2. Create a New Wallet

Once the data store is set up, you can create a wallet. The wallet will act as a container for managing your documents, DIDs, and credentials.

```ts
import {createWallet} from '@docknetwork/wallet-sdk-core/lib/wallet';

const wallet = await createWallet({
  dataStore,
});
```

This creates a new wallet instance that links to the previously created data store.

### 3. Fetch your DIDs

DIDs (Decentralized Identifiers) are a key part of self-sovereign identity. When a wallet is created, a default DID is automatically generated. You can retrieve and view the default DID associated with your wallet using the following code:

```ts
// The didProvider is used to manage DIDs
import {createDIDProvider} from '@docknetwork/wallet-sdk-core/src/did-provider';

const didProvider = createDIDProvider({wallet});
const defaultDID = await didProvider.getDefaultDID();

console.log(defaultDID);

// Example output: did:key:z6MkrcDhePAr5J44Htf6CLSQpZFUGGec4kPVVmERaY9Seijw
```

### 4. Add a Credential to the Wallet

Once you have a wallet and a DID, you can start managing credentials. In this example, you will import a credential from a URL into the wallet.

```ts
import {createCredentialProvider} from '@docknetwork/wallet-sdk-core/src/credential-provider';

const credentialProvider = createCredentialProvider({
  wallet, // Pass the wallet instance
});

await credentialProvider.importCredentialFromURI({
  uri: 'https://creds-testnet.dock.io/8489dc69b69a70c97646ad9b4f256acaddb57762b5a6f661f0c9dae3b7f72ea6', // Credential URL
  getAuthCode: async () => {
    // You can implement your own UI to get the password
    // For this example it will be hardcoded
    return 'test';
  },
});

const credentials = await credentialProvider.getCredentials(); // Retrieve all imported credentials

console.log(credentials);
```

In this example, the credential is fetched from a specified URI and imported into the wallet. The `getAuthCode` function is used to handle any authentication, such as providing a password if required.

### 5. Verify a Credential

The Dock Wallet SDK provides built-in functionality for verifying credentials. This is especially useful when interacting with third parties who need to verify your credentials. The verification controller manages this process. Below is an example of how to start a verification, select which credentials to reveal, create a presentation, and submit it for verification.

```ts
const {
  createVerificationController,
} = require('@docknetwork/wallet-sdk-core/src/verification-controller');

const controller = createVerificationController({
  wallet, // Your wallet instance
});

await controller.start({
  template: 'https://creds-testnet.dock.io/proof/1fd8c457-f805-4117-9469-67b3e8c70fff', // Proof request template from the verifier
});

controller.selectedCredentials.set(credential.id, {
  credential: credential, // Specify the credential you want to present
  attributesToReveal: ['credentialSubject.name'] // Choose which attributes to reveal
});

const presentation = await controller.createPresentation(); // Create a presentation based on the selected credentials

const verificationResponse = await controller.submitPresentation(presentation); // Submit the presentation for verification

console.log(verificationResponse);
```

In this example, the verification process starts by fetching a proof request template. After selecting the credentials and specifying which attributes to reveal, the wallet creates a verifiable presentation. The presentation is then submitted, and the verifier responds with a verification result.