# Interoperability with OpenID

The OpenID for Verifiable Credentials work is a product of the OpenID Connect Working Group. The [whitepaper](https://openid.net/wordpress-content/uploads/2022/06/OIDF-Whitepaper_OpenID-for-Verifiable-Credentials-V2_2022-06-23.pdf) OpenID for Verifiable Credentials describes the work and its motivations.

OID4VCs consists of three use cases with OID protocols:

1. Credential issuance: OpenID for Verifiable Credential Issuance (OID4VC)
2. Credential presentation: OpenID for Verifiable Presentations (OID4VP)
3. Pseudonymous user authentication through a wallet: OpenID for Self-Issued Identity Providers

Though it’s a distinct protocol, it uses patterns from [OpenID Connect Core](https://openid.net/specs/openid-connect-core-1_0-final.html). Credential issuance leverages the authorization code flow from oAuth for authenticating the user sufficient to authorize credential issuance and introduces a new “credential issuance” endpoint.&#x20;

The OpenID4VC is a widely respected standard, that has a large community with lots of contributors. By supporting OpenID4VC Truvera allows customers to issue credentials into various digital wallets. It shows our strong commitment to interoperability and gives them the flexibility needed to build their products.
