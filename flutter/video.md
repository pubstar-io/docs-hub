# Video

Load and immediately show an Video ads by ID.

### API

| Props                   | Function                                                                                                   |
| ----------------------- | ---------------------------------------------------------------------------------------------------------- |
| `adId`                  | id of Video ad                                                                                             | 
| `media`                 | url of media video                                                                                         |
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