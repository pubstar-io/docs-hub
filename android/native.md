# Native

Load and immediately show an Native ads by ID.

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

val requestNative = NativeAdRequest.Builder(context)
    .sizeType(NativeAdRequest.Type.Big) // change size of native has "Big" , "Medium" ,"Small"
    .colorCTA(ResourcesCompat.getColor(resources,R.color.purple_200,null)) // change color loading & button CTA
    .backgroundResource(ResourcesCompat.getDrawable(resources,R.drawable.custom_bg_color,null)) // change color background
    .withView(view) 
    .adLoaderListener(adLoaderListener)
    .adShowedListener(adShowListener)
    .build()

  
pubStarAdController.loadAndShow("id", requestNative)       
```