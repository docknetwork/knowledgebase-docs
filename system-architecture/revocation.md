# Revocation

Credential revocation is managed with on-chain revocation registries. To revoke a credential, its id (or hash of its id) must be added to the credential. It is advised to have one revocation registry per credential type. Each registry has a unique id and an associated policy. The policy determines who can update the revocation registry.&#x20;

{% hint style="warning" %}
The same revocation registry should be reused for thousands of credentials.  It speeds up issuance and increases privacy.
{% endhint %}

{% hint style="info" %}
Revocation registry is shared between all the schemas of the same organisation profile.
{% endhint %}

## W3C Status List 2021

Is a default trust registry in Truvera Workspace for non-anonymous credentials. It is the best choice for most users of non-anonymous credentials, but requires disclosure of revocation id, which identifies which credential is being revoked. This can be avoided by using Truvera's anonymous credentials, where you prove that the revocation id is not in "the list" (accumulator) without disclosing the id itself.

This registry is good for interoperability, because it follows the [W3C standard](https://www.w3.org/community/reports/credentials/CG-FINAL-vc-status-list-2021-20230102/).&#x20;

It tracks all revocation entries in a single data type.

The blockchain transaction to revoke multiple credentials at once is less expensive than the Truvera Revocation Registry.

Supports revocation and suspension flags, which allows specifying whether an id once added to the registry can be removed (leading to undoing the revocation) or not.

## Truvera Revocation Registry

Original approach to revocation for non-anonymous credentials that is implemented with a private status list. It is the preferred approach only in specific scenarios.&#x20;

Truvera Revocation registry blockchain transactions have a different cost profile than with W3C Status List 2021, it consumes more space on the ledger for multiple entries, so it is more expensive when revoking in batches, but it is less expensive for a single entry, when revoking a single credential at one time.

Requires disclosure of revocation id that wouldn't otherwise be disclosed with Truvera's anonymous credentials.&#x20;

The registry has an "add-only" flag specifying whether an id once added to the registry can be removed (leading to undoing the revocation) or not.&#x20;

For now, only one policy is supported which is that each registry is owned by a single DID. Also, neither the policy nor the "add-only" flag can be updated post the creation of the registry for now.

## Anonymous Credential Revocation

We use [VB and KB universal types](https://github.com/docknetwork/crypto/tree/main/vb_accumulator) of accumulators for anonymous credential revocation. They have different properties, but both are bilinear map pairing based accumulators.

Advantages over Status List 2021:

- *Superior Cryptographic Verification:* Accumulators provide strong cryptographic guarantees of membership, unlike status lists which rely on simple lookups that lack the same mathematical security properties.
- *Enhanced Privacy Through Zero-Knowledge:* Unlike status lists (such as W3C Status List 2021) which require disclosure of revocation IDs, accumulators enable proving non-revocation without disclosing which particular credential ID is being verified, allowing for anonymous credential revocation.
- *Consistently Efficient Storage:* While status lists grow linearly with each new element added, accumulators maintain constant-size representations regardless of how many credentials are included, ensuring storage requirements remain minimal even at massive scale.
- *Comprehensive Privacy Protection:* Accumulators offer fundamentally stronger privacy preservation than status lists, making them substantially better suited for applications where confidentiality of both membership and the specific credentials being verified is critical, particularly for anonymous credential systems.
- *Witness-Based Verification:* Accumulators utilize a witness-based approach that allows holders to prove non-revocation without revealing their credential identifier, unlike status lists which require direct disclosure of the identifier being checked.

#### Key terms

* Credential identifier
* Witness - additional information provided to the credential holder. The witness is issued to the Holder during the initial issuance process and needs to be re-issued or updated after each revocation process.
* Accumulator - one-way function that sums a large set of items into a single accumulator value. The membership of an included item can be proved using the accumulator, the item itself, and a witness. [Read more](https://github.com/docknetwork/crypto-wasm-ts/?tab=readme-ov-file#accumulator)&#x20;
* Update transactions - contain the additions, removals and witness update polynomial for the update.

#### Anonymous revocation process

* Issuer uses the credential identifier of an issued credential to generate an accumulator that gets stored on the blockchain.
* Issuer provides the holder with the credential and the witness.
* During revocation, issuer puts an update transaction on the blockchain that updates the accumulator and that the holder can use to update their witness. The most recent accumulator is present in the blockchain state and updates are stored in “calldata” which can be fetched with blockchain events.
* Holder uses the witness, accumulator, and the updates to generate an updated witness which is then used to create the proof of non-revocation by showing that their credential identifier is included in the accumulator.

#### Additional resources

* [The Rust codebase of the accumulators](https://github.com/docknetwork/crypto/tree/main/vb_accumulator). Contains additional documentation, including links to the 2 papers used for our implementation.
* [Anoncreds Tutorial](https://docknetwork.github.io/sdk/tutorials/tutorial_anoncreds.html)



