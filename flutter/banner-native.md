# Banner and Native

Load and immediately show an Banner ads or an Native ads by ID.

### API

| Props                   | Function                                                                                                   |
| ----------------------- | ---------------------------------------------------------------------------------------------------------- |
| `adId`                  | id of Banner or Native ad                                                                                  |
| `size`                  | size of ad View. (`small`, `medium`, `large`)                                                              |
| `type`                  | type of ad View. (`banner`, `native`)                                                                      |
| `mode`                  | mode of ad View (`onlyShow`, `loadAndShow`)                                                                |
| `onError`               | call when show ad failed. return object type `PubstarError`                                                |
| `onHide`                | call when ad hidden/closed (supports rewarded ads). Returns detailed PubstarReward object (type, amount) |
| `onLoaded`              | call when ad loaded                                                                                        |
| `onShowed`              | call when ad showed                                                                                        |

### Example

```dart
PubstarAdView(
  adId: adId,
  size: PubstarAdSize.small,
  type: PubstarAdType.banner,
  mode: PubstarAdViewMode.loadAndShow,
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