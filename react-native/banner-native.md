# Banner and Native

Load and immediately show an Banner ads or an Native ads by ID.

### API

| Props                   | Function                                                                       |
| ----------------------- | ------------------------------------------------------------------------------ |
| `adId`                  | id of Banner or Native ad                                                      |
| `size`                  | size of ad View. (`small`, `medium`, `large`)                                  |
| `type`                  | kind of ad View. (`banner`, `native`)                                          |
| `onLoaded`              | call when ad loaded                                                            |
| `onLoadedError`         | call when load ad failed. return object type `ErrorCode`                       |
| `onShowed`              | call when ad showed                                                            |
| `onHide`                | call when ad closed return object type `RewardModel`                           |
| `onShowedError`         | call when show ad failed. return object type `ErrorCode`                       |

### Example

```js
<PubstarAdView
    adId={adId}
    style={styles.ad}
    size="medium"
    type="banner"
    onLoaded={() => {
        // callback when ad loaded
    }}
    onLoadedError={(errorCode) => {
        // callback when ad load error
    }}
    onShowed={() => {
        // callback when ad showed
    }}
    onHide={() => {
        // callback when ad hide with reward option
    }}
    onShowedError={(errorCode) => {
        // callback when show error
    }}
/>
```