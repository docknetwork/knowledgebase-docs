# Configuration

You will be invited to a dedicated Github repository, which will contain the files needed to customize, build and sign a white label build of the Dock Wallet to be distributed in the Apple and Google Play stores.

## General Setup

First clone the GitHub repository to add the source code to your machine.

<figure><img src="../../.gitbook/assets/Screenshot 2023-09-01 at 17.25.08 (1) (1).png" alt=""><figcaption></figcaption></figure>

Open the code editor and now you can go through the documentation in [README.md](http://readme.md/) and start making changes on the repository.

To make changes follow the instructions below and then submit a pull request (PR) to this repository to be reviewed by the Dock team. Once the changes are accepted a new release will be generated.

### Set the Application's Display Name & Package Id

First thing to do is setting the Application Display name and Package Id/Package Name.

:information\_source: _The package name uniquely identifies the app on the device; it is also unique in the Google Play store/ Apple App Store. This means that once you have published an app with this package name, you can never change it; doing so would cause your app to be treated as a brand new app, and existing users of your app will not see the newly packaged app as an update._

In ../app.json set the following fields

```
"displayName": <your application name>
"packageId": <your application package name>
"companyName": <your application package name>
"companyNamePossessive": <your application package name>

For example:
"name": "DockApp",
"displayName": "Cool Wallet",
"packageId": "com.coolwallet.app",
"companyName": "Cool",
"companyNamePossessive": "Cool's"
```

## Enabling and Disabling Features

The white label wallet can have a subset of the available features enabled.

To enable or disable a feature update the entries in the features\_config.json file

### Features you can enable or disable

* **Accounts**: The `Tokens` tab allows users to buy, send and receive Dock tokens. This tab will be hidden if this feature is disabled.
* **Credentials**: The `Credentials` tab will be hidden and no credentials will be able to be imported into the wallet if this feature is disabled.
* **DID Management**: Disabling this feature will mean that the user can not add or delete Decentralized Identifiers (DIDs). The `DIDs` tab is controlled by this feature flag.
* **Credential Verifier**: Allows the user to act as a Verifier and initiate verification flows from their device
* **Credential URLs**: Detects URLs in credential details. It allows users to click the detected links which are then opened in a browser on the user's device.

## Customizing the Styling

The files placed in the `src` file tree will replace files during the build in the `dock-app` repo. This allows the white label build to have custom colors and styling.

### Theme

The app theme can be customized using the values in the ../src/design-system/theme.js file. The javascript file contains three customizable variables:

* `Theme`: Contains the following variables:
  * `borderRadius` determines the radius of some card-like elements, e.g Modals.
  * `touchOpacity` the opacity of pressable items that should indicate pressed state
* `COLORS`: Determines the color scheme of the entire application. It uses a color pallet system (You can generate a color pallet using any of the tools like [JSON Color Palette Generator](https://json-color-palette-generator.vercel.app/), [Smart Swatch](https://smart-swatch.netlify.app/), or [Palx](https://palx.jxnblk.com/)). This section contains the following main colors:
  * `primary`: primary brand color pallet.
  * `primaryButton`: range `200-600` pallet for primary button phases (disabled, pressed, etc.) and a `text` value to set the color of the primary button text.
  * `secondaryButton`: range `200-600` pallet for secondary button phases (disabled, pressed, etc.) and a `text` value to set the color of secondary button texts.
  * `secondary`: with only 400 and 600 values in the pallet, they is used as accent backgrounds in sections of the application. To maintain contrast in values are recommended to be dark colored for dark themed customization and light for light themed customization.
  * `neutral`: a pallet for background and text colors. Contrast between 1 and 900 should be as much as possible, with light theme ranging from very dark(e.g {1: "black"}) to very light (e.g {900: "white}) and dark theme ranging the opposite way
  * `orange`: test mode indicator background and text colors
  * `teal`: validity inidicator colors
  * `blue`: used once for information box background.
  * `warning`: pending state indicator color
  * `error`: error state indicotor pallet
  * `backdrop`: used for modal backdrop transparency (dark)
  * `whiteBackdrop`: used for modal backdrop transparency (light)
  * `warningBg`: warning box background
* `baseTheme`: This should require no much changes. However if there is a need to change the style for specific components, this can be updated based on [nativebase guideline](https://docs.nativebase.io/customizing-components).

[See examples of white labeled wallet designs](https://www.figma.com/file/hpHhkjv6tz3KdlSX8Hr1tH/White-label-wallet-\(Copy\)?type=design\&node-id=8-175\&mode=design)

### Images

The app icon and the splash screen logo can be customized on the app.

**TIP** You can use tools like https://www.appicon.co to auto-size your images to the appropriate sizes.

#### Updating the Splash Screen Logo&#x20;

There are two logos with sizes variations available for customization, they need to be replaced in the following folders.

{% hint style="warning" %}
&#x20;**Please ensure that the image width matches while allowing the height to be flexible. Avoid adding empty margins to fill the remaining height.**
{% endhint %}

| Icon Size | Example                                           | Icon Size | Example                                               |
| --------- | ------------------------------------------------- | --------- | ----------------------------------------------------- |
| 382 x 128 | ![](../../.gitbook/assets/logo.png)               | 318 x 72  | ![](<../../.gitbook/assets/splash\_logo (1) (1).png>) |
| 850 x 192 | ![](../../.gitbook/assets/splash-logo.png)        | 425 x 96  | ![](<../../.gitbook/assets/splash\_logo (2).png>)     |
| 212 x 48  | ![](../../.gitbook/assets/splash\_logo.png)       | 637 x 144 | ![](<../../.gitbook/assets/splash\_logo (3).png>)     |
| 212 x 48  | ![](<../../.gitbook/assets/splash\_logo (1).png>) | 850 x 192 | ![](<../../.gitbook/assets/splash\_logo (4).png>)     |

#### Updating the App Icon&#x20;

The app icon should be a `.png` file and needs to be replaced with your custom app icon in these sizes.

| Android icon size | Example                                           | iOS icon size | Example                                                |
| ----------------- | ------------------------------------------------- | ------------- | ------------------------------------------------------ |
| 120 x 120         | ![](../../.gitbook/assets/icon.png)               | 40 x 40       | ![](../../.gitbook/assets/40.png)                      |
| 48 x 48           | ![](../../.gitbook/assets/ic\_launcher.png)       | 58 x 58       | ![](../../.gitbook/assets/58.png)                      |
| 72 x 72           | ![](<../../.gitbook/assets/ic\_launcher (1).png>) | 60 x 60       | ![](../../.gitbook/assets/60.png)                      |
| 96 x 96           | ![](<../../.gitbook/assets/ic\_launcher (2).png>) | 80 x 80       | ![](../../.gitbook/assets/80.png)                      |
| 144 x 144         | ![](<../../.gitbook/assets/ic\_launcher (3).png>) | 87 x 87       | ![](../../.gitbook/assets/87.png)                      |
| 192 x 192         | ![](<../../.gitbook/assets/ic\_launcher (4).png>) | 120 x 120     | ![](../../.gitbook/assets/120.png)                     |
|                   |                                                   | 180 x 180     | ![](../../.gitbook/assets/180.png)                     |
|                   |                                                   | 1024 x 1024   | ![](<../../.gitbook/assets/App icon – Appstore-1.png>) |
