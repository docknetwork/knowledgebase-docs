# Release Notes v1.28.0 Apr 14, 2024

## Overview:

This release includes updates to the user interface, improvements to verification template handling, bug fixes related to credential issuance, and tasks aimed at defining architecture for future features.

## **New Features**

#### **Optional Fields in Verification Templates**

* **\[DCKA-2468]**: Verification templates in Certs now support optional fields. Administrators can designate attributes as optional, enhancing flexibility in proof presentation responses.

#### **Ability to Close Upgrade Pop-up**

* **\[DCKA-2485]**: Users now have the option to close the "Upgrade your plan to continue" pop-up and remain on the same screen. This feature allows users to adjust their work and proceed without triggering the pop-up again.

#### **Ecosystem Membership Display in Organization Profiles**

* **\[DCKA-2417]**: Organization profiles now display the ecosystems where the organization profile is used. Additionally, ecosystem badges are included in the organization profile details, providing easy access to ecosystem information.

## **Bug Fixes and Improvements**

#### **BBS+ Credential Issuance Error**

* **\[DCKA-2501]**: Resolved an error where issuing BBS+ credentials resulted in a "Schema properties did not contain top-level key" error, ensuring smooth credential issuance processes.

#### **Revocation Status Error with did:polygonid Creation**

* **\[DCKA-2509]**: Fixed an issue where creating a new organization profile with a did:polygonid DID resulted in a "can't fetch revocation status" error, ensuring successful profile creation without errors.

## **Tasks and Research**

#### **Architecture Definition for Verifier Pays Issuer**

* **\[DCKA-2263]**: Defined the architecture for Verifier Pays Issuer, laying the groundwork for future implementation and facilitating transactions within the ecosystem.

#### **Wallet Cache Management Solution**

* **\[DCKA-2474]**: Introduced a basic key/value map for wallet cache management, with plans to expand functionality to include limiting cached wallets, clearing old values, and improving the interface for setting/getting values.
