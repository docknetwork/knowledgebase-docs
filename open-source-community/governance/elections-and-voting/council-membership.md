# Council Membership

Council members can be added or removed through voting by token holders or by other Council members. A simple majority (over 50%) accepting votes are required to change Council membership. Below we show how you can see the current Council members and the steps to change Council members. Note that the screenshots are for illustrative purposes only, and the actual data (addresses, names, amounts, durations can be different).The current Council members can be seen at [https://fe.dock.io/#/council](https://fe.dock.io/#/council) as shown below.

<figure><img src="../../../.gitbook/assets/council-member-list.png" alt=""><figcaption></figcaption></figure>

### Council membership

To add a new Council member, go to [http://fe.dock.io/#/council/motions](http://fe.dock.io/#/council/motions) and click on the **Propose motion** button. It will show a dialog box where you should select the `addMember` under `councilMembership` and select an account that you want to add to the Council. You need to ensure that the account being added is not already added to the Council else the proposal will be rejected; the UI does not prevent that. As shown below, Ferdie is being proposed to be added to the Council by existing member Charlie. Also, note that the `threshold` is set to 2 as there are only 3 Council members and 2 is >50% of 3. Once the correct values have been set, click _Propose_ and then submit the transaction on the next screen.

<figure><img src="../../../.gitbook/assets/propose-council-add.png" alt=""><figcaption></figcaption></figure>

Now you should set the proposal as a motion. You can see the `votes` in addition to other data and also see there is 1 `Aye` (positive vote) already. This is because the proposer is assumed to accept the proposal. Below is an expanded view of the proposal showing exactly what was proposed which is the addition of Ferdie to the Council.

<figure><img src="../../../.gitbook/assets/council-add-motion.png" alt=""><figcaption></figcaption></figure>

A council member can accept or reject the motion by voting `Aye` or `Nay` respectively. To do that click on the **Vote** button for the motion and you will see a dialog box shown below. There you can vote and then submit the transaction on the next block. Make sure that you are voting with account that is a Council member already, in the picture below, `BOB_STASH` is a Council member (you can confirm from the above pictures)

<figure><img src="../../../.gitbook/assets/council-add-vote.png" alt=""><figcaption></figcaption></figure>

You can see the current votes, i.e. `Aye` vs `Nay` for each proposal and also the members who voted `Aye` or `Nay` for each proposal by expanding the row. The image below shows that the Motion to add "Ferdie" required 2 `Aye`s and has 2 `Aye`s (2/2).

<figure><img src="../../../.gitbook/assets/council-motion-aye.png" alt=""><figcaption></figcaption></figure>

Now that the Motion has had the required `Aye`s, it can be executed by closing it. It is done by clicking on the **Close** button. Closing can be done by any account and not just by Council members. The image below shows that a regular account "EVE" who is not a Council member is closing the proposal.

<figure><img src="../../../.gitbook/assets/council-add-close.png" alt=""><figcaption></figcaption></figure>

You can now go to the overview tab and see the new Council member. The image below shows "Ferdie" in the Council members list

<figure><img src="../../../.gitbook/assets/council-members-updated.png" alt=""><figcaption></figcaption></figure>

You can also remove a Council member following a similar process of "Propose" -> "Vote" -> "Close". The image below shows "Charlie" trying to remove "Ferdie" from the Council.

<figure><img src="../../../.gitbook/assets/propose-council-remove.png" alt=""><figcaption></figcaption></figure>
