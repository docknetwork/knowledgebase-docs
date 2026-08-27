# Part 3. Implementation

Before starting, make sure Claude Code (or another tool of your choice) has the configuration file from the Part 1, design from Part 2 and the [knowledgebase](https://github.com/docknetwork/knowledgebase-docs) repo in the working directory. Working from these means it will be easier to get predictable results and less de-bugging will be needed.

### 1. Project setup

A frontend plus a small server-side proxy. The Truvera API keys cannot go in the browser, so every call to the Truvera API goes through the proxy. Add these values to your `.env` file.

```
TRUVERA_API_URL=https://api-testnet.truvera.io
TRUVERA_ISSUER_API_KEY=          # issuance routes
TRUVERA_VERIFIER_API_KEY=        # proof request and result routes
EDV_AUTH_KEY=                    # used by the wallet SDK in the browser
```

The two API keys are the reason the proxy exists. Never use one for both, or the two-party structure set up in Part 1 quietly disappears while everything still appears to work.

The EDV auth key is different. It is used by the wallet SDK in the browser, not by the proxy, so it reaches the client. Checkpoint one assumes it is already in place.

Everything else comes from the `config.json` [configuration file](part-1.-setting-up-in-the-workspace.md#id-7.-write-the-configuration-file).

**For your use case.** One API key per participating account. Everything else is the same.

{% prompt description="Setup prompt" %}
```markdown
I have a working design prototype for a verifiable credentials app, and I want to build the real thing from it.

In this directory:
- The design prototype from Claude Design. Treat it as a visual reference for layout, wording, and the status colour convention. It is not a starting codebase. Its sample data, its stepper, and its Back and Next navigation are walkthrough devices and must not survive into the built app.
- config.json, containing the issuer DID, verifier DID, schema ID and URL, and proof template ID. Use these values exactly and read them from the file at runtime rather than copying them into code. Do not invent IDs.
- The schema URL in config.json is public. Fetch it and match the field names in code exactly.
- The Truvera knowledgebase. Use it for API and SDK details rather than assuming.
Architecture: a frontend plus a small Express proxy. Every Truvera API call goes through the proxy. Issuance routes use the issuer key, proof request and result routes use the verifier key.

Secrets live in .env and never in config.json: TRUVERA_ISSUER_API_KEY, TRUVERA_VERIFIER_API_KEY, and EDV_AUTH_KEY. The two API keys stay server-side. EDV_AUTH_KEY is the exception, it is used by the wallet SDK in the browser, so expose that one to the client.
Build this in four checkpoints. Stop after each one so I can run it.

```
{% endprompt %}

**Done when:** `config.json` and `.env` are both filled in, and everything Claude Code needs to read is in the directory.

### 2. Checkpoint one: the cloud wallet

[Install the wallet SDK ](https://www.npmjs.com/package/@docknetwork/wallet-sdk-web)and initialise the cloud wallet against the EDV using the [auth key](./#from-truvera-support), with passkey: true.

On first use the SDK registers a passkey, derives key material from it through the WebAuthn PRF extension, generates and encrypts a master key, and stores it in the vault. On return visits it is a single biometric prompt. The key material never leaves the browser, and the passkey syncs across the user's devices through iCloud Keychain or Google Password Manager.

Two things to know. Passkey unlock needs Chrome 116+, Safari 18+, or Edge 116+, so check the browser you plan to demo in. And on first enrolment only, the SDK returns a recovery phrase, which is the fallback if the passkey is ever lost. The prototype ignores it. A real deployment has to show it once and tell the holder to keep it, because a lost passkey with no recovery phrase means a lost wallet.

{% prompt description="Cloud wallet prompt" %}
```markdown
Checkpoint one: the cloud wallet.
Install @docknetwork/wallet-sdk-web and initialise the cloud wallet against the EDV with passkey: true, using the EDV auth key in the environment.

Show the wallet's DID on screen once it is ready. On first enrolment, show the recovery phrase the SDK returns, once, framed as a fallback rather than a login step. 
Done when I can create a wallet with a passkey and see its DID.
```
{% endprompt %}

**Done when:** the wallet panel shows the wallet's DID on screen. That DID is what the next checkpoint issues to.

### 3. Checkpoint two: issuance

Issuance to a cloud wallet uses OID4VCI, which is a two-step call on the backend followed by one line in the wallet.

The proxy creates an issuer with `POST /openid/issuers`, passing the issuer DID, the schema as context, and the subject data. It then creates an offer with `POST /openid/credential-offers`, which returns an `offerUrl`. That URL goes back to the app, and the wallet claims the credential with `wallet.addCredential(offerUrl)`.

The holder never sees any of this. Onboarding completes and the badge is there.

Three things in the issuer call:

* **subject.id is the wallet DID from checkpoint one**, where you know it. The offer is what delivers the credential, so this is not what makes issuance work, but it is what records who the credential is about.
* **Algorithm is dockbbs**, which is what makes selective disclosure possible at verification time.
* **revocation: true**, which is all that is needed to make the badge revocable. The API creates and manages the registry itself, so there is nothing to set up beforehand. A credential issued without this can never be revoked.

**For your use case.** Same two calls, different subject data. The schema and the field values change, the structure does not.

{% prompt description="Issuance prompt" %}
```markdown
The last step of onboarding issues a {{CREDENTIAL}} to the wallet over OID4VCI.

On the proxy, using the issuer key:
- POST /openid/issuers with the issuer DID from handoff.md, the schema as context, and the subject data. Set subject.id to the wallet DID from checkpoint one, algorithm to dockbbs, and revocation to true.
- POST /openid/credential-offers, which returns an offerUrl. Return that to the app.

In the wallet, claim it with wallet.addCredential(offerUrl).
The holder does not see any of this, they see the credential appear.
Done when completing onboarding puts the credential in the wallet without a reload.

```
{% endprompt %}

**Done when:** completing onboarding puts the badge in the wallet without a page reload.

### 4. Checkpoint three: verification

On the event registration page, create a proof request from the template created in Part 1, using the verifier key. The request comes back as a URL, and the "present credential" button is a deeplink carrying it. Following it opens the wallet with the request already loaded.

The result does not come back to the page on its own. The verifier reads it from `GET /proof-templates/{id}/history`, which returns recent presentations against that template. Both calls go through the proxy on the verifier key.

Poll that endpoint from the moment the request is created, and take the newest entry that postdates it. With one holder presenting, that is unambiguous. In production you would use a webhook and match on the request id rather than on recency, but a webhook needs a publicly reachable URL, which is not worth setting up for a prototype.

Display the fields that were actually received, not a success message. Seeing employer and status arrive, with no name and no employee ID, is what makes the point about disclosing only what is needed.

The same request also works as a QR, for holders using the mobile wallet. Same template, same deeplink, rendered differently.

**For your use case.** Same two calls against a different template. If your verifier needs to check a value rather than just its presence, that constraint lives in the template from 4.5, not in this code.

{% prompt description="Verification prompt" %}
```markdown
Checkpoint three: verification.
On {{VERIFIER_SURFACE}}, create a proof request from the template in handoff.md using the verifier key. The request URL becomes a deeplink on the "present credential" button, which opens the wallet with the request already loaded. Render the same URL as a QR code alongside it, for holders on the mobile wallet.
Results do not arrive on their own. Add a second proxy route, also on the verifier key, that reads GET /proof-templates/{id}/history from the Truvera API. Poll it from the moment the request is created and take the newest entry that postdates it. Do not build webhook handling.
Display the attribute values actually received, not a success message. The template requests only {{DISCLOSED_FIELDS}}, and the page should make clear what it did not receive.
Done when the holder can {{VERIFIER_GOAL}} by presenting the credential.
```
{% endprompt %}

\
**Done when:** the employee registers for the event using the badge, and the page shows what it verified.

### 5. Checkpoint four: revocation

Nothing to build on the issuer side. Revoke the badge from the Truvera Workspace, where the issued credentials are already listed.

Two things need to happen in the code, and they are on different sides.

In the wallet, the card status pill flips to revoked, and following the deeplink produces a clear error rather than a presentation. The wallet will not build a presentation from a revoked credential, so this is where the refusal actually happens and where the holder finds out.

On the verifier's page, nothing arrives. There is no failure to display, because a presentation was never made. The page needs a timeout and a neutral message saying no credential was presented, rather than polling indefinitely.

That split is worth pointing at when demonstrating this. The verifier learns that it did not get what it asked for, and nothing else. It is not told the credential exists, or that it was revoked, or why.

**For your use case.** This is the checkpoint to drop if you are running short. Everything before it is a working prototype on its own.

{% prompt description="Revocation prompt" %}
```markdown
I revoke the credential from the Truvera Workspace. Nothing to build on the issuer
side.

In the wallet: the card status pill flips to revoked, and following the verification deeplink fails with a clear error. The wallet cannot build a presentation from arevoked credential.

On {{VERIFIER_SURFACE}}: no presentation ever arrives, so there is no failure result to read. Give the polling a timeout and a neutral message saying no credential was presented. Do not invent a failure state that the API does not return.

Done when the same credential that granted access produces an error in the wallet,
and the verifier page gives up cleanly.
```
{% endprompt %}

**Done when:** the same badge that granted access a minute ago produces an error in the wallet, and the registration page gives up cleanly.



<br>
