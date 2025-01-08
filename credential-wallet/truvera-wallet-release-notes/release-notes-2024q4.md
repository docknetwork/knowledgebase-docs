# Release Notes 2024Q4

## Wallet 1.4.3 December 9

### New features and updates

DCKW-635 Upgraded the wallet to accept the updated credential SDK that splits credentials and blockchain functionalities.

### Bug fixes

DCKW-653 Fixed verification error messaging for when "Unexpected error" appeared when verifying a ZKP credential.

DCKW-656 Fixed the not working Decline button.

DCKW-672 Fixed issues with installing npm

DCKW-675 Fixed verification error "Subject required"

## Wallet 1.4.2 & Wallet 1.4.1 November 11&18

### New features and updates

DCKW-607 Updated the wallet notification functionality, when a notification is clicked, the user will be taken to the specific credential detail screen.

DCKW-644 Added a prompt to turn on notifications for those users that don't have them enabled.&#x20;

## Wallet 1.4.0 November 1

### New features and updates

DCKW-555 Released [Cloud wallet ](../../developer-documentation/wallet-sdk/cloud-wallet.md)

DCKW-629 Removed Transak code to prepare for token migration

DCKW-590 Refactored wallet-sdk-core and wallet-sdk-data-store to support Custom Data Storage Injection

### Bug fixes

DCKW-642  fixed an issue when a wallet was unable to fetch issuer's Ecosystem

DCKW-647 Adjusted the close button in the notification modal

DCKW-649 Wallet-sdk examples not running on NodeJS and React Native
