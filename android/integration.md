# SDK Integration

## Requirements

- Android >= 23

## Installation

Setting repository.

```bash
repositories {
  mavenCentral()
}
```

Dependency.

```bash
implementation 'io.pubstar.mobile:ads:1.5.1'
```

### Ad Network Adapters (Optional)

PubStar supports various third-party ad networks to maximize your fill rate. We highly recommend adopting a modular approach: **only install the adapters for the networks you actively use** to keep your app size optimized.

Add the desired adapters to your Podfile alongside the core PubStar SDK:

```ruby
# Facebook
implementation 'io.pubstar.facebook.adapter:ads:1.5.1'

# Mintegral
implementation 'io.pubstar.mintegral.adapter:ads:1.5.1'

# Pangle
implementation 'io.pubstar.pangle.adapter:ads:1.5.1'

# InMobi
implementation 'io.pubstar.inmobi.adapter:ads:1.5.1'

# Appodeal
implementation 'io.pubstar.appodeal.adapter:ads:1.5.1'

# Yandex
implementation 'io.pubstar.yandex.adapter:ads:1.5.1'

# Vungle
implementation 'io.pubstar.vungle.adapter:ads:1.5.1'

# OfferWall
implementation 'io.pubstar.offerwall.adapter:ads:1.5.1'

# Unity
implementation 'io.pubstar.unity.adapter:ads:1.5.1'
```

## Configuration

### 1. Update your AndroidManifest

Open `AndroidManifest.xml` and add inside `<application>`:

- A `io.pubstar.key` key with a string value of your PubStar ad ID [found in the PubStar Dashboard](https://pubstar.io/).

```bash
<meta-data
  android:name="io.pubstar.key"
  android:value="Your PubStar app ID" />
```

Replace `Your PubStar app ID` with your actual [PubStar App ID](https://pubstar.io/).  
