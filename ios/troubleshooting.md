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
