# Account Setup

Substrate's staking pallet introduces account abstractions that help keep funds as secure as possible. A key pair can represent an account and control funds, like normal accounts that you would expect from other blockchains. In the context of Substrate's Balances pallet, these accounts must have a minimum amount (a "minimal balance") to exist in storage. These abstractions are Stash, Controller, and Session:

**Stash Keys**: a Stash account is meant to hold large amounts of funds. Its private key should be as secure as possible in a cold wallet. The Stash keys are the public/private key pair that defines a Stash account.

This account is like a "savings account" in that you should not make frequent transactions from it. Therefore, its private key should be treated with the utmost security, for example protected in a safe or layers of hardware security. Since the Stash key is kept offline, it designates a Controller account to make non-spending decisions with the weight of the Stash account's funds. It can also designate a Proxy account to vote in governance on its behalf.

**Controller Keys**: a Controller account signals choices on behalf of the Stash account, like payout preferences, but should only hold a minimal amount of funds to pay transaction fees. Its private key should be secure as it can affect validator settings, but will be used somewhat regularly for validator maintenance.

In the context of NPoS, the Controller key will signal one's intent to validate or nominate. The Controller key is used to set preferences like the rewards destination and, in the case of validators, to set their Session keys. The Controller account only needs to pay transaction fees, so it only needs a minimal amount of funds.

Since the Stash key is kept offline, it designates a Controller account to make non-spending decisions with the weight of the Stash account's funds. It can also designate a Proxy account to vote in governance on its behalf. The Controller key can never be used to spend funds from its Stash account. However, actions taken by the Controller can result in slashing, so it should still be well secured.\


**Session Keys**: these are "hot" keys kept in the validator client and used for signing certain validator operations. They should never hold funds.&#x20;

Set the Stash and Controller accounts by going to [https://fe.dock.io/#/staking/actions](https://fe.dock.io/#/staking/actions).\


