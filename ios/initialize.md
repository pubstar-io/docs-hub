# Initialize SDK

### initAd()
Initialization PubStar SDK. Initialization must be called once before loading or showing ads.

### Event

`InitAdListenerHandler`

| Callback  | Function                                                 |
| --------- | -------------------------------------------------------- |
| `onDone`  | call when PubStar SDK initializes successfully           |
| `onError` | call when load ad failed. return object type `ErrorCode` |

### Example

```swift
import Pubstar

struct ContentView: View {

    init() {
        PubStarAdManager.getInstance()
            .setInitAdListener(InitAdListenerHandler(
                onDone: {
                    print("PubStar", "onDone")
                },
                onError: { errorCode in
                    print("PubStar", "\(errorCode)")
                }
            ))
            .initAd()
    }


    var body: some View {
        VStack {
            Text("Hello, PubStar's publisher")
        }
    }
}
```
