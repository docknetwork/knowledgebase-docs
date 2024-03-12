# Session Keys

## This is a test edit that we need to revert.

You need to tell the chain your Session keys by signing and submitting an extrinsic. This is what associates your validator node with your Controller account on Dock.

**Option 1: DockJS APP**

You can generate your Session keys in the client via the [DockJS App](http://fe.dock.io/). If you are doing this, make sure that you have the DockJS-Apps explorer attached to your validator node. You can configure the apps dashboard to connect to the endpoint of your validator in the Settings tab. If you are connected to a default endpoint hosted by Dock Labs, you will not be able to use this method since making RPC requests to this node would effect the local keystore hosted on a public node and you want to make sure you are interacting with the keystore for your node.

Once you have connected to your node, the easiest way to set session keys for your node is by calling the author\_rotateKeys RPC request to create new keys in your validator's keystore. Navigate to Toolbox tab and select RPC Calls then select the author > rotateKeys() option and remember to save the output that you get back for a later step.\\

**Option 2: CLI**

If you are on a remote server, it is easier to run this command on the same machine (while the node is running with the default HTTP RPC port configured): `curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "author_rotateKeys", "params":[]}' http://localhost:9933`

The output will have a hex-encoded "result" field. The result is the concatenation of the four public keys. Save this result for a later step.

You can restart your node at this point.

### Submitting the setKeys Transaction

You need to tell the chain your Session keys by signing and submitting an extrinsic. This is what associates your validator with your Controller account.

Go to Staking > Account Actions, and click "Set Session Key" on the bonding account you generated earlier. Enter the output from author\_rotateKeys in the field and click "Set Session Key".

`staking-change-sessionstaking-session-result`\\

Submit this extrinsic and you are now ready to start validating.\\

### Validate

To verify that your node is live and synchronized, head to Telemetry and find your node. Note that this will show all nodes on the Dock network, which is why it is important to select a unique name!

If everything looks good, go ahead and click on "Validate" in Dock UI.\\

dashboard validatedashboard validate\\

Payment preferences - You can specify the percentage of the rewards that will get paid to you. The remaining will be split among your nominators.

Click "Validate".

If you go to the "Staking" tab, you will see a list of active validators currently running on the network. At the top of the page, it shows the number of validator slots that are available as well as the number of nodes that have signaled their intention to be a validator. You can go to the "Waiting" tab to double check to see whether your node is listed there.

The validator set is refreshed every era. In the next era, if there is a slot available and your node is selected to join the validator set, your node will become an active validator. Until then, it will remain in the waiting queue. If your validator is not selected to become part of the validator set, it will remain in the waiting queue until it is. There is no need to re-start if you are not selected for the validator set in a particular era. However, it may be necessary to increase the number of DOCK staked or seek out nominators for your validator in order to join the validator set.

Congratulations! If you have followed all of these steps, and been selected to be a part of the validator set, you are now running a Dock validator! \\
