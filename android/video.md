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

| Method              | Type          | Description                                                                                                                                      |
| ------------------- | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| `withMedia(player)` | `MediaPlayer` | Required for `IN_STREAM` format. Do not call this method if using `OUT_STREAM`                                                                   |
| `withType(type)`    | `Enum`        | Receives the value `IMARequest.Type.IN_STREAM` or `IMARequest.Type.OUT_STREAM`.                                                                  |
| `withSize(size)`    | `Enum`        | Required for `OUT_STREAM` format. Do not call this method for `IN_STREAM`. Receives the value `IMARequest.Size.Medium` or `IMARequest.Size.Full`. |
| `withView(view)`    | `View`        | Required for `IN_STREAM` format. Do not call this method for `OUT_STREAM`. Pass the view containing the ad.                                      |

### Implementation

```kotlin
fun createVideo(buttonBinding: Button, callback: (mediaPlayer: MediaPlayer) -> Unit) {
    val videoView = VideoView(this)
    binding.nativeAd.removeAllViews()
    binding.nativeAd.addView(videoView)

    buttonBinding.isEnabled = false

    videoView.setVideoPath("https://storage.googleapis.com/gvabox/media/samples/stock.mp4")
    videoView.setOnCompletionListener({
        binding.nativeAd.removeAllViews()
    })

    videoView.setOnPreparedListener { mp ->
        mp.isLooping = false
        videoView.start()

        buttonBinding.isEnabled = true

        callback(mp)
    }
}

this.createVideo(
    buttonBinding = binding.btnVideoInStream,
    callback = { player ->
        val requestVideo = IMARequest.Builder(this)
            .withView(binding.nativeAd)
            .withType(IMARequest.Type.IN_STREAM)
            .withMedia(player)
            .adLoaderListener(adNetLoaderListener)
            .adShowedListener(adNetShowListener)
            .build()

        pubStarAdController.loadAndShow(videoAdKey, requestVideo)
    }
)

```

## Out Stream Video Ads

### API

**`IMARequest.Builder`** provides a set of methods to configure the video ad, including:

| Enum              | Value            | Description                                                             |
| ----------------- | ---------------- | ----------------------------------------------------------------------- |
| `IMARequest.Size` | `Medium` and `Full` | `Medium` for Native ads, `Full` for Interstitial, Open and Rewarded ads |

### Implementation

```kotlin
val requestVideo = IMARequest.Builder(this)
    .withSize(IMARequest.Size.Medium)
    .withType(IMARequest.Type.OUT_STREAM)
    .adLoaderListener(adNetLoaderListener)
    .adShowedListener(adNetShowListener)
    .build()

pubStarAdController.loadAndShow(videoAdKey, requestVideo)
```
