# Banner

Load and immediately show an Banner ads by ID.

## Event

`AdLoaderListener`
`AdShowedListener`

## API

**`BannerAdRequest.Builder`** provides a set of methods to configure the banner ad, including:

| Method                         | Type                    | Description                                                                                                                                                                      |
| ------------------------------ | ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `withView(view)`               | `View`                  | Passes a `View` that will be used to render the Banner Ad. This view serves as the container for the banner ad, allowing you to integrate it seamlessly into your app's layout.  |
| `backgroundResource(resource)` | `Drawable`              | Sets the background of the banner ad when loading. Accepts a `Drawable` resource to customize the background appearance during the loading phase.                                |
| `tag(tag)`                     | `BannerAdRequest.AdTag` | Sets the size of the banner ad. The tag parameter uses the Tag enum, allowing predefined options such as `Small`, `Medium`, `Big`, or `Full` for flexible layout configurations. |

### Implementation

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
