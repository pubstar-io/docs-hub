# AdMob Mediation Integration

This guide explains how to connect **PubStar** to **Google AdMob Mediation** on iOS using custom events.

> **AdMob must already be integrated in your iOS app**
>
> PubStar runs inside AdMob mediation waterfall. Finish base AdMob setup first (Google Mobile Ads SDK, App ID, ad units, test ads), then add PubStar SDK and adapter.
>
> **Recommended guides:**
> - [AdMob iOS quick start](https://developers.google.com/admob/ios/quick-start)
> - [AdMob mediation overview (iOS)](https://developers.google.com/admob/ios/mediation)
> - [PubStar iOS SDK integration](integration.md)

## Requirements

- iOS 13.0+
- Xcode 15+ recommended
- AdMob account and working GMA SDK integration on iOS
- PubStar App ID from [PubStar Dashboard](https://pubstar.io/)
- PubStar placement keys per ad format

## Installation (CocoaPods)

### Podfile

```ruby
platform :ios, '13.0'

target 'YourAppTarget' do
  use_frameworks! :linkage => :static

  pod 'Pubstar', '~> 1.6.0'
  pod 'PubStarMediationAdmobAdapter', '~> 1.6.0'
end
```

Run `pod install`, then open `.xcworkspace`.

## Configuration

### 1. Add PubStar App ID to Info.plist

Please refer to the [Info.plist Configuration Guide](integration.md#1-update-your-infoplist) to set up your PubStar App ID.

---

## AdMob Mediation Console Setup (iOS)

1. Create mediation group per format.
2. Choose platform **iOS**.
3. Add PubStar as **Custom Event**.
4. Use class name and parameter below.

### Mediation group setup

#### Step 1: Create Mediation Group

In AdMob, go to `Mediation` and click `Create Mediation Group`:

<figure>
  <img src="../assets/admob-setup/step1-create-mediation-group.png" alt="Create Mediation Group" loading="lazy" />
  <figcaption>Create Mediation Group.</figcaption>
</figure>

Select ad format, choose **iOS** platform, then continue and set group properties.

<figure>
  <img src="../assets/admob-setup/step1-mediation-group-properties.png" alt="Mediation group properties" loading="lazy" />
  <figcaption>Mediation group properties.</figcaption>
</figure>

Click **ADD AD UNITS** and attach iOS ad units:

<figure>
  <img src="../assets/admob-setup/step1-add-ad-units.png" alt="Add ad units" loading="lazy" />
  <figcaption>Add ad units.</figcaption>
</figure>

#### Step 2: Add Custom Events

Add one or more PubStar custom events (for example by eCPM tier):

<figure>
  <img src="../assets/admob-setup/step2-add-ad-sources.png" alt="Add ad sources" loading="lazy" />
  <figcaption>Add ad sources.</figcaption>
</figure>

Click **ADD CUSTOM EVENT**, set label and eCPM:

<figure>
  <img src="../assets/admob-setup/step2-custom-event-label-ecpm.png" alt="Custom event label and eCPM" loading="lazy" />
  <figcaption>Custom event label and eCPM.</figcaption>
</figure>

### Custom event values

- **Class Name**

  ```
  PubStarGADMediationAdapter
  ```

  If your project requires module-qualified Swift name, use: `PubStarMediationAdmobAdapter.PubStarGADMediationAdapter`.

- **Parameter** — PubStar placement key (plain text), for example: `1233/99228313580` (banner)

<figure>
  <img src="../assets/admob-setup/step2-custom-event-class-parameter.png" alt="Class Name and Parameter" loading="lazy" />
  <figcaption>Class Name and Parameter.</figcaption>
</figure>

<figure>
  <img src="../assets/admob-setup/step2-custom-events-list.png" alt="Custom events list" loading="lazy" />
  <figcaption>Custom events list.</figcaption>
</figure>

### Supported ad formats

| AdMob format | Test placement key |
| ------------ | ------------------ |
| Banner       | `1233/99228313580` |
| Interstitial | `1233/99228313582` |
| Rewarded     | `1233/99228313584` |
| App Open     | `1233/99228313583` |

These test keys pair with `pub-app-id-1233`. Use production keys before release. **Native Advanced** is not listed: native mediation only works with a **real native placement key** from your PubStar Dashboard (test native keys are not supported).

### Validation checklist

- `Pubstar` and `PubStarMediationAdmobAdapter` pods are installed.
- `io.pubstar.key` exists in app `Info.plist`.
- AdMob mediation group platform is iOS.
- Class Name is correct and Parameter is not empty.
- Placement key format matches the ad format.

### Troubleshooting

**No callback to custom event:** verify waterfall order/eCPM and class name spelling.

**No fill:** verify placement key + format mapping with PubStar support.

**Native Advanced not loading / no fill** — PubStar native in AdMob mediation **only works with a real native placement key** from your PubStar Dashboard for this app. Do **not** use shared test native keys (for example `1233/99228313581` with `pub-app-id-1233`); they will not serve. Create or copy your production native placement key, set it as the custom event **Parameter**, and confirm the mediation group format is Native Advanced on iOS.

**Recent console changes:** wait 10–15 minutes and relaunch app before retest.
