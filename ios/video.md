# Video

Load and immediately show a Video ad by ID.

### Format

PubStar supports two types of video ads:

- In Stream: Video ads that play within video content. Requires a MediaPlayer instance to manage video playback.
- Out Stream: Video ads that play outside of video content, typically within a native ad unit. Does not require a MediaPlayer instance. Including native video ads and interstitial, open and rewarded video ads.

## Event

`AdLoaderListener`
`AdShowedListener`

## In Stream Video Ads

### API

**`IMARequest.Builder`** provides a set of methods to configure the video ad, including:

| Method              | Type          | Description                                                                                                                                           |
| ------------------- | ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| `withMedia(player)` | `MediaPlayer` | Required for `inStream` format. Do not call this method if using `outStream`                                                                          |
| `withType(type)`    | `Enum`        | Receives the value `IMARequest.IMAType.inStream` or `IMARequest.IMAType.outStream`.                                                                   |
| `withSize(size)`    | `Enum`        | Required for `outStream` format. Do not call this method for `inStream`. Receives the value `IMARequest.IMASize.medium` or `IMARequest.IMASize.full`. |
| `withView(view)`    | `View`        | Required for `inStream` format. Do not call this method for `outStream`. Pass the view containing the ad.                                             |

### Implementation

```swift
private func createPlayerVideo() -> AVPlayer? {
    guard
        let url = URL(
            string:
                "https://storage.googleapis.com/gvabox/media/samples/stock.mp4"
        )
    else {
        return nil
    }

    let player = AVPlayer(url: url)
    player.isMuted = true
    player.actionAtItemEnd = .none

    return player
}

private func createVideoView(player: AVPlayer) -> UIView {
    let playerLayer: AVPlayerLayer = AVPlayerLayer(player: player)
    playerLayer.frame = videoContainerView.bounds
    playerLayer.videoGravity = .resizeAspect
    videoContainerView.layer.sublayers?.forEach {
        $0.removeFromSuperlayer()
    }
    videoContainerView.layer.addSublayer(playerLayer)

    return videoContainerView
}

@IBAction func didTapVideoInStream(_ sender: Any) {

    let adNetLoaderListener: AdLoaderListener = AdLoaderHandler {
        [weak self] in
        self?.showToast(message: "onLoaded")
    } onError: { [weak self] code in
        self?.showToast(message: "onLoadedError: \(code.rawValue)")
    }

    let adNetShowListener: AdShowedListener = AdShowedHandler {
        [weak self] in
        self?.showToast(message: "onAdShowed")
    } onHide: { [weak self] any in
        self?.showToast(message: "onAdHide: \(any?.type ?? "None")")
    } onError: { [weak self] code in
        self?.showToast(message: "onShowedError: \(code.rawValue)")
    }

    guard let player = self.createPlayerVideo() else {
        return
    }
    let videoView = self.createVideoView(player: player)
    player.play()

    let requestVideo = IMARequest.Builder(context: self)
        .withView(customView)
        .withType(.inStream)
        .withMedia(player)
        .adLoaderListener(adNetLoaderListener)
        .adShowedListener(adNetShowListener)
        .build()

    pubStarAdController.loadAndShow(
        key: self.videoAdId,
        adRequest: requestVideo
    )
}
```

## Out Stream Video Ads

### API

**`IMARequest.Builder`** provides a set of methods to configure the video ad, including:

| Enum                 | Value               | Description                                                             |
| -------------------- | ------------------- | ----------------------------------------------------------------------- |
| `IMARequest.IMASize` | `medium` and `full` | `medium` for Native ads, `full` for Interstitial, Open and Rewarded ads |

### Implementation

```swift
@IBAction func didTapVideoOutStreamNative(_ sender: Any) {
    let adNetLoaderListener: AdLoaderListener = AdLoaderHandler {
        [weak self] in
        self?.showToast(message: "onLoaded")
    } onError: { [weak self] code in
        self?.showToast(message: "onLoadedError: \(code.rawValue)")
    }

    let adNetShowListener: AdShowedListener = AdShowedHandler {
        [weak self] in
        self?.showToast(message: "onAdShowed")
    } onHide: { [weak self] any in
        self?.showToast(message: "onAdHide: \(any?.type ?? "None")")
    } onError: { [weak self] code in
        self?.showToast(message: "onShowedError: \(code.rawValue)")
    }

    let requestVideo = IMARequest.Builder(context: self)
        .withView(customView)
        .withType(.outStream)
        .withSize(.medium)
        .adLoaderListener(adNetLoaderListener)
        .adShowedListener(adNetShowListener)
        .build()

    pubStarAdController.loadAndShow(
        key: self.videoAdId,
        adRequest: requestVideo
    )
}
```
