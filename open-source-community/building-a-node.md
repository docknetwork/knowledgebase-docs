---
hidden: true
---

# Building a node

The blockchain node is built on [Substrate](https://substrate.dev/) and can be found on [Github](https://github.com/docknetwork/dock-substrate). The node can either be built from the source or it can be run with Docker using the [Docker images](https://hub.docker.com/repository/docker/docknetwork/dock-substrate) at Dockerhub.

### Using with Substrate Sidecar

When using with [substrate-api-sidecar](https://github.com/paritytech/substrate-api-sidecar), you need to use [our custom types](https://github.com/docknetwork/dock-substrate/blob/master/types.json), refer to [this section](https://github.com/paritytech/substrate-api-sidecar#custom-substrate-types) of sidecar documentation for more details.

Steps to run Substrate Sidecar

1. Download or clone [sidecar](https://github.com/paritytech/substrate-api-sidecar) version [8.0.3](https://github.com/paritytech/substrate-api-sidecar/releases/tag/v8.0.3) or above.
2. Download or clone the [types package](https://github.com/docknetwork/node-types).
3. Sidecar must be aware of which node to connect to through websocket and which types to use. For that, 2 variables need to be set.
   1. `SAS_SUBSTRATE_WS_URL` to specify where is the node. If using our hosted mainnet node, set it to [wss://mainnet-node.dock.io](wss://mainnet-node.dock.io/), otherwise set it to point to the websocket endpoint of your node. If running a local node with websockets at port 9944, you don't need to set it.
   2. `SAS_SUBSTRATE_TYPES_BUNDLE` to specify our custom types from the above types package. This needs to point to the file system path of the `index.js` file of the above package, eg if the types package was downloaded at the location `/home/Downloads/node-types` then this variable should be set to `/home/Downloads/node-types/src/index.js`.
4. Go to the sidecar directory now.
5.  You can either above 2 variables in the env file for Sidecar or you can run sidecar as

    `SAS_SUBSTRATE_TYPES_BUNDLE=<path to index.js> SAS_SUBSTRATE_WS_URL=<websocket endpoint> yarn dev`
