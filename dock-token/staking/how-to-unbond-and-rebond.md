# How to unbond and rebond

The following describes how to stop nominating or validating and retrieve your tokens. Please note that all staking networks have a delayed exit period, called the unbonding period, which serves as a cooldown. You will not be able to transfer your tokens before this period has elapsed, and you will not receive any staking rewards during this period (as you are not nominating any validators). This period is 7 days on the Dock network.

### Step 1: Stop Nominating

On the [Dock-JS Apps](https://fe.dock.io/#/staking) navigate to the **Staking** tab and go to the on the [**Account Actions**](https://fe.dock.io/#/staking/actions) tab and click **Stop Nominating** or **Stop Validating** (depending on your role) on the account you'd like to stop nominating. This will "chill" the tokens.

![](https://lh5.googleusercontent.com/Ll1N\_v8iNCIqI\_lD4\_uYz-j\_Voec0ehyIkxlUgVBFrlbwX5Dw4gwlF6V5WCWoMtGTheveTpo-bjiyaS3aG9SmcXMdXFB73PqDU6\_kc0rS7ZxoDAqxgilpdQXP1h5CqvFcbVE8rZG)

### Step 2: Unbonding an amount

Your tokens will need to be unbonded in order to be able to withdraw from staking. To unbond the amount, click the three dots icon for the account you want to unbond tokens and select **Unbond funds**.

![](https://lh4.googleusercontent.com/Iva0lok-cURaLfDvQ3J8awKh2GLGL5L7vow6kLqUiCTFEwbYLa7yhPJFuS8bH\_5sVUQPxKlRPsjqwCXfffza9SURrOczrhorz\_Quso1gbDLG\_m1mPUyO7cvYruUsuuBXvjyxv1F1)

Enter the amount of tokens to unbond, click **Unbond**, and confirm the transaction.

![](https://lh4.googleusercontent.com/3rGDzTeZXS5bZKyDPh2kekTOwzaMcb1UnKxdQvPluIe2AatA8EOxOUXri-HHNFQ3HBLnzZgdg-s3qu1dFPzN0qfISdHm4C4t-Hij-ILdQRTKJVCGeOxyrRPXqE1g\_j4WUZXEQd8U)

If successful, your balance will show as "unbonding" with an indicator of how many more blocks remain until the amount is fully unlocked.

![](https://lh6.googleusercontent.com/n\_PDwx5\_IEkl\_w6Z9RFEwnMSFWX5ey3D4DJqCQcad1dVuDOIWMwJNifGI0GVFl4UsJMzBEhy\_nzIkph1RqlA-4UBUbuwPwlkHY9\_1RdoLbdWKBrWvQ1W\_ERjHOBKRLal-334QT5\_)

### 3. Withdraw unbonded tokens

You can check the amount of time remaining until you can withdraw your stake in the [Accounts](https://fe.dock.io/#/accounts) page by expanding your account balance. There is a tiny icon beside the word "unbonding" that will eventually become an unlock icon once your tokens are available to withdraw. Click that icon directly to submit the withdraw transaction which, once complete, will increase your transferable balance by the amount of tokens you've just fully unbonded.

<figure><img src="../../.gitbook/assets/unbond.png" alt=""><figcaption></figcaption></figure>

## Rebonding before the end of the unbonding period

If you want to rebond your tokens before the unbonding period is over you can do this by issuing a rebond extrinsic. This allows you to bond your tokens that are still locked without waiting until the end of the unbonding period.

In order to do this you will need to manually issue an extrinsic by going to the [**Extrinsics**](https://fe.dock.io/#/extrinsics) section that's located in the **Developer** dropdown in the top menu. Enter the amount of tokens that are currently locked in unbonding that you want to rebond and click **Submit Transaction**.

![](https://lh4.googleusercontent.com/YGvNYTHQQxfIPiVESy88gQTlTSvLz7ZpAmKG9bMU-Ce2bjXXUxE0BDhOYGxAUmi8Q0sOSc\_PipvCpu6EVAKPTQroVIBzKchH7iEck5VU7tSPHT9tg4CFT7Dw2lTckHE9FpNHzUxI)

Confirm the transaction in the next pop-up. Once the transaction is processed, your tokens will be rebonded again and you can start staking with them.
