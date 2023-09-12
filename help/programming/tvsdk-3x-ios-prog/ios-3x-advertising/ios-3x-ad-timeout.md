---
description: You can insert ads in your VOD and live/linear content by using the Adobe Primetime ad decisioning interface.
title: Advertising requirements
exl-id: b162e5b0-9f6c-46de-85de-97cec009a9b7
---
# Ad Timeout {#ad-timeout}

## AV Foundation Requirements {#av-foundation-requirements}

In case of VOD content, the playlist stitching, which involves main content manifest loading, ad resolution and ad manifest loading, should be completed within 35 seconds.

In case of Live content, each time the playlist is updated, playlist stitching should be completed within 20 seconds

**APIs relevant to AdResolution Timeout**

```
/** @name Properties */
/** The default timeout value (in seconds) for resolution of ad requests is 15 seconds.
*
*/
*
@property (notatomic, assign) double adResolutionTimeout;
```

You can set adResolutionTimeout by setting PTAdMetadata::adResolutionTimeout when setting up your ad metadata.

```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adResolutionTimeout = 15 seconds
```

Thereafter follow the section: [Primetime ad server metadata](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).

**APIs relevant to AdManifest Timeout**

```
/** @name Properties */
 /** The default timeout value (in seconds) for loading of ad manifests is 5 seconds.
 *
 */
 *
 @property (notatomic, assign) double adManifestTimeout; 
```

You can set adManifestTimeout by setting PTAdMetadata::adManifestTimeout when setting up your ad metadata.


```
// Create an instance of PTAuditudeMetadata and set its property
PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init]autorelease];;
adMetadata.adManifestTimeout = 5 seconds
```

Thereafter follow the section: [Primetime ad server metadata](/help/programming/tvsdk-3x-ios-prog/ios-3x-advertising/ios-3x-primetime-ad-serving-metadata/ios-3x-primetime-ad-serving-metadata.md).
