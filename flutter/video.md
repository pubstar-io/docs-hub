# Video (IMA)

Load and immediately show a Video (IMA) ad by ID using `PubstarVideoAdView`.

### API

| Props                   | Function                                                                                                   |
| ----------------------- | ---------------------------------------------------------------------------------------------------------- |
| `adId`                  | id of Video ad                                                                                             | 
| `media`                 | url of media video                                                                                         |
| `type`                  | type of video ad. (`inStream`, `outStream`) — `PubStarVideoAdType`                                         |
| `onError`               | call when show ad failed. return object type `PubstarError`                                                |
| `onHide`                | call when ad hidden/closed (supports rewarded ads). Returns detailed PubstarReward object (type, amount) |
| `onLoaded`              | call when ad loaded                                                                                        |
| `onShowed`              | call when ad showed                                                                                        |


### Example

```dart
PubstarVideoAdView(
  adId: adId,
  media:
      'https://storage.googleapis.com/gvabox/media/samples/stock.mp4',
  type: PubStarVideoAdType.outStream,
  onError:
      (error) {
          // callback when ads error
      },
  onHide:
      (reward) {
          // callback when ad hide with reward option
      },
  onLoaded: () {
      // callback when ad loaded
  },
  onShowed: () {
      // callback when ad showed
  },
)
```

> `type` is required:
> - `PubStarVideoAdType.outStream`: a standalone video ad placed in your layout.
> - `PubStarVideoAdType.inStream`: the ad plays inside your own video content stream (`media`).
