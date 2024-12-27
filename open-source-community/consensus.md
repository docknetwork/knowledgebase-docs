---
hidden: true
---

# Blockchain consensus

Dock blockchain is built on [Substrate](https://substrate.dev/) and uses the consensus mechanism offered by Substrate which is a _hybrid_ as it separates block production and finality and achieves them through different methods. The finality is achieved through a finality gadget called GRANDPA (**G**HOST-based **R**ecursive **AN**cestor **D**eriving **P**refix **A**greement). It finalizes chains rather than individual blocks and offers provable finality.

The Dock Blockchain network started with a Proof of Authority (PoA) network and therefore the block production algorithm in this phase was Aura, which was transitioned to a Proof of Stake (PoS) consensus.

When Dock transitions into utilizing PoS, the block production algorithm changes from Aura to BABE (**B**lind **A**ssignment for **B**lockchain **E**xtension protocol) which selects a validator for each _slot_ (interval of time) randomly using a VRF (Verifiable Random Function). BABE is similar to IOHK's [Ouroboros Praos](https://eprint.iacr.org/2017/573.pdf).

For development purposes, we will bundle [instant-seal](https://github.com/paritytech/substrate/tree/master/client/consensus/manual-seal) consensus which produces a block as soon as the transaction reaches the node rather than wait for blocks to be produced at a fixed interval. This is helpful when running the SDK against a local node during development.

**Network Explorers**

Two explorers are available to query the Dock blockchain and view usage metrics:

* [Subscan Explorer](https://dock.subscan.io/)
* [DockJS App Explorer](https://fe.dock.io/#/explorer)

When the Dock network transitioned to PoS, a new blockchain was created from genesis and the previous PoA blockchain stopped supporting new transactions. The PoA blockchain is still accessible for historical purposes and hosted separately by Subscan: [Dock PoA Mainnet](https://dock-poa.subscan.io/).
