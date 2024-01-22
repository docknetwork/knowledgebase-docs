# Bonding

It is highly recommended that you make your controller and stash accounts be two separate accounts. For this, you will create two accounts and make sure each of them have at least enough funds to pay the fees for making transactions. Keep most of your funds in the stash account since it is meant to be the custodian of your staking funds.

Make sure not to bond all your DOCK balance since you will be unable to pay transaction fees from your bonded balance. It is now time to set up our validator. We will do the following:

* Bond the DOCK of the Stash account. These DOCK will be put at stake for the security of the network and can be slashed.
* Select the Controller. This is the account that will decide when to start or stop validating.

1. First, go to the Staking section. Click on "Account Actions", and then the "+ Stash" button.

![](https://lh6.googleusercontent.com/dxXfbDezWDe2NxzF6Rk\_FVWkQvrY2fD7gPLkNo0jvAWPqEluhL01pmkU8uCqT2EIrlcUzo\_ALjPV8rbHGl2O9gyYOrGxIhhnkFDcwO4ZTSPB2-Q1gevabG-av4tCsB8Sx1eFkyGY)

* **Stash account** - Select your Stash account. In this example, we will bond 4.5 MDOCK - you can, of course, stake any amount of DOCK.
* **Controller account** - Select the Controller account created earlier. This account will also need a small amount of DOCK in order to start and stop validating.
* **Value bonded** - How much DOCK from the Stash account you want to bond/stake. Note that you do not need to bond all of the DOCK in that account. Also note that you can always bond more DOCK later. However, withdrawing any bonded amount requires the duration of the unbonding period. The unbonding period is 7 days.
* **Payment destination** - The account where the rewards from validating are sent.&#x20;

2\. Once everything is filled in properly, click **Bond** and sign the transaction with your Stash account.

After a few seconds, you should see an "ExtrinsicSuccess" message. You should now see a new card with all your accounts (note: you may need to refresh the screen). The bonded amount on the right corresponds to the funds bonded by the Stash account.\
