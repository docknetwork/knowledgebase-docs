# Identity Setup

Dock provides a naming system that allows participants to add personal information to their on-chain account and subsequently ask for verification by registrars. It is strongly recommended that validators create identities for their stash accounts.

Users can set an identity by registering through default fields such as legal name, display name, website, Twitter handle, Riot handle, as well as custom fields which they want verified (see [Judgements](https://docs.dock.io/validators/identity-setup/judgements)).

Users must reserve funds in a bond to store their information on chain: 20.258, and 0.066 per each field beyond the legal name. These funds are locked, not spent, and are returned when the identity is cleared. These amounts can also be extracted by querying constants through the Chain state constants tab on the [DOCK-JS App](https://fe.dock.io/#/chainstate/constants).

### Identity Setup Steps

**Option1:** The easiest way to add the built-in fields is to click the three dot icon next to your account and select "Set on-chain identity"&#x20;

<figure><img src="../../../.gitbook/assets/onchain identity.png" alt=""><figcaption></figcaption></figure>

Enter your information in the fields below and click **Set identity.**

![](https://lh4.googleusercontent.com/ofBQG5o\_5GpAMQBHz1vGoI4Mt3pgtf\_fBBD3Da0XmZaDX-J9ry5nM6A0jDYqWiww9g7-z\_gObdn\_oQVLS6WbCXhsDXqTou9fT0C6CsHXcFUNaNosDG30U2XlANm0WwBqaCyNUr-C)

**Option 2:**\
Go to the Developer tab and select Chain state.

![](https://lh4.googleusercontent.com/ZW8kZ5Uu0kpp1cOsoWkA0F8QB7Tf4NlCAhcSUSHdlRKytYnL3ztCIGdismiZfQZ9vK6v8pgpeZK0N5pbdCJvaC\_r8kZAEQVnQHzkGgEfmCZTZUiZso0UtbDrkVk7UBUoflWt-P6X)

Next, select identity as the selected constant query.

![](https://lh4.googleusercontent.com/m7Z3ltRU0uOpTXo5sxC4wz2bwGR8HCA2ET53egmJNu-Go83aVk9O2se0npSjulMc6LRJ0LjNrCn5-RrDaTUDgmO1V4MJbGCuEd6ydFauDzthx5sNxRL8nT9i2kxkqwIYHemQF-NA)

Select the constants that you would like to view and add them onto the webpage by clicking the **+** icon at the end of the bar. Each field can store up to 32 bytes of information. When inputting the data manually through the Extrinsics UI, a UTF8 to bytes converter can help.&#x20;

![](https://lh5.googleusercontent.com/v5h-vVhjHpgeyVJyRXlRIx2Kzm-VzlJlao-WtbTXQvMB1GP2QBkIfNuH2SjObYqJWNAp7miQ3eQhEeiQhGa6YN6qeKpU3-h5pQCNezf6Bu8JoLskEIKJFeWHZjcZBgsGNJ83RUdI)

Enter your information in the fields below and click **Set identity.**

![](https://lh4.googleusercontent.com/ofBQG5o\_5GpAMQBHz1vGoI4Mt3pgtf\_fBBD3Da0XmZaDX-J9ry5nM6A0jDYqWiww9g7-z\_gObdn\_oQVLS6WbCXhsDXqTou9fT0C6CsHXcFUNaNosDG30U2XlANm0WwBqaCyNUr-C)

### **Custom Fields**

To add custom fields beyond the default ones, use the Extrinsics UI to submit a raw transaction by first clicking "Add Item" and adding any field name you like. The example below adds a field steam, which is a user's Steam username. The first value is the field name in bytes ("steam") and the second is the account name in bytes ("theswader"). The display name also has to be provided, otherwise, the Identity pallet would consider it wiped if we submitted it with the "None" option still selected. That is to say, every time you make a change to your identity values, you need to re-submit the entire set of fields: the write operation is always "overwrite", never "append".

![Setting a custom field](https://lh6.googleusercontent.com/OUth53YRlK9J-siS7o6WlsoYPhMdP-xoWI4\_DVeu-FoQZfXQg5H5E4gW8O-2SO8yqf8vypk6YQeWoaLY0c0rpJ5FP6gnnyGbi4IOn\_v9dxaAOG4YSQNjttX4\_PCMCiOGfNh9ZYXq)

Note that custom fields are not displayed, only official fields for displayed now. If you want to check that the values are stored, use the Chain State UI to query the active account's identity info.

![Raw values of custom fields are available on-chain](https://lh3.googleusercontent.com/Xzckx1daTp1pC1iyQjjturhjb9d3rWzoHvbVzKwRZK2pt0UMKLY9hlBB-j1HJBBjkwJcpZh9qq-TNV2ilYRaUmP\_-FNpsgcciVvt-kLorGLE9hK1EEChN1OrWsXVwPb26A9krsp5)

### **Format Caveat**

Please note the following caveat: because the fields support different formats, from raw bytes to various hashes, a UI has no way of telling how to encode a given field it encounters. The Dock UI currently encodes the raw bytes it encounters as UTF8 strings, which makes these values readable on-screen. However, given that there are no restrictions on the values that can be placed into these fields, a different UI may interpret them as, for example, IPFS hashes or encoded bitmaps. This means any field stored as raw bytes will become unreadable by that specific UI. As field standards are adopted, this will become easier to use, but for now, every custom implementation of displaying user information will likely have to make a conscious decision on the approach to take or support multiple formats and then attempt multiple encodings until the output makes sense.

### **Clearing and Killing an Identity**

Clearing: Users can clear their identity information and have their deposit returned. Clearing an identity also clears all sub accounts and returns their deposits.

To clear an identity:

1. Navigate to the [Accounts UI](https://fe.dock.io/#/accounts).
2. Click the three dots corresponding to the account you want to clear and select 'Set on-chain identity'.
3. Select 'Clear Identity', and sign and submit the transaction.

Killing: The Council can kill an identity that it deems erroneous. This results in a slash of the deposit.\
