# SDK Integration

## Requirements

- iOS >= 13.0
- Android >= 23

## Installation

### Import from GitHub

1. Download the latest [`.unitypackage`](https://github.com/pubstar-io/PubStar-Unity-SDK/releases) release from GitHub.
2. Import the `.unitypackage` file by selecting the Unity menu option **Assets > Import package > Custom Package** and importing all items.

The package contains the C# API (`Assets/PubStar`) and the native bridges it calls into (`Assets/Plugins/Android/PubStar.androidlib` and `Assets/Plugins/iOS/PubStar`). Make sure all three are ticked in the import dialog.

### Upgrading to 1.6.2

Import the 1.6.2 `.unitypackage` over your existing installation; files are replaced in place.

- **From 1.5.0 – 1.6.1:** those packages shipped without the native bridges, so the Android and iOS parts were missing (or left over from an older install). Importing 1.6.2 adds them — nothing else to do.
- **If you first installed 1.3.1** — even if you have upgraded since — also delete `Assets/Plugins/Android/PubStar.androidlib/build/`. It is Gradle build output that the 1.3.1 package included by mistake, and importing a newer package does not remove it.

After upgrading, `Assets/Plugins/Android/PubStar.androidlib/build.gradle` should declare `io.pubstar.mobile:ads:1.6.2`.

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

  > **Required.** From **1.6.2**, the SDK stops at initialization if `io.pubstar.key` is missing or empty (`Missing required key 'io.pubstar.key' in Info.plist`), the same way Android always has. Earlier iOS versions silently fell back to a built-in debug App ID, so the app ran normally while every report it sent went to the wrong app. Use the App ID of your own app from the PubStar Dashboard.

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

