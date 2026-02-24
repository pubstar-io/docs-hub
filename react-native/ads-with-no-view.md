# Interstitial, Open and Rewarded

## loadAd(adId, callbackEvent)

Load PubStar ads by `Advertisement Id` to application.

### Event

ShowListener

| Callback                             | Function                                                   |
| ------------------------------------ | ---------------------------------------------------------- |
| `onLoadError`                        | call when load ad failed. return object type `ErrorCode`   |
| `onLoaded`                           | call when ad loaded                                        |

### Example

```js
Pubstar.loadAd(adId, {
    onLoadError: errorCode => {
        // callback when ad load error
    },
    onLoaded: () => {
        // callback when ad loaded
    },
})
```

## showAd(adId, callbackEvent)

Show ad had loaded before.


### Event

ShowListener

| Callback                | Function                                                                       |
| ----------------------- | ------------------------------------------------------------------------------ |
| `onAdHide`              | call when ad hidden by press close button. return object type `ErrorCode`      |
| `onAdShowed`            | call when ad showed                                                            |
| `onShowError`           | call when show ad failed. return object type `ErrorCode`                       |

### Example

```js
Pubstar.showAd(adId, {
    onAdHide: reward => {
        // callback when ad hide with reward option
    },
    onAdShowed: () => {
        // callback when ad showed
    },
    onShowError: errorCode => {
        // callback when error
    },
});

```

## loadAndShow(adId, callbackEvent)

Load and immediately show an ad by ID.

### Event

LoadAndShowListener

| Callback                | Function                                                                       |
| ----------------------- | ------------------------------------------------------------------------------ |
| `onLoadError`           | call when load ad failed. return object type `ErrorCode`                       |
| `onLoaded`              | call when ad loaded                                                            |
| `onAdHide`              | call when ad hidden by press close button. return object type `RewardModel`    |
| `onAdShowed`            | call when ad showed                                                            |
| `onShowError`           | call when show ad failed. return object type `ErrorCode`                       |

### Example

```js
Pubstar.loadAndShowAd(
    adId, {
        onLoadError: errorCode => {
            // callback when ad load error
        },
        onLoaded: () => {
            // callback when ad loaded
        },
        onAdHide: reward => {
            // callback when ad hide with reward option
        },
        onAdShowed: () => {
            // callback when ad showed
        },
        onShowError: errorCode => {
            // callback when show error
        },
    }
);

```

