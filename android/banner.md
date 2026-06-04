# Banner

Load and immediately show an Banner ads by ID.

## Event

`AdLoaderListener`
`AdShowedListener`

## API

**`BannerAdRequest.Builder`** provides a set of methods to configure the banner ad, including:

| Method                         | Type                    | Description                                                                                                                                                                      |
| ------------------------------ | ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `colorCTA(color)`              | `Color`                 | Sets the color of the Call To Action (CTA) button. Accepts a `Color` object to customize the appearance of the CTA button.                                                       |
| `withView(view)`               | `View`                  | Passes a `View` that will be used to render the Banner Ad. This view serves as the container for the banner ad, allowing you to integrate it seamlessly into your app's layout.  |
| `backgroundResource(resource)` | `Drawable`              | Sets the background of the banner ad when loading. Accepts a `Drawable` resource to customize the background appearance during the loading phase.                                |
| `withTag(tag)`                 | `BannerAdRequest.AdTag` | Sets the size of the banner ad. The tag parameter uses the Tag enum, allowing predefined options such as `Small`, `Medium`, `Big`, or `Full` for flexible layout configurations. |

### Implementation

```kotlin
val pubStarAdController by lazy {
    PubStarAdManager.getAdController()
}
val adShowListener = object : AdShowedListener {
    override fun onAdShowed() {
        // callback when ad showed
    }

    override fun onAdHide(any: RewardModel?) {
        // callback when ad hide with reward option
    }

    override fun onError(code: ErrorCode) {
        // callback when error
    }
}
val adLoaderListener = object : AdLoaderListener {
        override fun onLoaded() {
            // callback when ad loaded
        }

        override fun onError(code: ErrorCode) {
            // callback when ad load code
        }

}

val requestBanner = BannerAdRequest.Builder(context)
    .colorCTA(ResourcesCompat.getColor(resources,R.color.purple_200,null)) // change color loading button CTA
    .withView(view)
    .backgroundResource(ResourcesCompat.getDrawable(resources,R.drawable.custom_bg_color,null)) // change color background when loading
    .adLoaderListener(adLoaderListener)
    .adShowedListener(adShowListener)
    .build()


pubStarAdController.loadAndShow("id", requestBanner)
```
