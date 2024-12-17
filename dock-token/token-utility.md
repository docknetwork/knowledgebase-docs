---
hidden: true
---

# Token Utility

The Dock utility token (DOCK) plays a key role in aligning incentives across all of the Dock network’s participants including issuers, validators, token holders, and the Dock Association, and ensures collaboration and growth. The Dock token provides three main utilities in the network:

## 1. Transactions on the Dock Blockchain <a href="#h_0461fee7b2" id="h_0461fee7b2"></a>

Any write operation completed on-chain requires tokens. The amount of tokens varies depending on the resource consumption of that operation including its size, disk usage, and CPU usage. All operations pay a minimum fee called the base fee. Examples of these transactions include:

DIDs (Decentralized Identities)

* Creating DIDs requires tokens.
* Adding keys to DIDs requires tokens. There are different kinds of keys including those for different variations of anonymous credentials and also keys utilizing different schemas.
* Updating keys of DID requires tokens.

Revocation Registries

* Creating a new revocation registry requires tokens. The number of tokens will vary depending on the type of registry and the policy, i.e., how many DIDs control it and how many can revoke the registry.
* Revoking credentials requires tokens. The number of tokens will vary depending on the number of credentials being revoked and the type and policy of the registry.
* Undoing the revocation of credentials also requires tokens. The number of tokens will vary on the same criteria as revocations.

Schema

* Creating schema requires tokens with the amount depending on the schema size. Schemas describe the structure of credentials, e.g., a driver's license credential should have 10 fields including the licensee's name and address. Schemas are shareable among issuers as they do not contain any cryptographic material and thus are created less frequently.

## 2. Validating and Staking <a href="#h_ef19f35a72" id="h_ef19f35a72"></a>

The Dock token provides emission rewards to validators who support the infrastructure of the network and process transactions. Emission rewards are paid to validators as compensation for their services.

In addition, the Dock token is also used to determine validators. To become a validator in the PoS network, the candidate needs to lock tokens ("stake") and can also invite other token holders to lock tokens on their behalf. The network selects validators based on the stake behind them.

## 3. Governance <a href="#h_df72b7d116" id="h_df72b7d116"></a>

The Dock token also plays an important role in ensuring token holders participate in the governance of the network. Major changes to the network are decided by token holders voting on proposals, and the value of each token holder's vote depends on the number of locked tokens and lock duration.
