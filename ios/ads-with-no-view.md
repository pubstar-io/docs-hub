# Interstitial, Open and Rewarded

## load()

Load PubStar ads by `Advertisement Id` to application.

### Event

`AdLoaderListener`

| Callback   | Function                                                 |
| ---------- | -------------------------------------------------------- |
| `onError`  | call when load ad failed. return object type `ErrorCode` |
| `onLoaded` | call when ad loaded                                      |

### Example

```swift
var viewController: UIViewController = PubStarUtils.getHostingViewController()

// *** with no callback ***
PubStarAdManager.getAdController()
    .load(
        context: viewController,
        key: "Your_Ads_Key"
    )


// *** with callback ***
let adLoaderListener: AdLoaderListener = AdLoaderHandler {
    // callback when ad loaded
} onError: { code in
    // callback when ad load error
}

PubStarAdManager.getAdController()
    .load(
        context: viewController!,
        key: "Your_Ads_Key",
        adLoaderListener: adLoaderListener
    )
```

## show()

Show ad had loaded before.

### Event

`AdShowedListener`

| Callback     | Function                                                                                   |
| ------------ | ------------------------------------------------------------------------------------------ |
| `onAdHide`   | call when ad hidden/closed (supports rewarded ads). Returns detailed `RewardModel` object. |
| `onAdShowed` | call when ad showed                                                                        |
| `onError`    | call when show ad failed. return object type `ErrorCode`                                   |

### Example

```swift
var viewController: UIViewController = PubStarUtils.getHostingViewController()
@State private var customView: UIView?

// *** with no callback ***
PubStarAdManager.getAdController()
    .show(
        context: viewController!,
        key: "Your_Ads_Key",
        view: customView  // view has optional
    )

// *** with callback ***
let adShowListener: AdShowedListener = AdShowedHandler {
    // callback when ad showed
} onHide: { result in
    // callback when ad hide
} onError: { error in
    // callback when error
}

PubStarAdManager.getAdController()
    .show(
        context: viewController,
        key: "Your_Ads_Key",
        view: customView, // view has optional
        adShowedListener: adShowListener
    )
```

## loadAndShow()

Load and immediately show an ad by ID.

### Event

`AdLoaderListener`
`AdShowedListener`

### Example

```swift
var viewController: UIViewController = PubStarUtils.getHostingViewController()
@State private var customView: UIView?

// *** with no callback ***
PubStarAdManager.getAdController()
    .loadAndShow(
        context: viewController!,
        key: "Your_Ads_Key",
        view: customView  // view has optional
    )

// *** with callback ***
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

PubStarAdManager.getAdController()
    .loadAndShow(
        context: viewController!,
        key: "Your_Ads_Key",
        view: customView,
        adLoaderListener: adLoaderListener,
        adShowedListener: adShowListener
    )
```
