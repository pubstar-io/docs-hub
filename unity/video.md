# Video (IMA)

Load and immediately show a Video (IMA) ad by ID using `VideoView`.

Pass the content video URL via `media` when creating the view.

### API

| Props         | Function                                                                                                             |
| ------------- | -------------------------------------------------------------------------------------------------------------------- |
| `media`       | URL of the media video to play                                                                                       |
| `OnLoaded`    | call when ad loaded                                                                                                  |
| `OnLoadError` | call when load ad failed. return Error code                                                                          |
| `OnShowed`    | call when ad showed                                                                                                  |
| `OnHidden`    | call when ad hidden/closed (supports rewarded ads). Returns detailed `PubstarReward` JSON string (`type`, `amount`). |
| `OnShowError` | call when show ad failed. return Error code                                                                          |

### Example

```C#
VideoView video = new VideoView(
    videoAdID,
    AdSize.Large,
    AdPosition.Center,
    media: "https://storage.googleapis.com/gvabox/media/samples/stock.mp4");
video.OnLoaded += () =>
{
    // callback when ad loaded
};
video.OnShowed += () =>
{
    // callback when ad showed
};
video.Show();
```
