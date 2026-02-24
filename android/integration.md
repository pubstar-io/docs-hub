# SDK Integration

## Requirements

- Android version >= 6.0
- API level >= 23

## Installation

Setting repository.

```bash
repositories {
  mavenCentral()
}
```

Dependency.

```bash
implementation 'io.pubstar.mobile:ads:1.3.1'
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
