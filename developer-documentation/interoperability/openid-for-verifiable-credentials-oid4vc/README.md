# OpenID for Verifiable Credentials (OID4VC)

The OpenID for Verifiable Credentials work is a product of the OpenID Connect Working Group. The [whitepaper](https://openid.net/wordpress-content/uploads/2022/06/OIDF-Whitepaper\_OpenID-for-Verifiable-Credentials-V2\_2022-06-23.pdf) OpenID for Verifiable Credentials describes the work and its motivations.

OID4VCs consists of three use cases with OID protocols:

1. Credential issuance: OpenID for Verifiable Credential Issuance (OID4VC)
2. Credential presentation: OpenID for Verifiable Presentations (OID4VP)
3. Pseudonymous user authentication through a wallet: OpenID for Self-Issued Identity Providers

Though it’s a distinct protocol, it uses patterns from [OpenID Connect Core](https://openid.net/specs/openid-connect-core-1\_0-final.html). Credential issuance leverages the authorization code flow from oAuth for authenticating the user sufficient to authorize credential issuance and introduces a new “credential issuance” endpoint.&#x20;

OID4VC uses the three-way model of SSI Verifiable Credential exchange by splitting the trust triangle into two parts: the Issuer (server)→Holder (client) interaction (using a oAuth based protocol), and the Holder (client)→Verifier (server) interaction (but the wallet acts as the oAuth authorization server and then uses DIF PEX to return the proof). In both of these parts, the server authenticates to the holder using an SSL certificate that is trusted by the client’s browser certificate trust chain, and the holder is anonymous to the server until identity information has been exchanged such as a username / password being provided to the issuer and a credential being provided to the verifier.

The OpenID4VC is a widely respected standard, that has a large community with lots of contributors. By supporting OpenID4VC Dock allows customers to issue credentials into various digital wallets. It shows our strong commitment to interoperability and gives them the flexibility needed to build their products.
