# Native

Load and immediately show an Native ads by ID.

### Event

`AdLoaderListener`
`AdShowedListener`

### Example

```swift
var viewController: UIViewController = PubStarUtils.getHostingViewController()

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

let requestNative = NativeAdRequest.Builder(context: viewController!)
    .sizeType(.Small)
    .withView(customView)
    .adLoaderListener(adLoaderListener)
    .adShowedListener(adShowListener)
    .build()

PubStarAdManager.getAdController()
    .loadAndShow(
        key: "Your_Ads_Key",
        adRequest: adRequest
    )
```
