---
title: TVSDK 3.15 for Android Release Notes
description: TVSDK 3.15 for Android Release Notes describe what is new or changed, the resolved and known issues and the device issues in TVSDK Android 3.15
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: cd2c64ef-dd42-4dc2-805f-eeb64a8a53d9
---
# TVSDK 3.15 for Android Release Notes {#tvsdk-for-android-release-notes}

TVSDK 3.15 for Android Release Notes describe what is new or changed, the resolved and known issues and the device issues in TVSDK Android 3.15.

The Android reference player is included with Android TVSDK in the samples/ directory of your distribution. The accompanying README.md file explains how to build the reference player.

>[!NOTE]
>
>To successfully build the reference player, as described in the README.md distributed with the release, make sure you do the following:
>
>1. Download VideoHeartbeat.jar from [https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) (VideoHeartbeat library for Android v2.0.0)
>1. Extract VideoHeartbeat.jar into the libs/ folder.

TVSDK for Android provides many performance improvements over previous versions. It provides a high quality viewing experience and carries all the features of version 1.4, with the exception of Multi-CDN support.

The comprehensive set of features supported and not supported are presented in the [Features Matrix](#feature-matrix) section of the release notes.

## Android TVSDK 3.15

This version fixes the issue where the application crashes multiple times when creative tag is missing or when [!UICONTROL url CDATA] is empty in [!UICONTROL VAST] response.

To know about the bug fixes in this and previous versions, see [issues fixed in TVSDK for Android](#resolved-issueszd).
  
### New features and enhancements in the previous releases

**Android TVSDK 3.14**

This version fixes the issue where application crashes when [!UICONTROL CDATA] node is empty for any of the [!UICONTROL ClickTracking], [!UICONTROL CustomClick] or [!UICONTROL CompanionClickTracking] elements in VAST response.

**Android TVSDK 3.13**

Widevine DRM stream freezes or shows black frames on ABR switch on FireTV devices, which include Fire TV 3rd generation Pendant and Fire TV Cube 1st and 2nd generation devices.

To resolve the issue, set the API `MediaPlayer.flushVideoDecoderOnHeaderChange(true)` for the specified Fire TV devices before initiating playback. The default value is false.

**Android TVSDK 3.12**

Primetime Reference application’s gradle version updated to version 5.6.4.

To setup and run Reference app using Android Studio follow the instructions from ReadMe file available with TVSDK zip at `TVSDK_Android_x.x.x.x/samples/PrimetimeReference/src/README.md`.

Top customer issues fixed in the current release are mentioned in [resolved issues](#resolved-issues) section.

**Android TVSDK 3.11**

* **Protection System Specific Header (PSSH) Box fetching allowed** - TVSDK allows fetching of Protection System Specific Header Box associated with current loaded Media Resource. New API `getPSSH()` added to `com.adobe.mediacore.drm.DRMManager`.

For more information, see [Widevine DRM](../programming/tvsdk-3x-android-prog/android-3x-content-security/android-3x-drm-widevine.md).

**Android TVSDK 3.10**

The release focused on fixing top customer issues as mentioned in [resolved issues](#resolved-issues) section.

**Android TVSDK 3.9**

* **Secure Delivery over HTTPS** - Android TVSDK 3.9 introduced the secure delivery capabilities via HTTPS to deliver content securely with unparalleled scale and performance.

  To enable secure delivery over HTTPS, new API introduced in `NetworkConfiguration` class.

  `public void setForceHTTPS (boolean value)`

  `public boolean getIsForceHTTPS()`

**Android TVSDK 3.8**

* **Pre-Roll support with Partial Ad-Break feature** - With this enhancement, TVSDK 3.8 supports pre-roll ads with Partial Ad-Break feature (PABI).

The pre-roll ad, if available, is played, and then the content plays from the live point emulating the experience of live television.

**Android TVSDK 3.7**

* For Widevine test content, a new API `setMediaDrmCallback` in DRMManager class is exposed to override the default implementation of MediaDrmCallback interface.

  `public static void setMediaDrmCallback(MediaDrmCallback callback)`

* Fixed AppCrash error for not handling `MediaPlayerEvent.ITEM_UPDATED` in C++ layer (Android 64 bit).

**Android TVSDK 3.6**

* **Enhance your apps for the 64-bit requirement** - The native library `(libAVEAndroid.so)` is now upgraded and made available in two versions. Existing armeabi (32 bit) native library location has been changed from `/framework/Player to /framework/Player/armeabi` and an additional arm64-v8a (64 bit) library is introduced in `/framework/Player/arm64-v8a.`

**Version 3.5**

* **Just In Time Ad Resolution** - TVSDK 3.5 removes support of the played ads from the timeline.

* **Enabled support for offline playback** - With offline playback, users can now download video content to their devices and watch it when they are not connected. For detailed information, refer to "[Offline Playback with Android](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_3.5.pdf)."

**Version 3.4**

* TVSDK now supports CMAF streams playback for CBC encrypted and plain streams.

**Version 3.3**

* **API changes**

  * A new API is added to `NetworkConfiguration::setNumOfTimesManifestRetryBeforeError(n)*` to handle network errors and timeouts.
    * where (n) is the number of retries.

**Version 3.2**

* **Parallel Ad Resolution and Manifest download support**

  * TVSDK 3.2 supports the simultaneous resolution, instead of the sequential resolution for all the Ad requests and Ad breaks except for VMAP.

  * All the ad manifests in an ad break are downloaded simultaneously.

* **Enabled support for Ad Resolution and Manifest Download Timeout.**

  * Users can now set the timeout value for overall ad resolution and manifest downloads.  In the case of VMAP, the timeout value applies for individual ad breaks as all the ad breaks are resolved sequentially.

* **Introduced new APIs in AdvertisingMetadata Class:**

  * `void setAdResolutionTimeout(int adResolutionTimeout)`

  * `int getAdResolutionTimeout()`

  * `void setAdManifestTimeout(int adManifestTimeout)`

  * `int getAdManifestTimeout()`

* **Removed below APIs from AdvertisingMetadata Class:**

  * `void setAdRequestTimeout(int adRequestTimeout)`

  * `int getAdRequestTimeout()`

* **Enabled playback of streams with AC3/EAC3 audio codec**

  * `void alwaysUseAC3OnSupportedDevices(boolean val)` in `MediaPlayer` class

* **TVSDK supports CMAF and plain streams playback for encrypted Widevine CTR.**

* **Playback of 4K HEVC streams is now supported.**

* **Parallel ad call requests** - TVSDK now prefetches 20 ad call requests in parallel.

**Version 3.0**

* **TVSDK 3.0 supports High Efficiency Video Coding (HEVC) streams.**

* **Just in Time - Resolving ads closer to ad markers**
Lazy Ad Resolving now resolves each ad break independently. Previously, ad resolution was a two-phased approach: pre-rolls were resolved prior to playback start and all mid/post roll slots combined after playback started. With this enhanced feature, each ad break is now resolved at a specific time prior to the ad cue point.

>[!NOTE]
>
>Lazy Ad Resolving has now changed to be turned off by default, and explicitly needs to be enabled.

A new API is added to `AdvertisingMetadata::setDelayAdLoadingTolerance` to get the delayed ad loading tolerance associated with this Advertising Metadata.  
Seeking is now allowed immediately after PREPARATION, seeking over ad breaks will result in immediate resolution before the completion of the seek.  
Signaling modes `SERVER_MAP` and `MANIFEST_CUES` are supported.  
  
For more information, see [TVSDK 3.0 for Android Programmer's Guide](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/c-lazy-ad-resolving/c-lazy-ad-resolving.md) on API and event changes.

* **Updated `targetSdkVersion` to latest Version**  
  
Updated `targetSdkVersion` from 19 to 27 for smooth functioning.

* **Placement.Type getPlacementType() is now a method on interface TimelineMarker**

  This method will return a placement type of Placement.Type.PRE_ROLL, Placement.Type.MID_ROLL or Placement.Type.POST_ROLL. If an ad break is unresolved, the getDuration() method on the TimelineMarker interface will return 0.

**Version 2.5.6.**

* **TVSDK 2.5 supports Android P.**

* **Enabling Background Audio**

  To enable audio playback when app moves from foreground to background, app should call `enableAudioPlaybackInBackground` API of MediaPlayer with true as argument when player is in PREPARED state.

* **alwaysUseAudioOutputLatency(boolean val) in MediaPlayer class**

When set, use output latency in the audio timestamp calculation.
Boolean parameters val - True will use audio output latency in audio timestamp calculation.

* **Optimized to get the best playback experience even if the bandwidth speed falls off suddenly**

TVSDK now cancels the ongoing segment's download, if required, and dynamically switches to the appropriate rendition. This is done by seamlessly switching among the bitrates without interruptions.

**Version 2.5.5**

* **Partial Ad-Break Insertion**  

  TV-like experience of joining in the middle of an ad without firing the tracking for the partially watched ad.  
  Example: User joins in the middle (at 40 seconds) of a 90-second ad break consisting of three 30-second ads. This is 10 seconds into the second ad in the break.

  * The second ad plays for the remaining duration (20 sec) followed by the third ad.
  
  * Ad trackers for the partial ad played (second ad) are not fired. The trackers for only the third ad are fired.

* **Secure Ad Loading over HTTPS**

  Adobe Primetime provides an option to request first call to primetime ad server and CRS over https.

* **AdSystem and Creative Id added to CRS requests**

  Now including `AdSystem` and `CreativeId` as new parameters in the 1401 and 1403 requests.

* **API setEncodeUrlForTracking in NetworkConfiguration class removed** as the unsafe characters in a URL should be encoded.

**Version 2.5.4**

Android TVSDK v2.5.4 offers the following updates and API changes:

* Changes in default value for `WebViewDebbuging`

  `WebViewDebbuging` value is set to `Fals`e by default. To enable it, call `setWebContentsDebuggingEnabled(true)` in the application.

* **OpenSSL and Curl version upgrade**

  Updated libcurl to v7.57.0 and OpenSSL to v1.0.2k.

* App level access for VAST response object

  Introduced a new API `NetworkAdInfo::getVastXml()` that provides access of the VAST response object to the application.

**Version 2.5.3**

Android TVSDK v2.5.3 offers the following updates and API changes.

* All TVSDK customers who use CRS are encouraged to upgrade their apps with TVSDK 2.5.3.85 or latest on Android. This will be a drop-in replacement to the existing app implementation. After the TVSDK upgrade, check for the CRS creative URL requests in a proxy tool (ex: Charles) and confirm that the host name and version in the path reflects as in the sample URL structure below.

  `https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784 bf3586d.m3u8`

* TVSDK's User Agent customizable: we have added some new API's to customize the user agents.

  * `setCustomUserAgent(String value)`
  * `getCustomUserAgent()`

* Share cookies between Android Application and TVSDK: Android TVSDK now supports accessing of cookies between JAVA layer (stored in CookieStore of the Android Application) and the C++ TVSDK layer. Now, it's possible to set and/or modify the cookies in native C++ layer as they will be exposed to the Java Cookie Store.

* API changes:

  * A new Event `CookiesUpdatedEvent` is added. It gets dispatched by the media player when its cookie is updated.

  * A new API is added to `NetworkConfiguration::set/ getCustomUserAgent()` to use custom user agent.

  * A new API is added to `NetworkConfiguration::set/ getEncodedUrlForTracking` to force Encoding of Unsafe characters.

  * A new API is added to `NetworkConfiguration::getNetworkDownVerificationUrl()` to set a network verification URL in case of a failover.

  * A new property is added to `TextFormat::treatSpaceAsAlphaNum` which define whether to treat space as alphanumeric while displaying captions.

* Changes in `SizeAvailableEvent`. Previously, `getHeight()` and `getWidth()` methods of `SizeAvailableEvent` in 2.5.2 used to return Frame height and frame width, which was returned by media format. Now it returns output height and output width respectively returned by decoder.

* Changes in Buffering behavior: Buffering behavior is changed. Its left up to App developer on what they want to do in case of buffer empty. 2.5.3 uses play buffer size at buffer empty situation.

**Version 2.5.2**

Android TVSDK v2.5.2 offers important bug fixes and a few API changes.

**Version 2.5.1**

The important new features released in Android 2.5.1.

* **Performance Improvements -** The new TVSDK 2.5.1 architecture brings a number of performance improvements. Based on statistics from a third party benchmarking study, the new architecture provides a 5x reduction in startup time and 3.8x fewer dropped frames compared to the industry average:

* **Instant on for VOD and live -** When you enable instant on, the TVSDK initializes and buffers media before playback starts. Because you can launch multiple MediaPlayerItemLoader instances simultaneously in the background, you can buffer multiple streams. When a user changes the channel, and the stream has buffered properly, playback on the new channel starts immediately. TVSDK 2.5.1 also supports the Instant On for **live** streams also. The live streams are re-buffered when the live window moves.

* **Improved ABR logic -** The new ABR logic is based on buffer length, rate of change of buffer length, and measured bandwidth. This ensures that the ABR chooses the right bit rate when the bandwidth fluctuates and also optimizes the number of times the bitrate switch actually happens by monitoring the rate at which the buffer length changes.
  
* **Partial Segment Download / Sub-segmentation -** TVSDK further reduces the size of each fragment, in order to start playback as soon as possible. The ts fragment must have a key frame every two seconds.

* **Lazy ad resolution -** TVSDK doesn't wait for resolution of non-preroll ads before starting playback, thus decreasing the startup time. APIs like seek and trick-play are still not allowed until all ads are resolved. This is applicable to VOD streams used with CSAI. Operations like seek and fast forward are not permitted till the ad resolution is completed. For live streams this feature cannot be enabled for ad resolution during a live event.

* **Persistent network connections -** This feature allows TVSDK to create and store an internal list of persistent network connections. These connections are reused for multiple requests, rather than opening a new connection for each network request and then destroying it afterwards. This increases efficiency and decreases latency in the networking code resulting in faster playback performance.
When TVSDK opens a connection it asks the server for a *keep-alive* connection. Some servers may not support this type of connection, in which case TVSDK will fall back to making a connection for each request again. Also, while persistent connections will be on by default, TVSDK now has a configuration option so that apps can turn persistent connections off if desired.

* **Parallel download -** Downloading video and audio in parallel rather than in series reduces startup delays. This feature allows HLS Live and VOD files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback.

* **Parallel ad downloads -** TVSDK prefetches ads in parallel to the content playback before hitting the ad breaks thus enabling seamless playback of ads and content.

* **Playback**

* **MP4 Content Playback -** MP4 short clips do not need to be re-transcoded to play back within TVSDK.

  >[!NOTE]
  >
  >ABR switching, trick play, ad insertion, late audio binding, and sub-segmentation are not supported for MP4 playback.

* **Trick play with adaptive bit rate (ABR) -** This feature allows TVSDK to switch between iFrame streams while in trick play mode. You can use non-iFrame profiles to do trick play at lower speeds.

* **Smoother trick play -** These improvements enhance the user experience:

  * Adaptive bit-rate and frame rate selection during trick play, based on bandwidth and buffer profile

  * Use of the main stream instead of the IDR stream to get up to 30 fps fast playback.

* **Content Protection**

  * **Resolution-based output protection -** This feature ties playback restrictions to specific resolutions, providing finer grained DRM controls.

* **Workflow Support**

  * **Direct Billing Integration -** This sends billing metrics to the Adobe Analytics backend, which is certified by Adobe Primetime for streams used by the customer.

  TVSDK automatically collects metrics, abiding by the customer sales contract to generate periodic usage reports required for billing purposes. On every stream start event, TVSDK uses the Adobe Analytics data insertion API to send billing metrics such as content type, ad insertion enabled flags, and drm enabled flags - based on the duration of the billable stream - to the Adobe Analytics Primetime owned report suite. This does not interfere with or get included in the customer's own Adobe Analytics report suites or server calls. On request, this billing usage report is sent to customers periodically. This is the first phase of the billing feature supporting usage billing only. It can be configured based on the sales contract using the APIs described in the documentation. This feature is enabled by default. To turn this feature off, refer to the reference player sample.

  * **Improved Failover Support -** Additional strategies implemented to continue uninterrupted playback, despite failures of host servers, playlist files, and segments.

* **Advertising**

  * **Moat Integration -** Support for ad viewability measurement from Moat.
  
  * **Companion banners -** Companion banners are displayed alongside a linear ad and often continue to be displayed on the view after the ad ends. These banners can be of type html (an HTML snippet) or type iframe (a URL to an iframe page).

* **Analytics**

  * **VHL 2.0 -** This is the latest optimized Video Heartbeats Library (VHL) integration for automatic collection of usage data for Adobe Analytics. The complexity of the APIs has been decreased to to ease the implementation. Download the VHL library [v2.0.0 for Android](https://github.com/Adobe-Marketing-Cloud/video-heartbeat-v2/releases) and extract the JAR file in the libs folder.

* **SizeAvaliableEventListener**

  * `getHeight()` and `getWidth()` methods of `SizeAvailableEvent` will now return output in height and width respectively. Display aspect ratio can be calculated as follows:
  
    ```java
    SizeAvailableEvent e;
    DAR = e.getWidth()/ e.getHeight();
    ```
  
    Storage Aspect Ratio in terms of Sar width and Sar height can also be used to calculate Frame width and Frame height:

    ```java
    SAR = e.getSarWidth()/e.getSarHeight();
    frameHeight = e.getHeight();
    frameWidth = e.getWidth()/SAR;
    ```

* **Cookies**

  * Android TVSDK now supports access to JAVA cookies stored in CookieStore of the Android Application. A Callback API (onCookiesUpdated) is provided to record whenever a new Cookie comes as part of **Set-Cookie** Response header. These cookies are available as a List of HttpCookie(s) used for a different URI/domain by setting these cookie values on that particular URI/domain using CookieStore. Similarly the cookie values in TVSDK are updated using CookieStore add API.

## Feature matrix {#feature-matrix}

TVSDK for Android supports a number of features that you can implement to add functionality to your video applications.

In the feature tables below, a 'Y' indicates that the feature is supported in the current release.

| Feature | Content type | HLS |
|---|---|---|
| General playback (Play, Pause, Seek) | VOD + Live | Y |
| FER - General playback (Play, Pause, Seek) | FER VOD | Y |
| Seek when an ad is playing | VOD + Live | Not supported |
| HEVC Playback | VOD + Live | fMP4 container only |
| AC3 and EAC3 | VOD + Live | Not supported |
| MP3 | VOD | Not supported |
| MP4 Content Playback | VOD | Y |
| Adaptive Bit Rate Switching Logic | VOD + Live | Y |
| Audio Only Playback | VOD + Live | Y |
| Multi CDN Support | VOD + Live | Not supported |
| Playback of ads with audio-only media | VOD + Live | Not supported |
| Closed Captions - 608/708 | VOD + Live | Y |
| Closed Captions - WebVTT | VOD + Live | Y |
| Manifest Failover | VOD + Live | Y |
| Advanced Failover | VOD + Live | Y |
| QoS and player notifications | VOD + Live | Y |
| Support for cookie headers | VOD + Live | Y |
| Support for custom HTTP headers | VOD + Live | Y (allow listing required) |
| Set buffer control parameters | VOD + Live | Y |
| Set adaptive bit-rate controls | VOD + Live | Y |
| Custom Manifest Tags | VOD + Live | Y |
| Late Audio Binding | VOD + Live | Y |
| 302 Redirect | VOD + Live | Y |
| Playback with Offset | VOD + Live | Y |
| Trick Play | VOD + Live | Y |
| Slow Motion in Trick Play | VOD + Live | Not supported |
| Smooth Trick Play (with ABR) | VOD + Live | Y |
| ID3 Parsing | VOD + Live | Y |
| Blackout of ads | VOD + Live | Not supported |
| Instant On | VOD + Live | Not supported |
| Discontinuity marker support | VOD + Live | Y |
| 302 Redirect Stickiness | VOD + Live | Y |

| Feature | Content type | HLS |
|---|---|---|
| General playback, ads enabled | VOD + Live | Y |
| FER content with ads enabled | VOD | Y |
| Default Ad Behaviors | VOD + Live | Y |
| VAST 2.0/3.0 | VOD + Live | Y |
| VMAP 1.0 | VOD + Live | Y |
| MP4 Ads | VOD + Live | Y (from CRS) |
| Trick Play with Ads Enabled | VOD + Live | Y |
| Ad only | VOD | Y |
| Targeting Parameters | VOD + Live | Y |
| Custom Parameters | VOD + Live | Y |
| Custom Ad Behaviors | VOD + Live | Y |
| Custom Ad Tags | Live | Y |
| Custom Ad Resolvers | VOD + Live | Y |
| Freewheel Custom Ad Resolver | VOD | Y |
| C3 | VOD + Live | Not supported |
| Lazy Ad Resolve | VOD | Y |
| Discontinuity marker support - SSAI | VOD + Live | Y |
| Companion Ads, Banner Ads, and Clickable Ads | VOD + Live | Y |
| VPAID 2.0 | VOD + Live | Y (JS) |
| Early Ad Exit | Live | Y |
| Rules-based Creative Prioritization | VOD + Live | Y |
| CRS Rules | VOD + Live | Y |
| JSON Ad Resolver | VOD + Live | Not supported |
| Moat Integration | VOD + Live | Y |
| Partial Ad Break Insertion | Live | Y |

| Feature | Content type | HLS |
|---|---|---|
| AES Encryption | VOD + Live | Y |
| Sample AES Encryption | VOD + Live | Y |
| Tokenized Streams | VOD + Live | Y |
| Widevine DRM | VOD + Live | fMP4 container only |
| Primetime DRM | VOD + Live | Y |
| External Playback (RBOP) |VOD + Live |Primetime DRM only |
| License Rotation |VOD + Live |Primetime DRM only |
| Key Rotation |VOD + Live |Primetime DRM only  |

| Feature |Content type |HLS |
|---|---|---|
| Adobe Analytics VHL integration | VOD + Live | Y |
| Billing | VOD + Live | Y |

## Resolved issues {#resolved-issues}

Where resolution is associated with a reported issue, a Zendesk reference is displayed, for example ZD#xxxxx.

**Android TVSDK 3.15**

This section provides a summary of the issue resolved in TVSDK 3.14 Android release.

* ZD#46903 - Application crashes multiple times when creative tag is missing or when [!UICONTROL url CDATA] is empty in [!UICONTROL VAST] response.

**Android TVSDK 3.14**

* ZD#46903 - Application crashes when [!UICONTROL CDATA] node is empty for any of the [!UICONTROL ClickTracking], [!UICONTROL CustomClick] or [!UICONTROL CompanionClickTracking] element in [!UICONTROL VAST] response.

### Resolved issues in the previous releases

**Android TVSDK 3.12**

* ZD#40584 - Primetime Reference app does not build with latest gradle version.

**Android TVSDK 3.11**

* ZD#41252 - Korean characters in WebVTT broken after Android 7.1.

**Android TVSDK 3.10**

* ZD#40340 - Application crashes with "App Not Responding" error on attempting playback after block listing all the TS (TypeScript) files.

**Android TVSDK 3.8**

* No new issues added.

**Android TVSDK 3.7**

* No new issues added.

**Android TVSDK 3.6**

* No new issues added.

**Version 3.5**

* ZD#37503 - JSON responses for the CRS rules are cached to avoid the duplicate requests.

**Version 3.4**

* ZD#37996 - Fixed an issue about choppy playback issue for linear and VOD CMAF HEVC streams.
* ZD#37706 - Fixed an issue about garbled captions.
* ZD#37622 - Fixed an issue about fatal URISyntaxErrors for  specific ads.
* ZD#36938 - Fixed an issue about bitrate switching down to the middle bitrate and then picking up to the highest bitrate after exiting out of trick plays.

**Version 3.3**

* ZD#37394 - CMAF asset fast forward causes artifacts after the speed changes.
  * Fixed an issue which occurs with a profile change during trick play.
* ZD#37396 - Ad tracking events are missing for some mid-rolls and post-rolls.
  * Fixed a specific case around ad tracking events.
* ZD#37491 - HTTP status code with error meta is not present.
  * Worked on propagating network errors higher in the stack.
* ZD#37808 - Allow list New Custom Header.
  * SSAI_TAG support added as part of this fix.
* ZD#37622 - URISyntax Errors from Specific Ad Pods.
  * Fixed an issue about stream playback crash when customer Android app is served ads that contain an un-encoded %
* ZD#37631 - Master manifest retry mechanism for Android TVSDK.
  * Added new API in the network configuration for handling this enhancement. If this API is not used, then manifest is not retried. If it is used then manifest will be retried for handling network errors and timeouts.

**Version 3.2**

* ZD#37493- Tracking beacons for live playback do not get fired intermittently for the first ad in sequence.
* ZD#36985- Tracking beacons are not sent for empty ad breaks in VMAP response. 
* ZD#37134 - TVSDK throws the wrong ID for VMAP response intermittently.

**Version 3.0**

* ZD#33740 - TVSDK throws an unneeded warning just after creating a MediaPlayer object and calling replaceCurrentResource()

  * Improved the earlier fix by calling restore only when player is in suspended state

* ZD#36442 - Every new playback disconnects remote debugging session making it impossible to debug.

  * Debug not possible by default on web view as debugging is not enabled by default. App should enable debugging if required by calling setWebContentsDebuggingEnabled(true) on object returned from MediaPlayer.getCustomAdView().

* ZD#33688 - Support for Just In Time ad resolving

  * Ad breaks are resolved at a specified interval prior to the position of the ad break.

* ZD#36441 - Duration of live window keeps increasing beyond 5 minutes causing multiple issues.

  * Fixed an issue where virtualStartTime was getting added twice while calculating virtual live point resulting in this issue.

**Android TVSDK 2.5.6**

* ZD #34992 - Language is empty in Closed Caption.

  * Fixed a case where TVSDK was not parsing #EXT-X-MEDIA:TYPE=CLOSED-CAPTIONS from main manifest to get the caption track details.

* ZD #35078 - Android P validation.

  * TVSDK 2..5.6 has been validated with latest Android P beta build(s). No issues found due to the new Android OS.

* ZD #34149 - Player continues to requests manifests even if error is encountered.

  * Fixed the case where TVSDK was making repetitive calls even when all the profiles were down (404 error).

* ZD #31533 - Playing audio on Android after the app is sent to background.

  * Added `enableAudioPlaybackInBackground` API of MediaPlayer which should be called with 'True' as argument (when player is in PREPARED state) to enable playback of audio when app is in background.

**Android TVSDK 2.5.5**

* ZD #21647 - Android TVSDK notifies 640x368 when actual video size is 640x360.

  * Due to variable m_nOutputHeight (inside AndroidMCVideoDecoder) getting updated with frame height instead of actual output height. Made relevant changes in function getVideoFrame to calculate m_nOutputHeight correctly.

* ZD #26614 - Urgent --- 3rd party ad serving / programmatic --- failure to serve impressions.

  * Enhanced the earlier fix by handling the case in XML parsing where issue was reproducible when "space" is before the "equal" sign like &lt;VAST version ="2.0"&gt;

* ZD #29296 - Android: Add AdSystem and Creative id to CRS requests.

    * Now including 'AdSystem' and 'CreativeId' as new parameters in the 1401 and 1403 requests.

* ZD #33062 - TVSDK crashes on the occurrence of pipe character in VAST response under CDATA node

  * API setEncodeUrlForTracking in NetworkConfiguration class removed as the unsafe characters in a URL to be encoded

* ZD #33063 - CRS file selection logic was broken - TVSDK was not sending CRS request for webm format but sending it for 3gpp files instead.

  * Fixed the logic now. On using media files with webm and 3gpp format, CRS request to be sent for webm. And on using both the media files with 3gpp format, the CRS request to be sent for the highest bitrate 3gpp file.

* ZD #33125 - Android app crashes with specific DoubleClick tag within the VMAP.

  * Fixed the scenario to avoid the crash.

* ZD #32256 - License Rotation & Key Rotation Issue - Adobe Access

  * Fixed the segments initialization with the DRM metadata for SampleAES content. Works fine with AES128 content.

* ZD #33619 - Fast-forwarding a growing playlist content stuck in buffering state near live point.

  * Handled the case when crossing the live point in trick play mode

* ZD #34151 - TimedMetadata objects out of order.

  * Two TimedMetadata events were appearing in random order if they belonged to same time in the timeline. Maintained their original order in manifest.

* ZD #34189 - Issue when seeking to beginning of ad break.

  * The issue was with SSAI ads which are stitched using discontinuity. And the cause was a behavior when we seek to the begining of such ads, we search for a keyframe and we don't find it. The reason was the ad's min audio timestamp being before min video timestamp. Hence, we end up searching for a key frame at a wrong fragmentDump data. Fixed now.

* ZD #34528 - Video resolution not upgrading beyond 640x360 on FireTV 3rd gen dongle.

  * Enhanced the fix to include latest firmware updates

* ZD #34793 - TVSDK 2.5.x used to crash with custom content resolver in some cases when VideoEngine was assuming that the auditudeSettings are available and they were not.

  * The crash was happening due to a function call on a Null shared pointer (auditudeSettings). Added a conditional check within VideoEngineTimeline::placeToSourceTimeline() to make sure auditudeSettings are available before calling anything on that object.

* ZD #32584 - Not able to access complete information present in the &lt;Extensions&gt; node of a VAST response.

  * Fixed the issue around XML parsing and now NetworkAdInfo provides the complete information present in the &lt;Extensions&gt; node

* ZD #35086 - Not getting complete extension data from player in case of specific VMAP responses.

  * The problem was specific to extension xml as XML parsing did not work if extension xml had double quotes within the attribute value. Fixed the issue.

**Android TVSDK 2.5.4**

* ZenDesk#33659 - Playback session enabling webview remote debugging.

WebViewDebbuging is set to False by default. To enable debugging, set as true via the application, using setWebContentsDebuggingEnabled(true).

* ZenDesk#33011 - Ad timeline is not resolved in case of a failed CRS request.

  When a CRS request to an ad fails, the timeline gets resolved and the remaining ads are played.

* ZenDesk#34528 - Video resolution does not upgrade beyond 640x360 on FireTV third-generation dongle.

  Video resolution switches up as bit rate switches.

* ZenDesk#33192 - AudioTrack has null name when track is retrieved via AudioUpdatedEventListener::onAudioUpdated.

  In a few scenarios on FireTV Stick, onAudioUpdate event was getting fired when there was no actual audio update. This is fixed now.

**Android TVSDK 2.5.3**

* Zendesk#32216 - TimedMetadata custom tag subscription is not working.

  We are returning ID3 data as a byte array(to support APIC or generic data) to client whereas in 1.4 return string. Byte array does not handle null terminated character itself, therefore, it was showing special character to the client. This issue is fixed now.
* Zendesk#32670 - Player Not Failing Over to Redundant Playlist

  This is working fine now and setNetworkDownVerificationUrl is working as expected.
* Zendesk#32369 - Closed caption shows different color garbage or artifact.

  Issue with CC glitches has been fixed in latest build
* Zendesk#25590 - Enhance: TVSDK cookie store ( C++ to JAVA )

  Android TVSDK now supports accessing of cookies between JAVA layer (stored in CookieStore of the Android Application) and the C++ TVSDK layer.
* Zendesk#32252 - TVSDK_Android_2.5.2.12 does not seem to have the fix for PTPLAY-20269

  This issue has been fixed and integerated to 2.5.2 branch.
* Zendesk#31806 - Auditude sticks in PREPARING

  Player was stuck in Preparing state because response xml had a empty tag. Now issue is fixed.
* Zendesk#31727 - TVSDK 2.5 closed caption characters are dropped or misspelled.

  Issue is fixed and we are not dropping/misspelling any character.
* Zendesk#31485 - DrmManager in 2.5

  There was some issue in Creating DrmManager via new DrmManager(Context context). Implemented DRMService class which would provide DRMManager.
* Zendesk#32794- 1080P resolution stream not playing on Android

  we have changed SizeAvailableEvent and Previously, getHeight() and getWidth() methods of SizeAvailableEvent in 2.5 used to return Frame height and frame width, which was returned by media format. It now returns output height and output width respectively returned by decoder.
* Zendesk #19359 Flash Player crashes due to the position of #EXT-X-FAXS-CM attribute in set-level manifest.

  The #EXT-X-FAXS-CM tag must always appear at the top playlist before individual bitrate or segments appear in playlist.

**Android TVSDK 2.5.2**

* Zendesk#17305 Artifacts in closed captions with non-opaque background.

  setTreatSpaceAsAlphaNum property in TextFormat is exposed. By default, the property is False. Set the property as True in a client to resolve the dark space issue.

* Zendesk#25097 CC display has visual artifacts with CC settings.

  setTreatSpaceAsAlphaNum property in TextFormat is exposed. By default, the property is False. Set the property as True in a client to resolve the dark space issue.

* Zendesk #31620 User agent string going out of TVSDK player is truncated.

  The User agent string will no more be truncated after 128 characters.

  Adobe Primetime version string is added to the system user agent.

* Zendesk #30809 Missing SEEK_END event prevents app from transitioning to a playing state.
* Zendesk #30415 Closed Caption's 'Cyan' color is now a darker hue of blue (turquoise), compared to the previous Primetime TVSDK releases.

  The color is changed from DarkCyan to Cyan.

* Zendesk #30727 VOD ads are not being downloaded/resolved.

  In VMAP XML if there is an empty VAST tag without an explicit closing tag (‘&lt;/VAST&gt;') and without a newline character after it, then the VMAP XML is not parsed properly and ads may not play.

**Android TVSDK 2.5.1**

* Device-specific (Samsung Galaxy Tab 4) crash; VOD DRM LBA with Auditude and click on ads.
* VHL - Incorrect heartbeat calls are sent when starting content from an offset.
* When VPAID ads are played, the VHL heartbeat calls for event:type:play ad are missing.
* After going into COMPLETE status, the player goes back to the PLAYING status with SKIP adBreakPolicy for post-roll ads.
* Cookies are not being attached to outgoing ad callbacks.
* Ads cue points are not visible.
* HLS with separate EAC3 SAP track won't load.
* Player crashes as TVSDK receives a Screen On intent after the Media Player is restored.

## Known issues and limitations {#known-issues-and-limitations}

**Android TVSDK 3.11**

* No new limitations added.

### Known issues and limitations in the previous releases

**Android TVSDK 3.10**

* No new limitations added.

**Android TVSDK 3.8**

* No new limitations added.

**Android TVSDK 3.7**

* No new limitations added.

**Android TVSDK 3.6**

* No new limitations added.

**Android TVSDK 3.5**

* No new limitation added.

**Android TVSDK 3.4**

* ID3, Closed Captions, Late Binding Audio support has not been verified for the CMAF (CBC) stream.
* On some devices, a low reproducibility issue exists due to which video distortion can appear on the top during trick play on CMAF streams.

**Android TVSDK 3.3**

* clcp:c608 captions are not supported for CMAF stream playback.

**Android TVSDK 3.2**

* TVSDK 3.2 does not support CMAF Sample AES and AES128 streams playback.
* HEVC CMAF streams do not include support for closed captions playback.
* Green coloration appears for WV Encrypted streams when seeking is performed around the non-encrypted segment. 
* CMAF streams do not support ID3 events.
* HLS streams do not support TTML captions format.

**Android TVSDK 3.0**

* HEVC support has following limitations in this release

    * DRM not supported
    * CC (CEA 608/708) support not verified
    * 4K support is not yet present
    * ID3 tags support not verified

* For ad progress events, the timeline bar may not reflect 100% accurate ad playback time. As a workaround, one can use `adcompleteevent` to know the ad playback completion and update UI for various purposes like update the timeline bar, removing ad related UI, etc.
* Vast ad calls returned from VMAP do not honor the Just-In-Time lookahead position.

**Android TVSDK 2.5.6**

* Multiple VMAP ad breaks at same time are not supported.

**Android TVSDK 2.5.3**

This version has the following issues:

* Live video playback may have audio-video sync issues on low end devices or poor network conditions.
* For FER streams, virtualTime and localTime may differ. Also FER with offset does not work.
* Playback might get stuck when Late Binding Audio contents are seek-ed.
* Intermittently, webVTT captions may become out of sync for LIVE contents.
* Intermittently, rapid playback of few frames can be seen after coming out of an ad break.
* Sometimes, 303 error is thrown for Tripple Wrapper Ad Breaks, even though Ads are played.

**Android TVSDK 2.5.2**

This version has the following issues:

* The live video playback may have audio-video sync issues on low-end devices.
* Playback may stall at times when seeking to the end of the VOD media.
* For FER streams, virtualTime and localTime may differ. Also, FER with offset does not work.

**Android TVSDK 2.5.1**

This version of TVSDK has the following issues:

* Live video playback may have audio-video sync issues on low-end devices.
* For FER streams, virtualTime and localTime may differ. Also, FER with offset does not work.
* In VMAP XML, if there is an empty VAST tag without an explicit closing tag (&lt;/VAST&gt;), and without a newline after it, then the VMAP XML is not parsed properly and ads may not play.
* VPAID post-roll are not supported.

## Helpful resources {#helpful-resources}

* [System Requirements](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/android-3x-requirements.md)
* [TVSDK 3.10 for Android Programmer's Guide](/help/programming/tvsdk-3x-android-prog/android-3x-introduction/overview-prod-audience-guide/android-3x-overview-prod-audience-guide.md)
* [TVSDK Android Javadoc for API Reference](https://help.adobe.com/en_US/primetime/api/psdk/javadoc3.5/index.html)
* [TVSDK Android C++ API Document](https://help.adobe.com/en_US/primetime/api/psdk/cpp_3.5/namespaces.html) - Each Java class has a corresponding C++ class, and the C++ documentation contains more explanatory material than the Javadocs, so refer the C++ documentation for a deeper understanding of the Java API.
* [TVSDK 1.4 to 2.5 for Android (Java) Migration Guide](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-25-android.html)
* For handling screen on/off scenarios, see the `Application_Changes_for_Screen_On_Off.pdf` file included in the build.
* See complete help documentation at [Adobe Primetime Learn & Support](https://helpx.adobe.com/support/primetime.html) page.
