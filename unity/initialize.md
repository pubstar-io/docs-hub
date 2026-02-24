# Initialize SDK

### Initialize(callback)
Initialization PubStar SDK. Initialization must be called once before loading or showing ads.

### Event

`Initialize`

| Callback  | Function                                                 |
| --------- | -------------------------------------------------------- |
| `onDone`  | call when PubStar SDK initializes successfully           |
| `onError` | call when load ad failed. return object type `ErrorCode` |


### Example

```C#
using PubStar.Io;

PubStar.Initialize(
    onDone: () =>
    {
        // callback when init done (ready to call load and show ad)
    },
    onError: code =>
    {
        // callback when init error
    }
);
```