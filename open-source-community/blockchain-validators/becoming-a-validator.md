# Becoming a validator

To become a validator, you need to run a full node that can be built from [our source code](https://github.com/docknetwork/dock-substrate) at Github. Make sure to checkout the correct tag. For mainnet, checkout the tag `mainnet` for testnet checkout tag `testnet` . Another thing to note is that we have only built the node on Ubuntu 20.04 and RHEL 8. The chain spec for mainnet is called `knox_raw.json` and can be seen in Github over [here](https://github.com/docknetwork/dock-substrate/blob/master/cspec/knox\_raw.json?raw=true). To build a mainnet node, run

```
cargo build --release --features mainnet
```

Once the node is built you can run it as below.&#x20;

```
./target/release/dock-node --chain-spec=./cspec/knox_raw.json --validator .... and any other arguments
```

_Note the flag_ `--validator` _Anyone running a validator node must use that flag else the node will not act as a validator._

You can also use a docker image from [here](https://hub.docker.com/r/docknetwork/dock-substrate). For mainnet download image with tag `mainnet` , for testnet image with tag `testnet`. When running the container, pass the chain spec

```
docker run -d -p 9944:9944 -p 9933:9933 -p 30333:30333 docknetwork/dock-substrate:mainnet --chain=./cspec/knox_raw.json --validator ... and any other arguments
```

Similarly, for testnet, checkout the tag `testnet` on github and use chain spec `knox_test_raw.json`.&#x20;

There is an ansible script as well to deploy docker node on provisioned machine. [Here is the Readme](https://github.com/docknetwork/dock-substrate/tree/testnet/scripts/ansible) for that.

Once the node is running and syncing, you need to bond tokens to become a validator which can be done through the polkadot-js apps UI [here](https://fe.dock.io/#/explorer). Add Stash and Controller accounts with sufficient balance and then go to the [Staking tab](https://fe.dock.io/#/staking) to set your session key and bond tokens.
