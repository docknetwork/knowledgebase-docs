# Registrars

Registrars can set a fee for their services and limit their attestation to certain fields. For example, a registrar could charge 1 DOCK to verify someone's legal name, email, and GPG key. When a user requests judgement, they will pay this fee to the registrar who provides the judgement on those claims. Users set a maximum fee they are willing to pay and only registrars below this amount would provide judgement.

Registrars gain trust by performing proper due diligence and would presumably be replaced for issuing faulty judgements.

### Becoming a registrar

To become a registrar, submit a pre-image and proposal into [Democracy](https://fe.dock.io/#/democracy), then wait for token holders to vote on your proposal. For best results, write a post about your identity and intentions beforehand and once the proposal is in the queue ask token holders to second the proposal so that it gets ahead in the referendum queue.

Here's how to submit a proposal to become a registrar on the Dock network:

1. Go to the [Democracy](https://fe.dock.io/#/democracy) tab, select **Submit preimage**, and input the information for this motion - notably which account you're nominating to be a registrar in the identity.setRegistrar function.

![](https://lh4.googleusercontent.com/MomwrKIR7\_wYG5mctyiVlPKOUU\_MzGzPWc4N1HrN-X8rr-icX1S9iF61VzPD6FFfoyMFdIzJT1h3nUciNDJuj7QpPn2ETcNwaRaSSjDcFciRLFknKvg61\_sppHYNj\_OUumBOIEt0)

2\. Copy the preimage hash. In the above image, it’s 0xc3a9c4807f2aff946375e586f300578dcc655837de28b0ba25aeab9b8118cf77. Submit the preimage by signing a transaction.

3\. Next, select **Submit Proposal** and enter the previously copied preimage hash. The locked balance field needs to be at least 1,000 DOCK. You can find out the minimum by querying the chain state under [Chain State](https://fe.dock.io/#/chainstate/constants) -> Constants -> democracy -> minimumDeposit.

![](https://lh3.googleusercontent.com/ULliv2p0yPHuUpJ4gR1-vb2WQHUV8pgHaLgQ4KKdHR6gjoW2tNdl2qRlW8e5uvXDZbj4wY0ztuHb3szePKQk1oCjLfReIxR9g\_9UNOH5e7qKIhftSGfNrh7VTdim9H7w\_5oh3M3H)

At this point, DOCK holders can second the motion. With enough seconds, the motion will become a referendum, which is then voted on. If it passes, users will be able to request judgement from this registrar.\


###
