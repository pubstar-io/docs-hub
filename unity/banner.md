# Banner

Load and immediately show an Banner ads by ID.

### API

| Props      | Function                                                                                                             |
| ------------- | -------------------------------------------------------------------------------------------------------------------- |
| `OnLoaded`    | call when ad loaded                                                                                                  |
| `OnLoadError` | call when load ad failed. return Error code                                                                          |
| `OnShowed`    | call when ad showed                                                                                                  |
| `OnHidden`    | call when ad hidden/closed (supports rewarded ads). Returns detailed `PubstarReward` JSON string (`type`, `amount`). |
| `OnShowError` | call when show ad failed. return Error code                                                                          |

### Example

```C#
BannerView banner = new BannerView(
    bannerAdID,
    AdSize.Medium,
    AdPosition.Center);
banner.OnLoaded += () =>
{
    // callback when ad loaded
};
banner.OnShowed += () =>
{
    // callback when ad showed
};
banner.Show();
```