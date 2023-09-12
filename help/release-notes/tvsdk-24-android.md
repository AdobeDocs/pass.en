---
title: TVSDK 2.4.1 for Android Release Notes
description: TVSDK 2.4.1 for Android Release Notes describe the new and supported features and the known issues and limitations in TVSDK Android 2.4.1.
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 3de09048-ae32-43b4-a019-34b217931a4c
---
# TVSDK 2.4.1 for Android Release Notes {#tvsdk-for-android-release-notes}

TVSDK 2.4.1 for Android Release Notes describe the new and supported features and the known issues and limitations in TVSDK Android 2.4.1.

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe is releasing TVSDK 2.4.1 for Android.

To use this version of TVSDK, ensure that your system meets the requirements described at [System Requirements](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

Here is where you can find documentation:

• Online help system TVSDK 2.4 for Android Help

• [Javadocs TVSDK 2.4 for Android Java API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

The Javadocs are the ultimate authority, because they are automatically generated directly from the TVSDK source code.

• [C++ API documentation TVSDK 2.4 for Android C++ API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

Each Java class has a corresponding C++ class, and the C++ documentation contains more explanatory material than the Javadocs, so consult the C++ documentation for a deeper understanding of the Java API.

• Migration guide ([TVSDK 2.4 for Android Migration Guide](../migration-guides/tvsdk-14-25-android.md))

This guide explains what you need to modify to migrate an application based on TVSDK 1.4 to one based on TVSDK 2.4.

## New features {#new-features}

TVSDK 2.4.1 for Android provides many performance improvements over earlier versions. It provides a high quality viewing experience.

This version includes all of the features of versions 2.4 and 2.4.1, and no features are deprecated.

Here are the key new features in version 2.4.1:

* HLS version 4 features

    * **Video playback** (play, pause, seek) with player control for live, linear, and VOD streams. 
    * **Closed captioning.** TVSDK can display 608/708 closed captions with a selection of fonts, font sizes, colors, and background. It can also support videos with roll-up captions and switch between language tracks if those are available. 
    * **Trick play mode** supports fast forward and rewind for HLS streams that use I-Frames. All video playback controls function on the content. Slow motion (forward) is available for external video playback mode with rates between 0 and 1. 
    * **Adaptive bitrate (ABR)** lets the player dynamically select which of multiple versions of the same content stream to play, based on network and other conditions. You can set parameters dynamically or in the manifest file to select among aggressive, moderate, and conservative selection policies. 
    * **Byte ranges** enable a single TS file to contain multiple TS segments. 
    * **Alternate audio renditions** enable the player to switch between available audio tracks. 
    * **ID3 support.** TVSDK can play HLS audio and video streams that contain ID3 audio metadata, such as artist name, title, and album. 
    * **Failover. **TVSDK uses strategies to continue uninterrupted playback, despite failures of host servers, playlist files, and segments. 
    * **Multi-channel audio pass-through (DD+).** TVSDK can pass Dolby Digital Plus audio (E-AC3) data to supporting hardware.

* Content protection features

    * **DRM for HLS.** All video playback APIs work with encrypted video content protected by Adobe Access. The following DRM features are supported:

        * License rotation 
        * Key rotation 
        * License caching 
        * Policy time 
        * IV rotation

* **AES 128 Playback.** TVSDK can play advanced encryption standard (AES) HLS content with key size of 128 bits. 
* **Protected HLS (PHLS)** provides a limited set of pre-built DRM policies, a subset of what Adobe Access provides, to enable lightweight DRM over HLS for live and VOD streams.

* Advertising/alternate content and monetization features

    * **Tracking for server-side-inserted ads.** TVSDK can track ads inserted by the Adobe Cloud ad insertion service. It supports linear ads in VAST2, VAST3, and VMAP formats for VOD and live/linear streams. 
    * **Custom HLS tags.** TVSDK uses its `MediaPlayerConfig` class to enable notifying the player application when custom HLS tags appear in the stream.
    * **Client side ad insertion.** The Auditude ad insertion library works with Adobe Auditude servers to resolve ads for insertion dynamically into live, linear, and VOD content, at pre-roll, mid-roll, or post-roll positions. 
    * **Custom ad resolvers.** The `ContentResolver, OpportunityGenerator,` and `MediaPlayerClientFactory` interfaces enable you to implement a custom ad/alternate content resolver and register a custom opportunity detector to work with TVSDK. The `TestAdResolver` and `AuditudeResolver` classes provide C++ examples of implementing a content resolver. You can find a Javascript example at `samples/jspsdk/testapp/psdk.js`.
    * **Consistent ad behavior.** Use the `AdPolicySelector` interface to enable consistent behavior across all players for operations like seek and trick play when ads are present in the content. If you don't implement your own, TVSDK uses `DefaultAdPolicySelector`.
    * **Remove/replace C3 ads.** Use the appropriate TVSDK API to remove custom content ranges and dynamically insert new ads without additional prep work. This is handy when live/linear content is broadcast, then immediately made available on demand without cleanup.

Here are the key new features version 2.4:

* **Instant on for VOD and live** When you enable instant on, the TVSDK initializes and buffers media before playback starts. Because you can launch multiple `MediaPlayerItemLoader` instances simultaneously in the background, you can buffer multiple streams. When a user changes the channel, and the stream has buffered properly, playback on the new channel starts immediately. TVSDK 2.4 also supports the Instant On for live streams also. The live streams are re-buffered when the live window moves. 

* **Performance Improvements **The new TVSDK 2.4 architecture brings various performance improvements:

    * **Sub-segmentation** - TVSDK further reduces the size of each fragment to start playback as soon as possible. 
    * **Parallel ad downloads** - TVSDK prefetches ads in parallel to the content playback before hitting the ad breaks thus enabling seamless playback of ads and content.
    * **Lazy ad resolution** - With this feature, we don't wait for resolution of non-preroll ads before starting playback, thus decreasing the startup time. APIs like seek and trick-play are still not allowed until all ads are resolved.

* **MP4 content playback**

This version of TVSDK supports playback of MP4 as main content.

* **Persistent network connections**

TVSDK maintains a set of reusable network connections, so it does not incur the overhead of creating and destroying a network connection for each network request.

* **Resolution-based output protection**

This feature ties playback restrictions to specific resolutions, providing finer grained DRM controls.

* **Trick play with adaptive bit rate (ABR)**

This feature allows TVSDK to switch between iFrame streams while in trick play mode. You can use non-iFrame profiles to do trick play at lower speeds.

* **Smoother trick play**

These improvements enhance the user experience:

• Adaptive bit-rate and frame rate selection during trick play, based on bandwidth and buffer profile

• Use the main stream instead of the IDR stream to get up to 30 fps fast playback.

* **Improved ABR logic**

The new ABR logic is based on buffer length, rate of change of buffer length, and measured bandwidth. This ensures that the ABR chooses the right bit rate when the bandwidth fluctuates and also optimizes the number of times the bitrate switch actually happens by monitoring the rate at which the buffer length changes.

* **Billing**

TVSDK automatically collects metrics, abiding by the customer sales contract to generate periodic usage reports required for billing purposes. On every stream start event, TVSDK uses the Adobe Analytics data insertion API to send billing metrics such as content type, ad insertion enabled flags, and drm enabled flags - based on the duration of the billable stream - to the Adobe Analytics Primetime owned report suite. This does not interfere with or get included in the customer's own Adobe Analytics report suites or server calls. On request, this billing usage report is sent to customers periodically. This is the first phase of the billing feature supporting usage billing only. It can be configured based on the sales contract using the APIs described in the documentation.

## Supported Features {#supported-features}

TVSDK for Android 2.4 supports a number of features that you can implement to add functionality to your video applications.

>[!NOTE]
>
>In the feature matrix tables below, a √ means that the feature is supported in the current release.

### Core Playback Features {#core-playback-features}

| **Feature** |**Content Type** |**HLS** |**DASH** |
|---|---|---|---|
| General playback (Play, Pause, Seek) |VOD + Live |√ |√ (VOD only) |
| FER - General playback (Play, Pause, Seek) |FER VOD  |√ |Not supported |
| MP3  |VOD |Not supported |Not supported |
| MP4 Content Playback |VOD |√ |√ |
| Adaptive Bit Rate Switching Logic  |VOD + Live |√ |Not supported |
| Audio Only Playback |VOD + Live |√ |Not supported |
| Closed Captions - 608/708  |VOD + Live |√ |√ (VOD only) |
| Closed Captions - WebVTT |VOD + Live |√ |√ (VOD only) |
| Manifest Failover  |VOD + Live |√ |√ (VOD only) |
| Advanced Failover |VOD + Live |√ |√ (VOD only) |
| QoS and player notifications |VOD + Live |√ |√ (VOD only) |
| Support for cookie headers |VOD + Live |√ |√ (VOD only) |
| Support for custom headers |VOD + Live |Not supported |Not supported |
| Set buffer control parameters |VOD + Live |√ |√ (VOD only) |
| Set adaptive bit-rate controls |VOD + Live |√ |√ (VOD only) |
| Custom Manifest Tags (HLS) / Event Streams (DASH) |VOD + Live |√ |√ (VOD only) |
| Late Bound Audio |VOD + Live |√ |√ (VOD only) |
| 302 Redirect |VOD + Live |√ |√ (VOD only) |

### Advanced Playback Features {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>Feature</strong></td> 
   <td><strong>Content Type</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Playback With Offset</td> 
   <td>Live</td> 
   <td>√</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Audio Only Playback</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Trick Play </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Smooth Trick Play (with ABR)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>ID3 Parsing (HLS) / Timed Metadata (DASH)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Blackouts </td> 
   <td>VOD + Live</td> 
   <td>Not supported</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Instant On</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Discontinuity marker support (HLS) </li> 
     <li>Multi-period (DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>302 Redirect Stickyness</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (VOD only)</td> 
  </tr>
  <tr>
   <td>Thumbnail Scrubbing (Iframe and JPEG)</td> 
   <td>VOD + Live</td> 
   <td>Not supported</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Stream Integrity </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Not supported</td> 
  </tr>
 </tbody>
</table>

### Core Ad Insertion Features (CSAI) {#core-ad-insertion-features-csai}

| **Feature** |**Content Type** |**HLS** |**DASH** |
|---|---|---|---|
| General playback, ads enabled |VOD + Live |√ |√ (VOD Pre-rolls only) |
| FER content with ads enabled |VOD |√ |Not supported |
| Default Ad Behaviors  |VOD + Live |√ |√ (VOD Pre-rolls only) |
| VAST 2.0/3.0 |VOD + Live |√ |√ (VOD Pre-rolls only) |
| VMAP 1.0 |VOD + Live |√ |√ (VOD Pre-rolls only) |
| MP4 Ads |VOD + Live |√ (from CRS) |√ (from CRS, Pre-rolls only) |

### Advanced Ad Insertion Features (CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>Feature</strong></td> 
   <td><strong>Content Type</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>DASH</strong></td> 
  </tr>
  <tr>
   <td>Trick Play with Ads Enabled</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Ad only </td> 
   <td>VOD</td> 
   <td>Not supported</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Targeting Parameters</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (VOD Pre-rolls only)</td> 
  </tr>
  <tr>
   <td>Custom Parameters</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (VOD Pre-rolls only)</td> 
  </tr>
  <tr>
   <td>Custom Ad Behaviors</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√ (VOD Pre-rolls only)</td> 
  </tr>
  <tr>
   <td>Custom Ad Tags</td> 
   <td>Live</td> 
   <td>√ </td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Custom Ad Resolvers</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Freewheel Custom Ad Resolver</td> 
   <td>VOD</td> 
   <td>Not supported</td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>C3 Ad Replacement </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Lazy Ad Loading</td> 
   <td>VOD</td> 
   <td>√ </td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>Discontinuity marker support - SSAI (HLS) </li> 
     <li>Multi-period (DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>Companion Ads, Banner Ads, and Clickable Ads</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>√ (VOD Pre-rolls only)</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Live</td> 
   <td>√ (JS) </td> 
   <td>√ (VOD Pre-rolls only)</td> 
  </tr>
  <tr>
   <td>Early Ad Exit</td> 
   <td>Live</td> 
   <td>√ </td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>Rules-based Creative VOD + Live Prioritization</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Not supported</td> 
  </tr>
  <tr>
   <td>CRS Rules </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>Not supported</td> 
  </tr>
 </tbody>
</table>

## Content Protection Features {#content-protection-features}

| **Feature** |**Content Type** |**HLS** |**DASH** |
|---|---|---|---|
| AES Encryption |VOD + Live |√ |√ (VOD only) |
| Sample AES Encryption |VOD + Live |√ |  |
| Tokenized Streams |VOD + Live |√ |  |
| DRM |VOD + Live |Primetime DRM only (Future: Widevine)  |Widevine only |
| External Playback (RBOP) |VOD + Live |Primetime DRM only |Not supported |
| License Rotation  |VOD + Live |Primetime DRM only |Not supported |
| Key Rotation  |VOD + Live |Primetime DRM only |Not supported |

### Integration Features {#integration-features}

| **Feature** |**Content Type** |**HLS** |**DASH** |
|---|---|---|---|
| Adobe Analytics VHL integration |VOD + Live |√ |√  |
| Billing |VOD + Live |√ |Not supported |

## Features not supported {#features-not-supported}

This version of TVSDK does not support:

* Blackout of ads. 
* Slow motion in trick play. 
* Seek and trickplay with MP4 Content. 
* Ad insertion with MP4 main content. 
* Seek when an ad is playing. 
* Playback of ads with audio-only media.

## Known issues and limitations {#known-issues-and-limitations}

This version of TVSDK has the following issues:

* Device-specific (Samsung Galaxy Tab 4) crash VOD DRM LBA with auditude and click on ads 
* Post-roll ad is not played for a specific content. 
* Setting the close caption to CJK languages does not work. 
* Video can come out of trick mode automatically in-between both VOD and live. 
* VHL - wrong heartbeat calls are send when we start a content from an offset. 
* When VPAID ads are played VHL heartbeat calls for event:type:play ad are missing. 
* Pre-roll ad plays even when adBreakPolicy SKIP is chosen. 
* After going into Complete state player goes back to Playing state with SKIP adBreakPolicy for Post-roll ads.

Without video, there is no viewport dimension, and without a viewport dimension, you cannot display any graphics for captions.

## Helpful resources {#helpful-resources}

* See complete help documentation at [Adobe Primetime Learn & Support](https://experienceleague.adobe.com/docs/primetime.html) page.
