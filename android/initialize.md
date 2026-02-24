# Initialize SDK

### init(Context)
Initialization PubStar SDK. Initialization must be called once before loading or showing ads.

### Event

`InitAdListener`

| Callback  | Function                                                 |
| --------- | -------------------------------------------------------- |
| `onDone`  | call when PubStar SDK initializes successfully           |
| `onError` | call when load ad failed. return object type `ErrorCode` |

### Example

```kotlin

PubStarAdManager.getInstance()
    .setInitAdListener(object : InitAdListener {
        override fun onDone() {
            // callback when init done (ready to call load and show ad)
        }

        override fun onError(code: ErrorCode) {
            // callback when init error
        }
    }).init(context)
```
