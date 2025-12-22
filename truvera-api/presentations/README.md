# Presentations

To verify a credential, the verifier will need to create a proof template and generate a proof request to which the holder wallet will provide the verifiable presentation. The REST API does not contain functions to create a verifiable presentation, as that is done through the [Wallet SDK](https://github.com/docknetwork/sdk).

Our system supports the [DIF Presentation Exchange (PEX)](https://identity.foundation/presentation-exchange/) syntax for querying and filtering credentials.

See the [https://identity.foundation/presentation-exchange/#input-descriptor-extensions](https://identity.foundation/presentation-exchange/#input-descriptor-extensions) for more examples, but a few common use cases are:

#### Require a numeric attribute to be within a range

For example, a verifier might require that the holder have an income between $100,000 and $200,000 per year. This could be requested using the following `input_descriptor`

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

For example, a verifier might require that the credential be issued after a certain date. In this example the verifier is requiring that the credential was issued between January 1, 2020 and December 31, 2020.

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
