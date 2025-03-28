# Biometric Plugin

## Purpose

The biometrics plugin provides a way to perform credential verification using the user's biometric data. It is useful to guarantee that only the biometric holder can perform the verification.

## How to trigger a biometric verification

To trigger a biometric verification, you need to use a verification template that asks for the biometric attributes. Check the following example:

```json
{
  "id": "Credential 1",
  "name": "Forsur Verification - Biometrics Enrollment",
  "purpose": "Forsur wants to verify the ownership of - Biometrics Enrollment and the validity of the Biometrics Credentials.",
  "constraints": {
    "fields": [
      {
        "path": ["$.credentialSubject.id"]
      },
      {
        "path": ["$.credentialSubject.biometric.id"]
      },
      {
        "path": ["$.credentialSubject.biometric.created"]
      },
      {
        "path": [
          "$.issuer.id",
          "$.issuer",
          "$.vc.issuer.id",
          "$.vc.issuer",
          "$.iss"
        ],
        "filter": {
          "const": "did:dock:5HLbQLSmirNuZVRsdWKbsgdajw9QTGzSFJABSVzMT5EBj5sb"
        },
        "predicate": "required"
      }
    ]
  }
}
```

The presence of the following fields should trigger the biometric check:

```json
{
  "path": ["$.credentialSubject.biometric.id"]
},
{
  "path": ["$.credentialSubject.biometric.created"]
}
```

## How to enable the biometric plugin in the wallet

To enable the biometric plugin in a white-label wallet, you need to edit the following file src/wallet-sdk-configs.ts and add your configuration:

```typescript
import { BiometricsPluginConfigs } from "@docknetwork/wallet-sdk-react-native/lib/default-biometrics-plugin";
export const biometricsPluginConfigs: BiometricsPluginConfigs = {
  enrollmentCredentialType: "ForSurBiometricEnrollment",
  biometricMatchCredentialType: "ForSurBiometric",
  issuerConfigs: [
    {
      networkId: "testnet or mainnet",
      did: "<The issuer DID>",
      apiKey:
        "<CERTS-API-KEY>",
      apiUrl: "https://api-testnet.dock.io or https://api.dock.io",
    },
  ],
};

```

## Credential expiration

Credential expiration allows the biometric service provider to specify a maximum length to the validity of a biometric check credential. If the verifier wants to force a refresh of the biometric check more frequently, the verifier can check the credential creation timestamp during verification to ensure it’s within their business rules.

## Credential types

This plugin uses two types of credentials to perform the biometric verification:

* Enrollment Credential: This optional credential contains the biometric data of the user. The biometric data is stored in the credential subject field and will be used to perform the biometric match.
* Biometric Match Credential: This credential is issued by the biometric plugin after the biometric match. It contains the biometric ID, the issuer, and the creation date. The verifier can use this credential to check if the biometric match was performed recently and by the same issuer, and it will not contain any biometric data.

## How to bind a biometric to a credential

Before issuing a credential, the issuer may request to verify the biometric check credential. If a valid credential does not exist, the wallet will trigger the biometric plugin to confirm the biometric and issue a credential.

The biometric check credential needs a unique binding ID that can only be generated by that specific user. The issuer can then include in the primary credential, the biometric ID and biometric issuer as attributes that bind that credential to that holder's biometric.

At the time of verification, the verifier can request the biometric check credential along with the primary credential. If the biometric check credential is recent enough, from the same issuer, and contains the same biometric ID, then the verifier can know it is the same holder presenting the credential.

The biometric ID should not contain the user's actual biometric information. When enrolling a holder in the biometric service, it might be useful to issue an enrolment credential containing the biometric template, the generated biometric ID and any other needed information to identify a returning user. This credential can be verified to get the user's information before checking their biometric. By storing this information with the holder, it avoids the biometric service having to store that PII outside of the control of the holder. The holder should only share a biometric enrollment credential with the biometric service that issued it.

## Using the Biometric Service Plugin

* Create a [Dock API key](../../workspace/creating-api-keys-and-webhook-endpoints.md)
* Wrap the Dock API in your mobile API (which is usually protected with an app username / password)
* When a specific install does a biometric check, call your mobile API to issue a biometric credential
  * The biometric binding nested attributes in the primary credential should include the ecosystem and biometric issuer alongside the biometric ID
  * Your mobile API calls the Dock API to do issuance to the DID
    * In order to use the ecosystem definition of the credentials, the Dock API should be used to query the ecosystem that is found in the credential for the “\*biometric check” schema
    * Mobile API should include the DID that the credential is pushed to
    * This allows the biometric check credential to be managed in the ecosystem where other participants can rely on it and VPI can be enforced
* Biometric Service Plugin monitors credentials received. When a new biometric check credential is received, old ones can be deleted from wallet storage.
* If biometric data should not leave the device, then the biometric service provider plugin can do a local verification of the biometric enrollment credential using the credential SDK. The biometric enrollment credential is managed independent from the ecosystem, as it should only be verified by the biometric provider.

## Adding a custom biometric provider

Adding a custom biometric provider will require the development of the plugin following the interface defined at [packages/react-native/lib/default-biometrics-plugin.ts](https://github.com/docknetwork/react-native-sdk/blob/master/packages/react-native/lib/default-biometrics-plugin.ts). The plugin should implement the following methods:

* hasProofOfBiometrics: Checks if the verification template is asking for biometric attributes.
* enrollBiometrics: Enrolls the biometric data.
* matchBiometrics: Performs the biometric match and if it is valid, returns a biometric match credential. It will try to reuse an existing biometric match credential if it is still valid, otherwise it will remove the expired credential and issue a new one.
