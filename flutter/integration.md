# SDK Integration

## Requirements

- Min Dart SDK >= 3.7
- iOS >= 13.0
- Android >= 23

## Installation

Add the dependency in your `pubspec.yaml` file:

```yaml
dependencies:
  pubstar_io
```

Then run:

```bash
flutter pub get
```

## Configuration

### iOS

#### 1. Configure Pod.
1. Navigate to your iOS project directory.

2. Install the dependencies using pod install.

```bash
pod install
```

3. Open your project in Xcode with the .xcworkspace file.

#### 2. Update your Info.plist

Update your app's Info.plist file to add several keys:

- A GADApplicationIdentifier key with a string value of your AdMob app ID [found in the AdMob UI](https://support.google.com/admob/answer/7356431).

- A `io.pubstar.key` key with a string value of your PubStar ad ID [found in the PubStar Dashboard](https://pubstar.io/).

- SKAdNetworkItems in Google AdMob refers to the necessary configuration within your iOS app's Info.plist file to support Apple's SKAdNetwork for conversion tracking, particularly when using the Google Mobile Ads SDK for AdMob [found in the AdMob privacy](https://developers.google.com/admob/ios/privacy/strategies).


```xml
<key>GADApplicationIdentifier</key>
<string>Your AdMob app ID</string>
<key>SKAdNetworkItems</key>
	<array>
		<dict>
			<key>SKAdNetworkIdentifier</key>
			<string>cstr6suwn9.skadnetwork</string>
		</dict>

        ...

        <dict>
			<key>SKAdNetworkIdentifier</key>
			<string>3qcr597p9d.skadnetwork</string>
		</dict>
    </array>
<key>NSUserTrackingUsageDescription</key>
<string>We use your data to show personalized ads and improve your experience.</string>
<key>io.pubstar.key</key>
<string>Your PubStar app ID</string>
```

### Android

#### 1. Add PubStar Key to AndroidManifest.
Open `AndroidManifest.xml` and add inside `<application>`:

- A `io.pubstar.key` key with a string value of your PubStar ad ID [found in the PubStar Dashboard](https://pubstar.io/).

```bash
<meta-data
  android:name="io.pubstar.key"
  android:value="Your PubStar app ID" />
```

Replace `Your PubStar app ID` with your actual [PubStar App ID](https://pubstar.io/).  