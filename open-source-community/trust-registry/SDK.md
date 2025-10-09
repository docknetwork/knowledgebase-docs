# Trust Registry SDK interaction

[Actions](SDK.md#actions)

[1. Initialize or update Trust Registry](SDK.md#initorupdatetrustregistry)

[2. Set or update schemas metadata](SDK.md#setschemasmetadata)

[3. Suspend issuers](SDK.md#suspendissuers)

[4. Unsuspend issuers](SDK.md#unsuspendissuers)

[5. Update delegated issuers](SDK.md#updatedelegatedissuers)

[Requests](SDK.md#requests)

[- Trust Registry identifiers](SDK.md#trust-registry-identifiers)

[- Schema metadata identifiers](SDK.md#schema-metadata-identifiers)

[- Trust Registry information](SDK.md#trust-registry-information)

[- Schema metadata information](SDK.md#schema-metadata-information)

## Actions

1. **InitOrUpdateTrustRegistry**
   *   **Description**: Initializes or updates a trust registry with the provided parameters.

       | Parameter    | Type            | Description                                              |
       | ------------ | --------------- | -------------------------------------------------------- |
       | registryId   | TrustRegistryId | Identifier for the trust registry.                       |
       | name         | String          | Name of the trust registry.                              |
       | govFramework | Bytes           | Government framework associated with the trust registry. |
       | nonce        | u32             | Nonce of the caller DID.                                 |
   *   **Example:**

       ```jsx
       const trustRegistryId = randomAsHex(32);
       await dock.trustRegistry.initOrUpdate(
         convenerDID,
         trustRegistryId,
         "My Trust Registry",
         '{"name":"Sample Government Framework","description":"This is a sample government framework for use in a trust registry.","authority":"Sample Government Authority","contact":{"name":"John Doe","email":"johndoe@example.com","phone":"+1234567890"},"policies":[{"name":"Identity Verification Policy","description":"Policy for verifying the identity of participants in the trust registry.","requirements":["Government-issued identification","Biometric verification"]},{"name":"Data Protection Policy","description":"Policy for protecting the data stored in the trust registry.","requirements":["Encryption of sensitive data","Regular security audits"]},{"name":"Compliance Policy","description":"Policy for ensuring compliance with relevant regulations and standards.","requirements":["Adherence to GDPR regulations","ISO 27001 certification"]}]}',
         convenerPair,
         dock
       );
       ```
2. **SetSchemasMetadata**
   *   **Description**: Sets the schemas metadata for a trust registry.

       | Parameter  | Type                   | Description                        |
       | ---------- | ---------------------- | ---------------------------------- |
       | registryId | TrustRegistryId        | Identifier for the trust registry. |
       | schemas    | UnboundedSchemasUpdate | Schemas to be updated.             |
       | nonce      | u32                    | Nonce of the caller DID.           |
   *   **Example:**

       ```jsx
       const issuers = new BTreeMap(dock.api.registry, 'Issuer', 'VerificationPrices');
       const issuerPrices = new BTreeMap(dock.api.registry, 'String', 'VerificationPrice');
       issuerPrices.set("DOCK", 10e6); // 10 DOCK tokens with 6 decimals of precision
       issuers.set(issuerDID, issuerPrices);

       const verifiers = new BTreeSet(dock.api.registry, 'Verifier');
       verifiers.add(verifierDID);

       const schemas = new BTreeMap(dock.api.registry, 'Verifier');
       schemas.set(schemaId, {
         Set: {
           issuers,
           verifiers,
         },
       });

       await dock.trustRegistry.setSchemasMetadata(
         convenerDID,
         trustRegistryId,
         { Modify: schemas },
         convenerPair,
         dock
       );
       ```
3. **SuspendIssuers**
   *   **Description**: Suspends issuers within a trust registry.

       | Parameter  | Type            | Description                        |
       | ---------- | --------------- | ---------------------------------- |
       | registryId | TrustRegistryId | Identifier for the trust registry. |
       | issuers    | BTreeSet        | Set of issuers to be suspended.    |
       | nonce      | u32             | Nonce of the caller DID.           |
   *   **Example:**

       ```jsx
       await dock.trustRegistry.suspendIssuers(
         convenerDID,
         trustRegistryId,
         [issuerDID, issuerDID2],
         convenerPair,
         dock
       );
       ```
4. **UnsuspendIssuers**
   *   **Description**: Unsuspends previously suspended issuers within a trust registry.

       | Parameter  | Type            | Description                        |
       | ---------- | --------------- | ---------------------------------- |
       | registryId | TrustRegistryId | Identifier for the trust registry. |
       | issuers    | BTreeSet        | Set of issuers to be unsuspended.  |
       | nonce      | u32             | Nonce of the caller DID.           |
   *   **Example:**

       ```jsx
       await dock.trustRegistry.unsuspendIssuers(
         convenerDID,
         trustRegistryId,
         [issuerDID],
         convenerPair,
         dock
       );
       ```
5. **UpdateDelegatedIssuers**
   *   **Description**: Updates delegated issuers within a trust registry.

       | Parameter  | Type                     | Description                        |
       | ---------- | ------------------------ | ---------------------------------- |
       | registryId | TrustRegistryId          | Identifier for the trust registry. |
       | delegated  | UnboundedDelegatedUpdate | Delegated issuers to be updated.   |
       | nonce      | u32                      | Nonce of the caller DID.           |
   *   **Example:**

       ```jsx
       const issuers = new BTreeSet(dock.api.registry);
       issuers.add(delegatedIssuer);

       await dock.trustRegistry.updateDelegatedIssuers(
         issuerDID,
         trustRegistryId,
         { Set: issuers },
         issuerPair,
         dock
       );
       ```

## Requests

### **Trust registry identifiers**

1. **Fetch all Trust Registry identifiers by Verifier**:

* Request: **`dock.api.query.trustRegistry.verifiersTrustRegistries(verifierDID)`**
* Response: Returns trust registries where the specified verifier exists.

2. **Fetch all Trust Registry identifiers by Issuer**:

* Request: **`dock.api.query.trustRegistry.issuersTrustRegistries(issuerDID)`**
* Response: Returns trust registries where the specified issuer exists.

3. **Request Trust Registry identifiers by Issuers**:

* Request: **`dock.trustRegistry.registriesIds({ issuers: { AnyOf: [issuerDID] } })`**
* Response: Returns information about trust registries where the specified issuer exists.

4. **Request Trust Registry identifiers by Issuers or Verifiers**:

* Request: **`dock.trustRegistry.registriesIds({ issuersOrVerifiers: { AnyOf: [verifierDID, issuerDID] } })`**
* Response: Returns information about trust registries where the specified issuer or verifier exists.

5. **Request Trust Registry identifiers by schema identifiers**:

* Request: **`dock.trustRegistry.registriesIds({ schemaIds: { AnyOf: [schemaId] } })`**
* Response: Returns information about trust registries associated with the specified schema.

### **Schema metadata identifiers**

1. **Fetch all schema metadata identifiers in the Trust Registry with the supplied id by Verifier**:

* Request: **`dock.api.query.trustRegistry.trustRegistryVerifierSchemas(registryID, verifierDID)`**
* Response: Returns trust registries where the specified verifier exists.

2. **Fetch all schema metadata identifiers in the Trust Registry with the supplied id by Issuer**:

* Request: **`dock.api.query.trustRegistry.trustRegistryIssuerSchemas(registryID, issuerDID)`**
* Response: Returns trust registries where the specified issuer exists.

3. **Request schema metadata identifiers by Issuers**:

* Request: **`dock.trustRegistry.registrySchemaIds({ issuers: { AnyOf: [issuerDID] } }, registryID)`**
* Response: Returns information about trust registries where the specified issuer exists.

4. **Request schema metadata identifiers by Issuers or Verifiers**:

* Request: **`dock.trustRegistry.registrySchemaIds({ issuersOrVerifiers: { AnyOf: [verifierDID, issuerDID] } }, registryID)`**
* Response: Returns information about trust registries where the specified issuer or verifier exists.

5. **Request schema metadata identifiers by schema identifiers**:

* Request: **`dock.trustRegistry.registrySchemaIds({ schemaIds: { AnyOf: [schemaId] } }, registryID)`**
* Response: Returns information about trust registries associated with the specified schema.

### **Trust registry information**

1. **Request Trust Registry information by Verifiers**:

* Request: **`dock.trustRegistry.registriesInfo({ verifiers: { AnyOf: [verifierDID] } })`**
* Response: Returns information about trust registries where the specified verifier exists.

2. **Request Trust Registry information by Issuers**:

* Request: **`dock.trustRegistry.registriesInfo({ issuers: { AnyOf: [issuerDID] } })`**
* Response: Returns information about trust registries where the specified issuer exists.

3. **Request Trust Registry information by Issuers or Verifiers**:

* Request: **`dock.trustRegistry.registriesInfo({ issuersOrVerifiers: { AnyOf: [verifierDID, issuerDID] } })`**
* Response: Returns information about trust registries where the specified issuer or verifier exists.

4. **Request Trust Registry information by schema identifiers**:

* Request: **`dock.trustRegistry.registriesInfo({ schemaIds: { AnyOf: [schemaId] } })`**
* Response: Returns information about trust registries associated with the specified schema.

### **Schemas metadata**

1. **Request Trust Registry schemas metadata by Verifiers**:

* Request: **`dock.trustRegistry.registrySchemasMetadata({ verifiers: { AnyOf: [verifierDID] } }, registryId)`**
* Response: Returns metadata for all schemas in the given trust registry where the specified verifier exists.

2. **Request Trust Registry schemas metadata by Issuers**:

* Request: **`dock.trustRegistry.registrySchemasMetadata({ issuers: { AnyOf: [issuerDID] } }, registryId)`**
* Response: Returns metadata for all schemas in the given trust registry where the specified issuer exists.

3. **Request Trust Registry schemas metadata by Issuers or Verifiers**:

* Request: **`dock.trustRegistry.registrySchemasMetadata({ issuersOrVerifiers: { AnyOf: [verifierDID, issuerDID] } }, registryId)`**
* Response: Returns metadata for all schemas in the given trust registry where the specified issuer or verifier exists.

4. **Request Trust Registry schemas metadata by schema identifiers**:

* Request: **`dock.trustRegistry.registrySchemasMetadata({ schemaIds: { AnyOf: [schemaId] } }, registryId)`**
* Response: Returns metadata for schemas with supplied identifiers.
