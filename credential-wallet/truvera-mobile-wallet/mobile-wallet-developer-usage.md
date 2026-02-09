# Mobile Wallet developer usage

### Test mode toggle

By default, the Truvera Mobile Wallet will be setup in "Production" mode. This means that it will interact with assets configured using the [Truvera Workspace](../../truvera-workspace/) in production mode or that were created with a production API key. Most developers first interact with Truvera Workspace as part of the free trial, which defaults to "Test mode". In order for the wallet to work with assets created using Truvera Workspace in "Test mode" or with a test API key, you need to go into the Wallet, click "Settings" in the footer menu, and select "Test mode". You can then flip the toggle.

If you have problems issuing a credential from Truvera to the Mobile Wallet, this is the first thing to check.

## Accessing the logs

To access the logs in the Truvera Wallet, you need to enable developer mode:

1. Got to "Settings" and then tap on the version number a bunch of times.
2. You will then see the developer menu.
   1. If you click the "Export debug logs" option emails, your team will silently receive an email containing your logs. This can help us to troubleshoot problems. We can share the logs with you if you [contact our support team](../../support/support-services.md#contacting-support).
   2. If you click "Log Request", then it enables an option "View debug logs". This will allow you to see any errors that the app encountered.
