# Customizing the Styling

The files placed in the `src` file tree will replace the original files. This allows the white label build to have custom colors and styling.

## Theme

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
  * `teal`: validity indicator colors
  * `blue`: used once for information box background.
  * `warning`: pending state indicator color
  * `error`: error state indicator pallet
  * `backdrop`: used for modal backdrop transparency (dark)
  * `whiteBackdrop`: used for modal backdrop transparency (light)
  * `warningBg`: warning box background
* `baseTheme`: This should require no much changes. However if there is a need to change the style for specific components, this can be updated based on [nativebase guideline](https://docs.nativebase.io/customizing-components).

[See examples of white labeled wallet designs](https://www.figma.com/file/hpHhkjv6tz3KdlSX8Hr1tH/White-label-wallet-\(Copy\)?type=design\&node-id=8-175\&mode=design)

## Images

The app icon and the splash screen logo can be customized on the app.

**TIP** You can use tools like https://www.appicon.co to auto-size your images to the appropriate sizes.

### Updating the Splash Screen Logo

There are two logos with sizes variations available for customization, they need to be replaced in the following folders.

{% hint style="warning" %}
**Please ensure that the image width matches while allowing the height to be flexible. Avoid adding empty margins to fill the remaining height.**
{% endhint %}

| Icon Size | Example                                       | Icon Size | Example                                       |
| --------- | --------------------------------------------- | --------- | --------------------------------------------- |
| 382 x 128 | ![](../../../.gitbook/assets/splash-logo.png) | 318 x 72  | ![](../../../.gitbook/assets/splash-logo.png) |
| 850 x 192 | ![](../../../.gitbook/assets/splash-logo.png) | 425 x 96  | ![](../../../.gitbook/assets/splash-logo.png) |
| 212 x 48  | ![](../../../.gitbook/assets/splash-logo.png) | 637 x 144 | ![](../../../.gitbook/assets/splash-logo.png) |
| 212 x 48  | ![](../../../.gitbook/assets/splash-logo.png) | 850 x 192 | ![](../../../.gitbook/assets/splash-logo.png) |

### Updating the App Icon

The app icon should be a `.png` file and needs to be replaced with your custom app icon in these sizes.

<table><thead><tr><th width="197">Android icon size</th><th>Example</th><th>iOS icon size</th><th>Example</th></tr></thead><tbody><tr><td>120 x 120</td><td><img src="../../../.gitbook/assets/icon (2).png" alt=""></td><td>40 x 40</td><td><img src="../../../.gitbook/assets/40.png" alt=""></td></tr><tr><td>48 x 48</td><td><img src="../../../.gitbook/assets/ic_launcher.png" alt=""></td><td>58 x 58</td><td><img src="../../../.gitbook/assets/58.png" alt=""></td></tr><tr><td>72 x 72</td><td><img src="../../../.gitbook/assets/ic_launcher (1).png" alt=""></td><td>60 x 60</td><td><img src="../../../.gitbook/assets/60.png" alt=""></td></tr><tr><td>96 x 96</td><td><img src="../../../.gitbook/assets/ic_launcher (2).png" alt=""></td><td>80 x 80</td><td><img src="../../../.gitbook/assets/80.png" alt=""></td></tr><tr><td>144 x 144</td><td><img src="../../../.gitbook/assets/ic_launcher (3).png" alt=""></td><td>87 x 87</td><td><img src="../../../.gitbook/assets/87.png" alt=""></td></tr><tr><td>192 x 192</td><td><img src="../../../.gitbook/assets/ic_launcher (4).png" alt=""></td><td>120 x 120</td><td><img src="../../../.gitbook/assets/icon (1).png" alt=""></td></tr><tr><td></td><td></td><td>180 x 180</td><td><img src="../../../.gitbook/assets/180.png" alt=""></td></tr><tr><td></td><td></td><td>1024 x 1024</td><td><img src="../../../.gitbook/assets/App icon – Appstore-1.png" alt=""></td></tr></tbody></table>
