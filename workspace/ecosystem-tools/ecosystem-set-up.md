# Ecosystem set up

### Create an ecosystem

You can create an Ecosystem through the left side menu by clicking **Ecosystem -> Create Ecosystem** button.

When creating an ecosystem an on-chain trust registry is created on the blockchain, a list of relationships between issuers and verifiers. It simplifies the process of identifying which issuers and verifiers are trustworthy within a particular ecosystem.

{% hint style="info" %}
Ecosystem Tools is an add-on feature. If you do not see it in your menu bar and want it enabled for your account please contact support@truvera.io
{% endhint %}

First steps in creating your ecosystem is defining your brand. Ecosystem branding is important, it will be present on the credentials issued by the participants and verification templates for the verifiers. Having a clearly defined brand makes it easier for ecosystem participants to trust the ecosystem and have a unified experience from credential issuance, to storage and verification.

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-23 at 14.11.27.png" alt="" width="375"><figcaption></figcaption></figure>

You will need to set the Ecosystem **Name**, **Description,** add an **Ecosystem URL**, a valid URL that links to a page outlining the advantages and key details of joining your ecosystem.

**Ecosystem Administrator Profile DID** will allow you to choose from an existing or add a new DID that will be the administrator of the ecosystem.

Next step will allow you to set your Governance Framework document, that is used to communicate the rules and guidelines of the ecosystem to every stakeholder, ensuring clarity and consistency, which helps align all stakeholders on the processes surrounding issuance and verification.

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-09 at 16.30.03.png" alt="" width="375"><figcaption></figcaption></figure>

### Invite a participant

After the ecosystem is set up you can start inviting participants. Ecosystem participants can be Issuers, Verifiers or both depending on their role in your ecosystem. You will be able to assign credential schemas based on the role of the participant.

Ecosystem participants can have and manage their own Truvera accounts, but we also enable our customers to create ecosystems where the participant accounts are managed and paid for by them. Using [Sub-accounts](../../truvera-api/sub-accounts.md) allows creation of additional Truvera accounts and inviting them to participate in the ecosystem using the API.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-09 at 16.41.36.png" alt=""><figcaption></figcaption></figure>

After clicking **Invite participants** you will be able to select a credential schema and a role of the participant.&#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2024-03-21 at 16.57.38.png" alt="" width="375"><figcaption></figcaption></figure>

Ecosystem participants will need to have an account with Truvera to join the ecosystem. When they are logged in to their Truvera Workspace account and click on the link provided by the ecosystem administrator, they will be immediately prompted to **Join the ecosystem** and select an organization profile that will be used to participate in the ecosystem.

<figure><img src="../../.gitbook/assets/Screenshot 2024-02-12 at 16.10.15.png" alt=""><figcaption></figcaption></figure>

Ecosystem Administrator and participants will see the list of Issuers and Verifiers in the table.

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-23 at 14.16.55.png" alt=""><figcaption></figcaption></figure>

Ecosystem administrator will be able to **Suspend**, **Remove** or **Edit** the existing Ecosystem participants. They can also change the role of the participant and assign schemas.

### Assign credential schemas

To assign a credential schema to participants you will need to first [create the schemas](../create-a-schema.md). To assign the schema you will click the **Add schema** button.

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-23 at 14.17.50.png" alt=""><figcaption></figcaption></figure>

You will be able to select from your schemas from a dropdown or enter schema URL and assign it to ecosystem participants.

<figure><img src="../../.gitbook/assets/Screenshot 2024-07-16 at 15.48.02.png" alt="" width="375"><figcaption></figcaption></figure>

{% hint style="info" %}
You can choose to add a verification price for your schema, which will set a fee for each verification of credential using the selected schema. [Learn more about verification prices](../monetizing-credentials/)
{% endhint %}

Credential schemas can have Restricted or Public verifiability. If the schema is assigned to at least one participant that can verify the schema, the verification will restricted to only those participants. If there are no assigned verifiers the schema will be publicly verifiable.

<figure><img src="../../.gitbook/assets/Screenshot 2024-12-23 at 14.28.24.png" alt=""><figcaption></figcaption></figure>



Assigned schemas will be immediately available to participants and once credentials are issued using a schema assigned to an ecosystem, the ecosystem branding will be visible throughout the entire credential user journey.

Ecosystem branding will be visible in the wallet once a credential is issued by an ecosystem participant.

![](<../../.gitbook/assets/Screenshot_20240212_164914_Dock Wallet.jpg>)

### Add verification templates

Ecosystem administrator will be able to add verification templates that will be available for all ecosystem participants.

<figure><img src="../../.gitbook/assets/Screenshot 2024-07-18 at 14.46.28.png" alt=""><figcaption></figcaption></figure>
