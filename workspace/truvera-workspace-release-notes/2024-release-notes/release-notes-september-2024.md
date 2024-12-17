# Release Notes September 2024

## v1.43.0 September 30

### Bug fixes

DCKA-2907 Fixed an error that ocured when issuing credentials with new DIDs on testnet.

### New features

DCKA-2566 Updated OpenAPI documentation for Schemas.

DCKA-2712 Added verification status to the billing report.

DCKA-2819 Deprecated sr25519 and secp256k1 key formats from the Dock API.

DCKA-2823 Expanded the trial subscription by allow users to have 3 team members in their trial.

DCKA-2828 Allowed OpenID pre-authed flow to bypass authorize route when appropriate.

DCKA-2829  Added verification of more credential options for the OpenID issuer setup to ensure easier setup.

DCKA-2835 Deprecated the ability to createnew StatusList2017 revocation registries.

## v1.42.0 September 13

### New features

Added ability to verify test mobile drivers licenses.

DCKA-2756 Added support for requesting mDL verification QR and verify presentation in the API

DCKA-2757 Added the ability to create a verification request for an mDL in Certs

DCKA-2758 Added the ability to  view mDL verification data in Certs&#x20;

DCKA-2759 Added an indication of accepted credential types into verification templates in Certs&#x20;



## v1.40.1 September 4

### Bug fixes

**\[DCKA-2812]** Fixed the did:polygonid creation in Dock Certs and API
