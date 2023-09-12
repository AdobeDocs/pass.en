---
description: To use TVSDK most effectively, you should consider certain details of its operation and follow certain best practices.
title: Considerations and best practices
exl-id: f5d3e0ff-675f-4bd4-bfda-71988d25c85d
---
# Considerations and best practices {#considerations-and-best-practices}

To use TVSDK most effectively, you should consider certain details of its operation and follow certain best practices.

## Considerations {#section_tvsdk_considerations}

Remember the following information when using TVSDK:

* Adobe Primetime does not work on iOS simulators.

  You must use real devices for testing.

* Playback is supported only for HTTP Live Streaming (HLS) content.

* Main video content can be multiplexed, where video and audio streams are in the same rendition, or nonmultiplexed, where video and audio streams are in separate renditions.

* The TVSDK API is implemented in Objective-C.

* Video playback requires the native Apple AV Foundation framework. This affects how and when media resources, including closed captions and timelines, can be accessed:

  * Timeline adjustments cannot be revised after the initial setup.

    For example, an advertisement cannot be removed from the timeline after it has played. If the user seeks back in the presentation, the same ad plays again even if the policy would have been to remove the ad.

  * Depending on encoder precision, the actual encoded media duration might differ from the durations that are recorded in the stream resource manifest.

    There is no reliable way to resynchronize between the ideal virtual timeline and the actual playout timeline. Progress tracking of the stream playback for ad management and Video Analytics must use the actual playout time, so reporting and user interface behavior might not precisely track the media and advertisement content.

  * The incoming user agent for all HTTP requests from TVSDK on this platform is determined by the device and the iOS version that is running on the device.

    The value of the user agent string defaults to what the operating system assigns.

## Best practices {#section_tvsdk_best_practices}

Here are recommended practices for TVSDK:

* Use HLS version 3.0 or above for program content.

* Use Apple's mediastreamvalidator tool to validate VOD streams.

* The PTSDKConfig class provides methods to enforce SSL on requests made to Primetime ad decisioning, DRM, and Video Analytics servers.

For more information, see the forceHTTPS and isForcingHTTPS methods in this class.

>[!IMPORTANT]
>
>Requests to third-party domains such as Ad Tracking pixels, Content and Ad URLs, and similar requests are not modified. It is the responsibility of the content providers and ad servers to provide URLs that are supported through HTTPS.
