# Banner and Native

Load and immediately show an Banner ads or an Native ads by ID.

### API

| Props                   | Function                                                                       |
| ----------------------- | ------------------------------------------------------------------------------ |
| `adId`                  | id of Banner or Native ad                                                      |
| `size`                  | size of ad View. (`small`, `medium`, `large`)                                  |
| `type`                  | kind of ad View. (`banner`, `native`)                                          |
| `onLoaded`              | call when ad loaded                                                            |
| `onLoadedError`         | call when load ad failed. return object type `ErrorCode`                       |
| `onShowed`              | call when ad showed                                                            |
| `onHide`                | call when ad closed return object type `RewardModel`                           |
| `onShowedError`         | call when show ad failed. return object type `ErrorCode`                       |

### Example

```js
<PubstarAdView
    adId={adId}
    style={styles.ad}
    size="medium"
    type="banner"
    onLoaded={() => {
        // callback when ad loaded
    }}
    onLoadedError={(errorCode) => {
        // callback when ad load error
    }}
    onShowed={() => {
        // callback when ad showed
    }}
    onHide={() => {
        // callback when ad hide with reward option
    }}
    onShowedError={(errorCode) => {
        // callback when show error
    }}
/>
```

## Custom Native

Render a Native ad inside **your own layout** instead of the default Pubstar native template.

You build the layout natively (an XML layout on Android / a view on iOS), then tell Pubstar which view inside that layout maps to each ad asset (title, body, icon, media, call-to-action, …) by passing a `NativeCustomConfig` to `PubstarAdView` via the `customConfig` prop.

### `NativeCustomConfig.Builder`

Build the config with the builder pattern. Only `layoutName` is required; bind the asset views you actually use.

| Method                              | Function                                                                  |
| ----------------------------------- | ------------------------------------------------------------------------- |
| `Builder(layoutName)`               | name of your native layout (Android XML layout name / iOS view identifier) |
| `setAdvertiserTextViewId(id)`       | view id for the advertiser name text                                      |
| `setIconImageViewId(id)`            | view id for the advertiser icon image                                     |
| `setTitleTextViewId(id)`            | view id for the headline / title text                                     |
| `setMediaContentViewGroupId(id)`    | view id for the media content container                                   |
| `setBodyTextViewId(id)`             | view id for the body / description text                                   |
| `setCallToActionButtonId(id)`       | view id for the call-to-action button                                     |
| `setLoadingViewName(id)`            | name of the loading / shimmer view shown while the ad loads               |
| `setCtaColorHex(hex)`               | hex color for the call-to-action button (e.g. `#FFFFFF`)                  |
| `build()`                           | returns a `NativeCustomConfig`                                            |

> The view ids/layout names refer to **native resources** in your host app. When `customConfig` is provided, the `size` prop is ignored — the ad fills your custom layout.

### Example

```js
import { Platform } from 'react-native';
import { PubstarAdView, NativeCustomConfig } from 'rtn-pubstar';

const customConfig = useMemo(() => {
    if (Platform.OS === 'android') {
        return new NativeCustomConfig.Builder('pubstar_applovin_native_big')
            .setAdvertiserTextViewId('ad_advertiser')
            .setIconImageViewId('ad_logo')
            .setTitleTextViewId('ad_headline')
            .setMediaContentViewGroupId('ad_media')
            .setBodyTextViewId('ad_body')
            .setCallToActionButtonId('ad_call_to_action')
            .setLoadingViewName('pubstar_shimmer_native_big')
            .setCtaColorHex('#FFFFFF')
            .build();
    }

    // iOS
    return new NativeCustomConfig.Builder('AppAdmobNativeCustom')
        .setAdvertiserTextViewId('1')
        .setIconImageViewId('2')
        .setTitleTextViewId('3')
        .setMediaContentViewGroupId('4')
        .setBodyTextViewId('5')
        .setCallToActionButtonId('6')
        .setLoadingViewName('AppShimmerBanner')
        .build();
}, []);

<PubstarAdView
    adId={adId}
    style={styles.ad}
    type="native"
    customConfig={customConfig}
    onLoaded={() => {
        // callback when ad loaded
    }}
    onLoadedError={(errorCode) => {
        // callback when ad load error
    }}
    onShowed={() => {
        // callback when ad showed
    }}
    onHide={(reward) => {
        // callback when ad hide with reward option
    }}
    onShowedError={(errorCode) => {
        // callback when show error
    }}
/>
```