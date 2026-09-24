# Troubleshooting problems

Here's how to troubleshoot when integrating PubStar SDK in your project

### 1. Operation not permitted error

When you build your project, you may see the error ` ... : Operation not permitted`. This means that your project entered a `User Script Sandbox` mode. To fix this, you need to disable the `User Script Sandbox` mode in your project settings. Following this instrusction:

- Open `Your_Project` in Xcode.
- Select `Your_Project` in the Project Navigator.
- Select `Your_Target`.
- Go to the `Build Settings` tab.
- Expand the `Build Options` section.
- Set the `User Script Sandbox` option to `No`.

### 2. When runtime, you are facing error `Library not loaded: @rpath/PrebidMobile.framework/PrebidMobile`

Enable use_frameworks! in your Podfile.

**Required Fix**
Update your `Podfile` as follows:

```ruby
platform :ios, '13.0'

target 'YourAppName' do
  use_frameworks!

  pod 'Pubstar'
end
```

Then run:

```ruby
pod install
```

Clean and rebuild the project before running again.

### 3. The app crashes at launch with `Missing required key 'io.pubstar.key' in Info.plist`

From **1.6.2**, the SDK requires your PubStar App ID and stops at initialization when it is missing or empty. It calls your init listener's `onError` with `INIT_ERROR` first, then ends the process with this message. Earlier versions did not fail here: they fell back to a built-in debug App ID, so the app ran but every report it sent — sessions and crashes included — went to the debug app instead of yours.

**Required Fix**
Add your App ID to `Info.plist`:

```xml
<key>io.pubstar.key</key>
<string>pub-app-id-XXXX</string>
```

Replace `pub-app-id-XXXX` with the App ID shown for your app in the PubStar Dashboard, then rebuild.
