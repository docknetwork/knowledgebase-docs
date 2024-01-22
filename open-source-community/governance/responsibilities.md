# Responsibilities

### Actors

The governance framework describes the different actors in the network:

* **Validators** process transactions, produce blocks (by putting transactions in blocks), and finalize them; they also validate blocks produced by other validators. The maximum number of validators that validate concurrently is 50 and they are selected by the network based on the amount of stake they hold.
* **Nominators** select validators they would like to process transactions, produce blocks and validate transactions. They do so by staking Dock tokens.
* The **Technical Committee** provides technical guidance to the network and also fast-tracks any urgent technical proposals.
* The **Governing Council** is responsible for ensuring the optimal performance of the network. It does so by proposing source code upgrades, enforcing and upgrading the governance framework, selecting the Technical Committee, rewarding good actors and punishing bad actors, and allocating the Treasury.

### Network Configuration

Due to the nature of the Dock chain (built on Substrate), the chain's configuration can be changed by raising proposals that are voted on by the council or by the token holder. These configuration parameters include the core operational parameters like maximum block size, maximum block weight, block time, minimum transaction fee, etc., or economic parameters like block rewards, penalties for misbehavior, Treasury share and application-level configuration like revocation policy.&#x20;

### Features

As with configuration, features can be added or removed through proposals and voting. Some example features are the consensus algorithm (NPoS with BABE) or the addition of privacy enhancing blind signatures, for example. Application-level features such as DID authorization and more flexible revocation policies can also be proposed and managed through governance.

### Rewards and Punishments

The network rewards participation for actions such as block production and reporting bad behavior, and punishes bad behavior such as validators being offline, accepting invalid transactions, producing bad blocks, or any kind of equivocation. The conditions of these rewards and penalties are defined by the governance. As an example, the network will emit at most a fixed amount of tokens each year and this amount will decrease each year. For more details on the economics, refer to the [token economics section](broken-reference).

### Treasury Management

The network will periodically emit tokens for about 25 years with a decreasing number each year to incentivize early participation. These tokens are called emission rewards and are distributed among the validators and the Treasury. Sixty percent of the emission rewards and the penalties applied to bad actors will go to the Treasury. The Treasury will fund the ongoing development and maintenance of the network. It also rewards efforts to increase network adoption such as; building apps using the Dock SDK, writing tutorials, implementing the client SDK in other languages, etc. The Treasury is controlled by the Dock Association Council who will vote before any funds can be withdrawn.&#x20;
