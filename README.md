# What is PubStar?

PubStar Mobile Ads SDK is a comprehensive monetization solution that enables developers to seamlessly integrate high-performance ad formats into mobile applications across multiple platforms:

- [iOS](https://cocoapods.org/pods/Pubstar)
- [Android](https://central.sonatype.com/artifact/io.pubstar.mobile/ads)
- [React Native](https://www.npmjs.com/package/rtn-pubstar)
- [Flutter](https://pub.dev/packages/pubstar_io)
- [Unity](https://openupm.com/packages/io.pubstar.unity/)

The SDK provides a unified and flexible API for loading, displaying, and managing ads while ensuring a non-intrusive and optimized user experience.

Beyond traditional ad SDK functionality, PubStar integrates Prebid and Google Ad Manager (GAM) to create a competitive bidding environment between demand sources.

This means:

- Multiple demand partners compete in real time.
- The highest paying advertiser in a given region wins.
- Developers automatically maximize yield without manual mediation optimization.

PubStar combines direct demand, programmatic bidding, and header bidding technology into a single unified SDK.

# Supported Ad Formats

PubStar supports the following ad formats:

- Banner Ads
- Native Ads
- Interstitial Ads
- App Open Ads
- Rewarded Ad
- Video Ads (supported on selected platforms)

All formats are responsive and optimized for performance and revenue maximization.
    
# Key Advantages of PubStar SDK

## 1. Prebid + Google Ad Manager Integration

PubStar integrates with:

- Prebid (Header Bidding Technology)
- Google Ad Manager (GAM)

This enables:

- Real-time auction across multiple demand sources
- Dynamic CPM competition
- Automatic selection of the highest-paying ad
- Region-based revenue optimization
- Increased fill rate

Instead of waterfall mediation (which serves ads sequentially), PubStar uses bidding logic to ensure the best paying ad wins instantly.

## 2. Revenue Optimization by Region

The SDK automatically:

- Detects geographic demand differences
- Selects the highest CPM ad in each region
- Improves eCPM and overall monetization performance

Developers do not need to manually configure waterfalls per country.

## 3. Multi-Platform Support

Single monetization solution across:

- Native mobile (iOS & Android)
- Cross-platform frameworks
- Game engines (Unity)

## 4. Unified API Design

All platforms support consistent core operations:

- Initialize
- Load
- Show
- LoadAndShow

## 5. Event-Driven Architecture

Structured callbacks for:

- onLoaded
- onShowed
- onHide
- onError

This allows precise control over user experience.

## 6. Easy Integration

- CocoaPods (iOS)
- Maven (Android)
- npm/yarn (React Native)
- pub.dev (Flutter)
- Unity Package (.unitypackage)

## 7. Customization Support

- Native layout customization
- Advertising management
- Frequency control