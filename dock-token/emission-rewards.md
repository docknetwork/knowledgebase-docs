# Emission Rewards

The tokens released each year as emission rewards are fewer than the previous year and the total supply is expected to be in circulation within around 25 years. Each year, the network releases at most 25% of the remaining supply.&#x20;

| Year | Tokens released | Tokens remaining to be released | Total Issuance |
| ---- | --------------- | ------------------------------- | -------------- |
| 1    | 36,652,688      | 109,958,063                     | 890,041,937    |
| 2    | 27,489,516      | 82,468,547                      | 917,531,453    |
| 3    | 20,617,137      | 61,851,410                      | 938,148,590    |
| 4    | 15,462,853      | 46,388,558                      | 953,611,442    |
| 5    | 11,597,139      | 34,791,418                      | 965,208,582    |
| 10   | 2,752,056       | 8,256,167                       | 991,743,833    |
| 15   | 653,076         | 1,959,227                       | 998,040,773    |
| 20   | 154,978         | 464,934                         | 999,535,066    |
| 25   | 36,777          | 110,331                         | 999,889,669    |

The supply is adjusted such that if more than 40% of the circulating supply is staked, the emissions start to decrease each era. Thus, token holders will see more value in keeping the system liquid and encouraging apps to transact. If the staked tokens are less than 40% of the circulating supply, then the network increases the emission rate for each era until the staked tokens reach 40%. For example, the emission rewards when 30% of total supply is staked will be more than when 20% of total supply is staked which will be more than when 10% of total supply is staked; but all of these rewards will be less than those at 40% stake. This ensures that there is enough security in the network.&#x20;

The rewards for each era consist of the transaction fees collected in the era and the emission in the era. The rewards are distributed among the Treasury and the validators. The Treasury receives 50% of the rewards and the validators get 50%. Among the validators, the rewards are distributed based on their performance in that era. The network keeps track of the contributions of each validator in the era. For each validator, the network gives rewards proportional to their performance which are then distributed to the nominators in proportion to their stake after deducting commission. For instance, if a validator is expected to receive 100 tokens in an era with a 5% commission and 3 nominators with 35%, 30%, and 20% stake each, the network would give 15 tokens (10+5) to the validator and 35, 30 and 20 tokens to each of the nominators.\


#### **Key points:**

* Each year, the network will release **up to** 25% of the remaining supply.
* The released tokens are distributed across eras, each of which lasts 12 hours.
* For each era, the emission rewards and the transaction fees are first distributed: 50% to the Treasury and 50% to the validators.
* Dock uses [Nominated Proof of Stake (NPoS)](https://research.web3.foundation/Polkadot/protocols/NPoS) developed by the Web3 Foundation.
* Anyone can register on-chain to be a validator by declaring their stake and commission levels.
* The validators are selected based on the stake behind them, but their rewards depend on their performance in the network. These rewards are then distributed to the nominators proportionally.
* The emission rate is kept such that it incentivizes 40% of the circulating supply to be liquid as NPoS increases the emission per era linearly (next era will have more emission) until the 40% level (`Chi_ideal` in NPoS doc) is reached. Otherwise, emission rates per era decrease exponentially.
* Should malicious behavior be detected, the validators and their nominators will be slashed, i.e. lose a fraction of their stake. The fraction depends on the severity of the malicious behavior:
  * Remaining unavailable (not producing blocks or sending heartbeats) has milder penalties.
  * Producing a block out of turn comes with harsher penalties.
  * Equivocation, either producing 2 blocks at the same height or finalizing 2 blocks at the same height results in even more severe penalties.
  * Malicious activities carried out by multiple validators are punished more severely since that is seen as a coordinated attack.
* The slashed stake goes to the Treasury and/or may go to the validators depending on the malicious behavior. Dock's governing council can reverse any slashes should the slashing be found to be unfair.
* Tokens staked can be used for governance as well.
