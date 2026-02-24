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


```kotlin
val pubStarAdController by lazy {
    PubStarAdManager.getAdController()
}
// with no callback
pubStarAdController.load(context,"id")

// with callback
val adNetLoaderListener = object : AdLoaderListener {
    override fun onLoaded() {
        // callback when ad loaded
    }

    override fun onError(code: ErrorCode) {
        // callback when ad load code
    }
}

pubStarAdController.load(context,"id",adNetLoaderListener)

// with builder
val adNetLoaderListener = object : AdLoaderListener {
    override fun onLoaded() {
        // callback when ad loaded
    }

    override fun onError(code: ErrorCode) {
        // callback when ad load error
    }

}
pubStarAdController.load("id", AdRequest.Builder(context)
    .isAllowLoadNext(true) // allow load to cache after dismiss
    .adLoaderListener(adNetLoaderListener)
    .build())
       
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


```kotlin
val pubStarAdController by lazy {
    PubStarAdManager.getAdController()
}
// with no callback
pubStarAdController.show(context,"id",view) // view has optional

// with callback
val adNetShowListener = object : AdShowedListener {
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
    
pubStarAdController.show(context,"id",view,adNetShowListener) // view has optional

// with builder
val adNetShowListener = object : AdShowedListener {
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
pubStarAdController.show("id", AdRequest.Builder(context)
    .isAllowLoadNext(true) // allow load to cache after dismiss
    .adShowedListener(adNetShowListener)
    .withView(view) // view has optional
    .build())       
```

## loadAndShow()

Load and immediately show an ad by ID.

### Event

`AdLoaderListener`
`AdShowedListener`

### Example

```kotlin
val pubStarAdController by lazy {
    PubStarAdManager.getAdController()
}
// with no callback
pubStarAdController.loadAndShow(context,"id",view) // view has optional

// with callback
val adNetShowListener = object : AdShowedListener {
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

val adNetLoaderListener = object : AdLoaderListener {
        override fun onLoaded() {
            // callback when ad loaded
        }

        override fun onError(code: ErrorCode) {
            // callback when ad load error
        }
}    
    
pubStarAdController.loadAndShow(context,"id",view,adNetLoaderListener,adNetShowListener) // view has optional

// with builder
val adNetShowListener = object : AdShowedListener {
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
val adNetLoaderListener = object : AdLoaderListener {
    override fun onLoaded() {
        // callback when ad loaded
    }

    override fun onError(code: ErrorCode) {
        // callback when ad load code
    }

}       
pubStarAdController.loadAndShow("id", AdRequest.Builder(context)
    .isAllowLoadNext(true) // allow load to cache after dismiss
    .adShowedListener(adNetShowListener)
    .adLoaderListener(adNetLoaderListener)                
    .withView(view) // view has optional
    .build())       
```
