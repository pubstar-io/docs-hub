# Interstitial, Open and Rewarded

## Load(adId, callbackEvent)

Load PubStar ads by `Advertisement Id` to application.

#### Event

LoadListener

| Callback   | Function                                    |
| ---------- | ------------------------------------------- |
| `onError`  | call when load ad failed. return Error code |
| `onLoaded` | call when ad loaded                         |

#### Example

```C#
PubStar.Load(
  "Ads ID",
  onLoaded: () => 
  {
    // callback when ad loaded
  },
  onError: err => 
  {
    // callback when ad load error
  }
);
```

## Show(adId, callbackEvent)

Show ad had loaded before.

#### Event

ShowListener

| Callback   | Function                                                                                                        |
| ---------- | --------------------------------------------------------------------------------------------------------------- |
| `onHidden`   | call when ad hidden/closed (supports rewarded ads). Returns detailed `PubstarReward` object (`type`, `amount`). |
| `onShowed` | call when ad showed                                                                                             |
| `onError`  | call when show ad failed. return Error code                                                                     |

#### Example

```C#
PubStar.Show(
  "Ads ID",
  onShowed: () => 
  {
      // callback when ad showed
  },
  onHidden: payloadJson => 
  {
      // callback when ad hide with reward option
  },
  onError: err => 
  {
      // callback when error
  }
);
```

## LoadAndShow(adId, callbackEvent)

Load and immediately show an ad by ID.

#### Event

| Callback      | Function                                                                                                             |
| ------------- | -------------------------------------------------------------------------------------------------------------------- |
| `onLoaded`    | call when ad loaded                                                                                                  |
| `onLoadError` | call when load ad failed. return Error code                                                                          |
| `onShowed`    | call when ad showed                                                                                                  |
| `onHidden`    | call when ad hidden/closed (supports rewarded ads). Returns detailed `PubstarReward` JSON string (`type`, `amount`). |
| `onShowError` | call when show ad failed. return Error code                                                                          |

#### Example

```C#
PubStar.LoadAndShow(
  "Ads ID",
  onLoaded: () => 
  {
    // callback when ad loaded   
  },
  onLoadError: err => 
  {
    // callback when load ads error   
  },
  onShowed: () => 
  {
    // callback when ad showed   
  },
  onHidden: payloadJson => 
  {
    // callback when ad hide with reward option   
  },
  onShowError: err => 
  {
    // callback when show ads error      
  }
);
```

