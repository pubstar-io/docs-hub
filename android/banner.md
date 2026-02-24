# Banner

Load and immediately show an Banner ads by ID.

### Event

`AdLoaderListener`
`AdShowedListener`

### Example

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
