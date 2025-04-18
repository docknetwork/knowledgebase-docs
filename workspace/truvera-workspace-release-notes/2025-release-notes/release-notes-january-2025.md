# Release notes Q1 2025

## v1.60.0 April 3

### Updates and new features

DCKA-4779 Upon issuance of the credential there will be no download of the issued credential, credential needs to be distributed via email or DID during issuance or if persisted can be downloaded from the credential view.&#x20;

DCKA-4802 Update API OID4VCI flows to support latest spec requirements

### Bug fixes&#x20;

DCKA-3089  Fixed an error where the verification template attribute field would change value if edited.&#x20;

## v1.59.0 March 27

### Updates and new features

DCKA-2413 The auto generation of “subject reference ID” from the ID or Name to make it easy to for a human to identify credentials in Workspace is optional.

## v1.58.0 March 24

### Updates and new features

DCKA-3043 Implemented SD-JWT support in the API for issuance and verification. Credentials can be distributed via OpenID and via DIDComm.

DCKA-3048 Improved the credential variant selector SD-JWT variant in Truvera Workspace

DCKA-4776 Move "plan and billing" item from left menu to the profile settings menu.

## v1.57.0 March 13

### Updates and new features

DCKA-1169 Added sub-account management to the Workspace UI.&#x20;

DCKA-2233 Added filtering for verification history in the API.

DCKA-2392 Implemented team retention policy for issuance data.

DCKA-2433 Implemented team retention policy for verification data.

DCKA-2987 Proof requests can be created with an expiration date.

DCKA-3091 Renamed the Key column on the API key table to avoid mixing the key alias with the actual API key.

### Bug fixes&#x20;

DCKA-3110 Fixed a typo in the credential distribution email, where the first letter was a vowel.

## v1.56.0 February 24

### Updates and new features

DCKA-3112  Fixed verifying presentations with many different accumulators

DCKA-3113 Added assigning dockbbs keypairs at DID creation via the API.

DCKA-3114 Improved cheqd transaction processing

## v1.54.0\&v1.55.0 February 10

### Updates and new features

DCKA-2917 Added production  API support for cheqd blockchain.

DCKA-2938 did:cheqd becomes the default DID method in Certs.

## v1.53.0 February 6

### Updates and new features

DCKA-2941 Credentials will have a new revocation registry assigned automatically.&#x20;

DCKA-2386 Added the option to Delete all verification history in Truvera Workspace.

DCKA-2918 Disabled did:dock creation for testnet

## v1.52.0 January 29

### Updates and new features

Added support for multiple blockchains at the same time and cheqd blockchain in particular.

Migrated customer data from Dock blockchain to cheqd.

DCKA-2892 Added support multiple chains at the same time

DCKA-2715 Added new mDL verification templates in Truvera Workspace.

DCKA-3070 Disabled Dock node connection for testnet.

### Bug fixes

DCKA-3051 Enabled deleting verification templates that are connected to an Ecosystem in the Workspace.

DCKA-3056 Added the initials of the account user, when there is no profile picture to be visible in the Workspace.

## v1.51.0 January 9

### Updates and new features

DCKA-2915  Released API support for cheqd

### Bug fixes

DCKA-2989 Fixed an issue in the Truvera Workspace, when a polygon did was selected and then changed to a different did the subject id field would still have the "Request info" checkbox selected.&#x20;

DCKA-3028 Added a better message for a team invitation that has been accepted twice.

