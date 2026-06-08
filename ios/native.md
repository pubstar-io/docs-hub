# Native

Load and immediately show an Native ads by ID.

## Format

PubStar support tow types of native ads:

- Prebuilt Native: a Native Ad view provided directly by the SDK. The layout is pre-designed and optimized, and all ad assets are automatically rendered.
- Custom Native: a Native Ad view that you can customize. You can design the layout and style of the ad according to your needs, and the SDK will provide the necessary ad assets for you to render.

## Event

`AdLoaderListener`
`AdShowedListener`

## Prebuilt Native Ads

### API

**`NativeAdRequest.Builder`** provides a set of methods to configure the custom Native Ad, including:

| Method           | Type                       | Description                                                                                                                                                                                      |
| ---------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `sizeType(size)` | `NativeAdRequest.TypeSize` | Sets the size of the Native Ad. The size parameter uses the TypeSize enum, allowing predefined options such as `Medium`, `Big`, `Small`, `Full`, or `Custom` for flexible layout configurations. |
| `withView(view)` | `UIView`                   | Passes a `UIView` that will be used to render the Native Ad.                                                                                                                                     |

### Implementation

```swift
let adLoaderListener: AdLoaderListener = AdLoaderHandler {
    // callback when ad loaded
} onError: { code in
    // callback when ad load error
}

let adShowListener: AdShowedListener = AdShowedHandler {
    // callback when ad showed
} onHide: { result in
    // callback when ad hide
} onError: { error in
    // callback when error
}

let requestNative = NativeAdRequest.Builder(context: self)
    .sizeType(.Small)
    .withView(customView)
    .adLoaderListener(adLoaderListener)
    .adShowedListener(adShowListener)
    .build()

PubStarAdManager.getAdController()
    .loadAndShow(
        key: "Your_Ads_Key",
        adRequest: requestNative
    )
```

## Custom Native Ads

### API

**`NativeAdRequest.Builder`** provides a set of methods to configure the custom Native Ad, including:

| Method                                         | Type                       | Description                                                                                                                                                                                      |
| ---------------------------------------------- | -------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `sizeType(size)`                               | `NativeAdRequest.TypeSize` | Sets the size of the Native Ad. The size parameter uses the TypeSize enum, allowing predefined options such as `Medium`, `Big`, `Small`, `Full`, or `Custom` for flexible layout configurations. |
| `withView(view)`                               | `UIView`                   | Passes a `UIView` that will be used to render the Native Ad.                                                                                                                                     |
| `withNativeAdViewBinderCustom(view)` | `NativeAdViewBinder`       | Passes a `NativeAdViewBinder` object that defines the custom layout and mapping of ad assets for the Native Ad. This allows for a fully customized ad presentation.                              |

**`NativeAdViewBinder.Builder`** provides a set of methods to configure the custom layout and asset mapping for the Native Ad, including:

| Method                       | Type     | Description                                                                                                                                                                            |
| ---------------------------- | -------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `layoutId`                   | `String` | Sets the layout ID for the Native Ad. This allows for specifying a custom layout for the ad presentation.                                                                              |
| `setAdvertiserTextViewId`    | `Int`    | Sets the view ID for the advertiser text in the custom Native Ad layout. This maps the advertiser information to a specific view in the layout.                                        |
| `setIconImageViewId`         | `Int`    | Sets the view ID for the icon image in the custom Native Ad layout. This maps the ad's icon asset to a specific view in the layout.                                                    |
| `setTitleTextViewId`         | `Int`    | Sets the view ID for the title text in the custom Native Ad layout. This maps the ad's title asset to a specific view in the layout.                                                   |
| `setMediaContentViewGroupId` | `Int`    | Sets the view ID for the media content in the custom Native Ad layout. This maps the ad's media asset (such as video or image) to a specific view in the layout.                       |
| `setBodyTextViewId`          | `Int`    | Sets the view ID for the body text in the custom Native Ad layout. This maps the ad's body text asset to a specific view in the layout.                                                |
| `setCallToActionButtonId`    | `Int`    | Sets the view ID for the call-to-action button in the custom Native Ad layout. This maps the ad's call-to-action asset to a specific view in the layout.                               |
| `setLoadingView`             | `UIView` | Sets a loading view that will be displayed while the custom Native Ad is being loaded. This allows for a better user experience by showing a placeholder while the ad content is being |

### Implementation

```swift
func getPlaceholdderView() -> UIView? {
    let frameworkBundle = Bundle(for: NetworkAdsController.self)
    return UINib(nibName: "AppShimmerBanner", bundle: frameworkBundle)
        .instantiate(withOwner: nil, options: nil).first as? UIView
}

let adNetLoaderListener: AdLoaderListener = AdLoaderHandler {
    [weak self] in
    self?.showToast(message: "onLoaded")
} onError: { [weak self] code in
    self?.showToast(message: "onLoadedError: \(code.rawValue)")
}

let adNetShowListener: AdShowedListener = AdShowedHandler {
    [weak self] in
    self?.showToast(message: "onAdShowed")
} onHide: { [weak self] any in
    self?.showToast(message: "onAdHide: \(any?.type ?? "None")")
} onError: { [weak self] code in
    self?.showToast(message: "onShowedError: \(code.rawValue)")
}

guard let placeholderView = self.getPlaceholdderView() else {
    return
}

let customNativeAd = NativeAdViewBinder.Builder(
    layoutId: "AppNativeCustom"
)
.setAdvertiserTextViewId(7)
.setIconImageViewId(4)
.setTitleTextViewId(1)
.setMediaContentViewGroupId(6)
.setBodyTextViewId(2)
.setCallToActionButtonId(3)
.setLoadingView(placeholderView)
.build()

let nativeAdRequest = NativeAdRequest.Builder(context: self)
    .sizeType(.Custom)
    .withView(customView)
    .adLoaderListener(adNetLoaderListener)
    .adShowedListener(adNetShowListener)
    .withNativeAdViewBinderCustom(customNativeAd)
    .build()

pubStarAdController.loadAndShow(
    key: self.nativeAdId,
    adRequest: nativeAdRequest
)
```
