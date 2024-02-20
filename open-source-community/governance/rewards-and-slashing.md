# Rewards and slashing

### Rewards

Dock utilizes [Nominated Proof of Stake (NPoS)](https://research.web3.foundation/en/latest/polkadot/NPoS/index.html) as designed by Web3 Foundation wherein validators can participate by staking (locking) tokens. Candidate validators can stake their own tokens or other token holders can nominate candidates by locking tokens on their behalf. The locked tokens can only be withdrawn after 7 days. This time period is called an unbonding period.&#x20;

The candidates with the most stake behind them become validators and earn rewards every epoch; while there can be several hundred validators, only 50 validators will be validating at any given instant. In case of malicious behavior, the validators and their nominators are penalized proportionately via a mechanism called _slashing_. Slashing is an event where the validator and/or nominator loses a defined proportion of staked tokens, which are then redistributed among validators, the maliciousness reporter (if applicable), and the Treasury.\
\
The block rewards consist of the emission rewards and fees from the transactions and block rewards for each epoch go to the Treasury with 60% being reserved for Treasury and 40% for validators. The emission rewards are configured such that every year at most a certain amount of tokens needs to be emitted and this number decreases each year by 25% of the remaining supply. The Treasury also gets a share of the slashing depending on the malicious activity.&#x20;

### Slashing

The network can punish validators for being offline or equivocation in block production or finality. The nature and severity of the punishment also changes with the number of validators involved in the activity. If only 10% of validators are detected offline then no direct economic penalty (slashing) is applied. Otherwise, the penalty increases linearly to the number of offline validators.&#x20;

However, validators are removed from the current validator set and barred from participating in the next validator selection (indirect economic penalty) for being offline. This is called chilling. Validators found to be equivocating are sent to chilling and slashed, the slashing being quadratically proportional to the number of validators equivocating. Anticipating that a validator might go offline or might equivocate due to bugs in the software, the Council reserves the right to reverse any slashing event (up to 6 epochs in the past, i.e. approx. 2 months) by voting.

Reversing any slash requires at least a simple majority of Council votes. As the slashing amount increases, more Council votes are needed to reverse the slash.

Once a validator gets slashed, it goes into the state as an "unapplied slash" (these are viewable by all, the apps UI shows it per validator and then all the affected parties along with the amounts) while unapplied, a proposal can be made to reverse it after this grace period, the slashes are applied.
