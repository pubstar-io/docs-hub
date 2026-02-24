# Banner

Load and immediately show an Banner ads by ID.

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

let adRequest: AdRequest = BannerAdRequest.Builder(context: viewController!)
    .isAllowLoadNext(true) // allow load to cache after dismiss
    .withView(customView)
    .tag(.big)
    .adLoaderListener(adLoaderListener)
    .adShowedListener(adShowListener)
    .build()

PubStarAdManager.getAdController()
    .loadAndShow(
        key: "Your_Ads_Key",
        adRequest: adRequest
    )
```
