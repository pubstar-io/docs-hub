# Native

Load and immediately show a Native ad by ID.

### API

| Props      | Function                                                                                                             |
| ------------- | -------------------------------------------------------------------------------------------------------------------- |
| `OnLoaded`    | call when ad loaded                                                                                                  |
| `OnLoadError` | call when load ad failed. return Error code                                                                          |
| `OnShowed`    | call when ad showed                                                                                                  |
| `OnHidden`    | call when ad hidden/closed (supports rewarded ads). Returns detailed `PubstarReward` JSON string (`type`, `amount`). |
| `OnShowError` | call when show ad failed. return Error code                                                                          |

### Example

```C#
NativeView native = new NativeView(
    nativeAdID,
    AdSize.Medium,
    AdPosition.Bottom);
native.OnLoaded += () =>
{
    // callback when ad loaded
};
native.OnShowed += () =>
{
    // callback when ad showed
};
native.Show();
```

## Custom Native

Render a Native ad inside **your own layout** instead of the default Pubstar native template.

Build the layout natively (an XML layout on Android / a view on iOS), map your view IDs to the ad fields with `NativeCustomConfig.Builder`, then pass the result (a JSON string) to `NativeView`.

### NativeCustomConfig.Builder

| Method                              | Function                                                                  |
| ----------------------------------- | ------------------------------------------------------------------------- |
| `Builder(layoutName)`               | name of your native layout (Android XML layout name / iOS view identifier) |
| `SetAdvertiserTextViewId(id)`       | view id for the advertiser name text                                      |
| `SetIconImageViewId(id)`            | view id for the advertiser icon image                                     |
| `SetTitleTextViewId(id)`            | view id for the headline / title text                                     |
| `SetMediaContentViewGroupId(id)`    | view id for the media content container                                   |
| `SetBodyTextViewId(id)`             | view id for the body / description text                                   |
| `SetCallToActionButtonId(id)`       | view id for the call-to-action button                                     |
| `SetLoadingViewName(name)`          | name of the loading / shimmer view shown while the ad loads               |
| `SetCtaColorHex(hex)`               | hex color for the call-to-action button (e.g. `#FFFFFF`)                  |
| `Build()`                           | returns the config as a JSON string to pass to `NativeView`               |

### Example

```C#
string customConfig = new NativeCustomConfig.Builder("pubstar_admob_native_big")
    .SetAdvertiserTextViewId("ad_advertiser")
    .SetIconImageViewId("ad_logo")
    .SetTitleTextViewId("ad_headline")
    .SetMediaContentViewGroupId("ad_media")
    .SetBodyTextViewId("ad_body")
    .SetCallToActionButtonId("ad_call_to_action")
    .SetLoadingViewName("pubstar_shimmer_native_big")
    .SetCtaColorHex("#FFFFFF")
    .Build();

NativeView native = new NativeView(
    nativeAdID,
    AdSize.Medium,
    AdPosition.Bottom,
    customConfig);
native.OnLoaded += () =>
{
    // callback when ad loaded
};
native.OnShowed += () =>
{
    // callback when ad showed
};
native.Show();
```

> The view IDs and layout name must match native resources defined in your exported app. The media view must be a container (ViewGroup on Android / UIView on iOS) — the SDK injects the network's media view into it.