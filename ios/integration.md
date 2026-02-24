# SDK Integration

## Requirements

- iOS >= 13.0
- Swift >= 4.0

## Installation

### CocoaPods

1. If you haven't set up CocoaPods, run `pod init` in your project directory.
2. In your Podfile, add PubStar dependencies:

   ```ruby
   target 'YourAppName' do
       # Add this line to use the latest version of PubStar SDK
       pod 'Pubstar'

   end
   ```

3. Add `use_frameworks!` inside your app target in the Podfile:

   ```ruby
   platform :ios, '13.0'

   target 'YourAppName' do
       use_frameworks! # <-- Must be add this line

       pod 'Pubstar'
   end

   ```

4. Install the dependencies using `pod install`.
5. Open your project in Xcode with the `.xcworkspace` file.

## Configuration

### 1. Update your Info.plist

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
