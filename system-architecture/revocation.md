# Revocation

Credential revocation is managed with on-chain revocation registries. To revoke a credential, its id (or hash of its id) must be added to the credential. It is advised to have one revocation registry per credential type. Each registry has a unique id and an associated policy. The policy determines who can update the revocation registry.

{% hint style="info" %}
A revocation registry is shared between all the schemas of the same organisation profile.
{% endhint %}

{% hint style="warning" %}
The same revocation registry should be reused for thousands of credentials. It speeds up issuance and increases privacy.
{% endhint %}

## W3C VC Bitstring Status List v1.0

The default trust registry in Truvera Workspace for non-anonymous credentials is the VC Bitstring Status List. It is the best choice for most users of non-anonymous credentials, but requires disclosure of a revocation id to identify which credential is being revoked. This can be avoided by using Truvera's anonymous credentials, where you prove that the revocation id is not in "the list" (accumulator) without disclosing the id itself.

This registry is good for interoperability, because it follows the [W3C standard](https://www.w3.org/TR/vc-bitstring-status-list/).

It tracks all revocation entries in a single data type.

The blockchain transaction to revoke multiple credentials at once is less expensive than the Truvera Revocation Registry.

The Bitstring Status List supports both a revocation and suspension flag. An id that is added to the registry with a suspended flag can be removed, which undoes the revocation. Adding an id to the registry with the revoked flag is permanent. When triggering a credential revocation, the Truvera API uses the suspended flag by default.

## Truvera Revocation Registry

This is the original approach to revocation for non-anonymous credentials that is implemented with a private status list. It is the preferred approach only in specific scenarios.

Truvera revocation registry blockchain transactions have a different cost profile than a Bitstring Status List. It consumes more space on the ledger for multiple entries, so it is more expensive when revoking in batches but less expensive for a single entry (when revoking a single credential at one time).

The Truvera revocation registry requires disclosure of a revocation id that wouldn't otherwise be disclosed with Truvera's anonymous credentials.

The registry has an "add-only" flag specifying whether an id once added to the registry can be removed (leading to undoing the revocation) or not.

For now, only one policy is supported which is that each registry is owned by a single DID. Also, neither the policy nor the "add-only" flag can be updated post the creation of the registry for now.

## Anonymous Credential Revocation

We use [VB and KB universal types](https://github.com/docknetwork/crypto/tree/main/vb_accumulator) of accumulators for anonymous credential revocation. They have different properties, but both are bilinear map pairing based accumulators.

Truvera Anonymous Credential Revocation has specific advantages over a Bitstring Status List:

* _Superior Cryptographic Verification:_ Accumulators provide strong cryptographic guarantees of membership, unlike status lists which rely on simple lookups that lack the same mathematical security properties.
* _Enhanced Privacy Through Zero-Knowledge:_ Unlike status lists (such as W3C Bitstring Status List) which require disclosure of revocation IDs, accumulators enable proving non-revocation without disclosing which particular credential ID is being verified, allowing for anonymous credential revocation.
* _Consistently Efficient Storage:_ While status lists grow linearly with each new element added, accumulators maintain constant-size representations regardless of how many credentials are included, ensuring storage requirements remain minimal even at massive scale.
* _Comprehensive Privacy Protection:_ Accumulators offer fundamentally stronger privacy preservation than status lists, making them substantially better suited for applications where confidentiality of both membership and the specific credentials being verified is critical, particularly for anonymous credential systems.
* _Witness-Based Verification:_ Accumulators utilize a witness-based approach that allows holders to prove non-revocation without revealing their credential identifier, unlike status lists which require direct disclosure of the identifier being checked.

#### Key terms

* Credential identifier
* Witness - additional information provided to the credential holder. The witness is issued to the Holder during the initial issuance process and needs to be re-issued or updated after each revocation process.
* Accumulator - one-way function that sums a large set of items into a single accumulator value. The membership of an included item can be proved using the accumulator, the item itself, and a witness. [Read more](https://github.com/docknetwork/crypto-wasm-ts/?tab=readme-ov-file#accumulator)
* Update transactions - contain the additions, removals and witness update polynomial for the update.

#### Anonymous revocation process

* Issuer uses the credential identifier of an issued credential to generate an accumulator that gets stored on the blockchain.
* Issuer provides the holder with the credential and the witness.
* During revocation, issuer puts an update transaction on the blockchain that updates the accumulator and that the holder can use to update their witness. The most recent accumulator is present in the blockchain state and updates are stored in “calldata” which can be fetched with blockchain events.
* Holder uses the witness, accumulator, and the updates to generate an updated witness which is then used to create the proof of non-revocation by showing that their credential identifier is included in the accumulator.

#### Additional resources

* [The Rust codebase of the accumulators](https://github.com/docknetwork/crypto/tree/main/vb_accumulator). Contains additional documentation, including links to the 2 papers used for our implementation.
* [Anoncreds Tutorial](https://docknetwork.github.io/sdk/tutorials/tutorial_anoncreds.html)
