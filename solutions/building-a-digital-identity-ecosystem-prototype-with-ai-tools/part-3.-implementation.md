# Part 3. Implementation

Before starting, make sure Claude Code (or another tool of your choice) has the configuration file from the Part 1, design from Part 2 and the [knowledgebase](https://github.com/docknetwork/knowledgebase-docs) repo in the working directory. Working from these means it will be easier to get predictable results and less de-bugging will be needed.

### 1. Project setup

A frontend plus a small server-side proxy. The Truvera API keys cannot go in the browser, so every call to the Truvera API goes through the proxy.



```
TRUVERA_API_URL=https://api-testnet.truvera.io
TRUVERA_ISSUER_API_KEY=          # issuance routes
TRUVERA_VERIFIER_API_KEY=        # proof request and result routes
EDV_AUTH_KEY=                    # used by the wallet SDK in the browser
```

The two API keys are the reason the proxy exists. Never use one for both, or the two-party structure set up in Part 1 quietly disappears while everything still appears to work.

The EDV auth key is different. It is used by the wallet SDK in the browser, not by the proxy, so it reaches the client. Checkpoint one assumes it is already in place.

Everything else comes from the configuration file.&#x20;
