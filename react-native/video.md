# Video (IMA)

Load and immediately show a Video (IMA) ad by ID.

Video ads are rendered with the same `PubstarAdView` component, using a video `type` and a `media` URL for the content stream.

### API

| Props           | Function                                                                       |
| --------------- | ------------------------------------------------------------------------------ |
| `adId`          | id of the Video ad                                                             |
| `type`          | kind of video ad. (`videoInStream`, `videoOutStream`)                          |
| `media`         | url of the media video to play                                                 |
| `size`          | size of ad View. (`small`, `medium`, `large`)                                  |
| `customConfig`  | optional `NativeCustomConfig` to render the ad inside a custom layout          |
| `style`         | React Native style object for the ad container                                 |
| `onLoaded`      | call when ad loaded                                                            |
| `onLoadedError` | call when load ad failed. return object type `ErrorCode`                        |
| `onShowed`      | call when ad showed                                                            |
| `onHide`        | call when ad closed. return object type `RewardModel`                          |
| `onShowedError` | call when show ad failed. return object type `ErrorCode`                        |

- `videoInStream`: the ad plays inside your own video content stream.
- `videoOutStream`: a standalone video ad placed in your layout (e.g. in a feed).

### Example

```js
import { PubstarAdView } from 'rtn-pubstar';

<PubstarAdView
    adId={adId}
    style={styles.ad}
    size="medium"
    type="videoOutStream"
    media="https://storage.googleapis.com/gvabox/media/samples/stock.mp4"
    onLoaded={() => {
        // callback when ad loaded
    }}
    onLoadedError={(errorCode) => {
        // callback when ad load error
    }}
    onShowed={() => {
        // callback when ad showed
    }}
    onHide={(reward) => {
        // callback when ad hide with reward option
    }}
    onShowedError={(errorCode) => {
        // callback when show error
    }}
/>
```

> You may also use the dedicated `PubstarAdVideoView` component (same props, `type="video"`). For in-stream / out-stream control, prefer `PubstarAdView` with `videoInStream` / `videoOutStream` as shown above.
