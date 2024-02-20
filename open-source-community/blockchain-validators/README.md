# Blockchain Validators

Validators are in charge of producing blocks (processing transactions) and validating blocks produced by other validators. Validators earn token rewards for participating in the network, these are described in the [emission rewards](../../dock-token/emission-rewards.md) section.

{% hint style="info" %}
Join Dock's [Validator Discord channel](https://discord.gg/kV9ZfsskGy) for additional support and to connect with other Dock validators
{% endhint %}

The nodes currently running the mainnet can be seen at the Dock Network [telemetry](https://telemetry.polkadot.io/#list/Dock%20PoS%20Mainnet). Our fork of the Polkadot-js apps showing block explorer and other tools is[ here](https://fe.dock.io/). You can also check our explorer at [Subscan](https://dock.subscan.io/).

![](https://lh5.googleusercontent.com/YIWtkIq09uYTcCXJ-wUKLakXWV1EeOmjAfJvpNBVxGzy0QNGT47wpS9HYMgnE7Va\_\_iavD1NRPNhbibtKWMjyW2AEqqXiqhxVB36dpbPLP6b8XHQF5EuUJX3dXCXGOL0Ge5E35Qy)

Any cloud provider can be used to run a Dock node cost at minimal expense.

Specifically, the following are required:

1. 1 or 2 publicly accessible machines
2. At least 4 GB of RAM
3. At least several hundred GB of SSD. But keep in mind that the chain is always growing and the validators need to keep the whole chain, thus disk usage should be periodically reviewed and increased if needed.&#x20;
4. Bandwidth of 10 Mbps over WAN

Some familiarity with provisioning machines (either cloud or on-prem) and some familiarity with Linux command line is needed to run the provided scripts to generate keys and deploy node. Dock currently supports Ubuntu 18.04.

There are different requirements to become a validator in the PoS network. More information is available in the following sections.



