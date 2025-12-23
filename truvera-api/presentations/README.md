# Presentations

[Credential verification](../../workspace/verify-credentials.md) consists of [defining a verification template / proof template](proof-templates.md), using it to generate a [proof request](proof-requests.md), delivering the proof request to a holder, receiving the proof response from the holder's wallet, and checking that response for consistency. The Truvera API automates many of these steps for you. The REST API does not contain functions to create a verifiable presentation, as that is done through the [Wallet SDK](../../credential-wallet/wallet-sdk/). The open source [Truvera Credential SDK](https://github.com/docknetwork/sdk) also contains the foundational capabilities needed to create proof presentations.

Our system supports the [DIF Presentation Exchange (PEX)](https://identity.foundation/presentation-exchange/) syntax for querying and filtering credentials.

## Examples

These are a few common examples of credential verification. More examples are in the documentation for [DIF Presentation Exchange](https://identity.foundation/presentation-exchange/#input-descriptor-extensions).

#### Require a numeric attribute to be within a range

A verifier might require that the holder have an income between $100,000 and $200,000 per year. This could be requested using the following `input_descriptor`

```
{
  path: ['$.credentialSubject.income.2022.total'],
  filter: {
    type: 'number',
    minimum: 100000,
    maximum: 200000
  },
}
```

#### Require a date attribute to be within a range

A verifier might require that the credential be issued after a certain date. In this example the verifier is requiring that the credential was issued between January 1, 2020 and December 31, 2020.

```
{
  path: ['$.issuanceDate'],
  filter: {
    "type": "string",
    "format": "date",
    "formatMinimum": "2020-01-01",
    "formatMaximum": "2020-12-31"
  },
}
```
