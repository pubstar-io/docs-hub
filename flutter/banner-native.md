# Banner and Native

Load and immediately show an Banner ads or an Native ads by ID.

### API

| Props                   | Function                                                                                                   |
| ----------------------- | ---------------------------------------------------------------------------------------------------------- |
| `adId`                  | id of Banner or Native ad                                                                                  |
| `size`                  | size of ad View. (`small`, `medium`, `large`)                                                              |
| `type`                  | type of ad View. (`banner`, `native`)                                                                      |
| `mode`                  | mode of ad View (`onlyShow`, `loadAndShow`)                                                                |
| `onError`               | call when show ad failed. return object type `PubstarError`                                                |
| `onHide`                | call when ad hidden/closed (supports rewarded ads). Returns detailed PubstarReward object (type, amount) |
| `onLoaded`              | call when ad loaded                                                                                        |
| `onShowed`              | call when ad showed                                                                                        |

### Example

```dart
PubstarAdView(
  adId: adId,
  size: PubstarAdSize.small,
  type: PubstarAdType.banner,
  mode: PubstarAdViewMode.loadAndShow,
  onError:
      (error) {
          // callback when ads error
      },
  onHide:
      (reward) {
          // callback when ad hide with reward option
      },
  onLoaded: () {
      // callback when ad loaded
  },
  onShowed: () {
      // callback when ad showed
  },
)
```

## Custom Native

Render a Native ad inside **your own layout** instead of the default Pubstar native template.

You build the layout natively (an XML layout on Android / a view on iOS), then tell Pubstar which view inside that layout maps to each ad asset (title, body, icon, media, call-to-action, …) by passing a `PubstarNativeCustomConfig` to `PubstarAdView` via the `nativeCustomConfig` prop.

### `PubstarNativeCustomConfig`

Only `layoutName` is required; bind the asset views you actually use. Resource names are resolved from your host app package (Android XML layout/view names, iOS view identifiers).

| Field                     | Function                                                            |
| ------------------------- | ------------------------------------------------------------------ |
| `layoutName`              | name of your native layout (required)                              |
| `advertiserTextViewId`    | view id for the advertiser name text                               |
| `iconImageViewId`         | view id for the advertiser icon image                              |
| `titleTextViewId`         | view id for the headline / title text                              |
| `mediaContentViewGroupId` | view id for the media content container                            |
| `bodyTextViewId`          | view id for the body / description text                            |
| `callToActionButtonId`    | view id for the call-to-action button                              |
| `loadingViewId`           | name of the loading / shimmer view shown while the ad loads        |
| `ctaColorHex`             | hex color for the call-to-action button (e.g. `#FFFFFF`)           |

### Example

```dart
import 'dart:io';
import 'package:pubstar_io/pubstar_io.dart';

final customConfig = Platform.isAndroid
    ? PubstarNativeCustomConfig(
        layoutName: "pubstar_admob_native_big",
        advertiserTextViewId: "ad_advertiser",
        iconImageViewId: "ad_logo",
        titleTextViewId: "ad_headline",
        mediaContentViewGroupId: "ad_media",
        bodyTextViewId: "ad_body",
        callToActionButtonId: "ad_call_to_action",
        loadingViewId: "pubstar_shimmer_native_big",
        ctaColorHex: "#FFFFFF",
      )
    : PubstarNativeCustomConfig(
        layoutName: "AppAdmobNativeCustom",
        advertiserTextViewId: "1",
        iconImageViewId: "2",
        titleTextViewId: "3",
        mediaContentViewGroupId: "4",
        bodyTextViewId: "5",
        callToActionButtonId: "6",
        loadingViewId: "AppShimmerBanner",
        ctaColorHex: "#FFFFFF",
      );

PubstarAdView(
  adId: adId,
  type: PubstarAdType.native,
  nativeCustomConfig: customConfig,
  onError: (error) {
      // callback when ads error
  },
  onHide: (reward) {
      // callback when ad hide with reward option
  },
  onLoaded: () {
      // callback when ad loaded
  },
  onShowed: () {
      // callback when ad showed
  },
)
```

> `nativeCustomConfig` is only applied when `type: PubstarAdType.native`. The view ids and `layoutName` must match native resources defined in your host app.