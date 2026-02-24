# Interstitial, Open and Rewarded

### loadAd(adId, callbackEvent)

Load PubStar ads by `Advertisement Id` to application.

### Event

`LoadListener`

| Callback   | Function                                                    |
| ---------- | ----------------------------------------------------------- |
| `onError`  | call when load ad failed. return object type `PubstarError` |
| `onLoaded` | call when ad loaded                                         |

### Example

```dart
PubstarIo.loadAd(
  adId,
  LoadListener(
    onLoaded: () {
        // callback when ad loaded
    },
    onError:
        (error) {
            // callback when ad load error
        },
  ),
);
```

## showAd(adId, callbackEvent)

Show ad had loaded before.

### Event

`ShowListener`

| Callback   | Function                                                                                                        |
| ---------- | --------------------------------------------------------------------------------------------------------------- |
| `onHide`   | call when ad hidden/closed (supports rewarded ads). Returns detailed `PubstarReward` object (`type`, `amount`). |
| `onShowed` | call when ad showed                                                                                             |
| `onError`  | call when show ad failed. return object type `PubstarError`                                                     |

### Example

```dart
PubstarIo.showAd(
  adId,
  ShowListener(
    onShowed: () {
        // callback when ad showed
    },
    onHide:
        (reward) {
            // callback when ad hide with reward option
        },
    onError:
        (error) {
            // callback when error
        },
  ),
);
```

## loadAndShow(adId, callbackEvent)

Load and immediately show an ad by ID.

### Event

LoadAndShowNoViewListener

| Callback             | Function                                                                                                          |
| -------------------- | ------------------------------------------------------------------------------------------------------------------|
| `onLoaded`           | call when ad loaded                                                                                               |
| `onShowed`           | call when ad showed                                                                                               |
| `onHide`             | call when ad hidden/closed (supports rewarded ads). Returns detailed `PubstarReward` object (`type`, `amount`). |
| `onError`            | call when show ad failed. return object type `PubstarError`                                                       |

### Example

```dart
PubstarIo.loadAndShow(
  adId,
  LoadAndShowNoViewListener(
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
  ),
);
```
