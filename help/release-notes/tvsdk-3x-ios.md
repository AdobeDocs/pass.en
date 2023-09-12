---
title: TVSDK 3.13 for iOS Release Notes
description: TVSDK 3.13 for iOS Release Notes describe what is new or changed, the resolved and known issues and the device issues in TVSDK iOS 3.13.
exl-id: adf8ab23-86d6-4113-b243-2709d5f7f829
---
# TVSDK 3.13 for iOS Release Notes {#tvsdk-for-ios-release-notes}

TVSDK 3.12 for iOS Release Notes describe what is new or changed, the resolved and known issues and the device issues in TVSDK iOS 3.12.

## System and software requirements {#system-software-requirements}

Before you download iOS 3.12, ensure that your hardware, operating system, and application versions meet the following requirements:

Operating System: iOS 8.0 or later.

## iOS TVSDK 3.13

The release introduces support for DEMUXED 'HLS/CMAF' (preroll, midroll, and postroll) ads for LIVE, VOD, and FER streams.

For fixes to customer-reported issues, see [Resolved issues](#resolved-issues). For limitations, see [known issues and limitations](#known-issues-and-limitations).

### New features and fixes in the previous releases {#whats-new-previous}

**iOS TVSDK 3.12**

Fixed an issue where live stream fails after 15 minutes of playback. 

**iOS TVSDK 3.11**

Provided fixes for customer issues where `isFallbackOnInvalidCreativeEnabled` and method `customParams` cause application to crash.

**iOS TVSDK 3.10**

* Fixed an issue where TVSDK player does not fire `PTMediaPlayerStatusError` notification when network is unavailable.

**iOS TVSDK 3.9**

* Fixed an issue where VTT subtitles fail to play back causing app freeze.

* iOS TVSDK 3.9 included the updated individualization transport certificate.

**iOS TVSDK 3.8.0.83 Hotfix**

The hotfix had the updated individualization transport certificate.

**iOS TVSDK 3.8**

iOS 13 compliance and handled iOS 13 `UIWebView` API deprecation.

**iOS TVSDK 3.7**

Hotfix for a scenario where play back stopped when many ad resolution requests were made simultaneously.

**iOS TVSDK 3.6**

**Fixes in vastXML property of class `PTNetworkAdInfo`**

The `vastXML` property was not being set properly and was returning a nil value.

**iOS TVSDK 3.5**

**Enabling Background Audio**

*Configure your app to continue playing audio when it goes into the background.*

To enable this feature, we must set the new API `audioPlaybackInBackground` added in the `PTMediaPlayer` class. With this API enabled, your app is ready to play background audio.

**iOS TVSDK 3.4.0.19 (Hotfix)**

This release has a fix for the application crashes that occur in an ad failover scenario.

**iOS TVSDK 3.4**

**Ad Resolution Timeout**

* With TVSDK 3.4, users can now set the timeout value for overall ad resolution and manifest downloads. If within a given timeout some ads are not resolved, TVSDK plays the remaining ads.

* `PTAdMetadata: adRequestTimeout` API has been deprecated and will be removed. The default value has been set to 35 seconds.

* Two new alternate APIs have been introduced in the `PTAdMetadataClass: adResolutionTimeout`  - timeout for overall ad resolution calls                adManifestTimeout – timeout for ad manifest downloads.

**Revenue Optimization**

Enabled TVSDK to identify problem areas related to ad insertion workflows to report to an analytics end point of choice.

**Version 3.3**

TVSDK 3.3 is now compliant with iOS 11 SDK. All the deprecated APIs have been replaced with suitable alternatives.

**Version 3.2**

**Additional Logging Support (Phase 2)**

Added support for error notifications, in case of:

* HLS version of ad uses higher level than content.

* Audio-only variant is excluded.

* VAST/VMAP request is failed.

**Version 3.1**

* **Additional Logging Support**
Added support for descriptive notifications if there is Ad playback failures.

* **Added [!DNL Fairplay] Encrypted CMAF stream support**
[!DNL Fairplay] Encrypted CMAF streams with AVC codec playback is now supported.

**Version 3.0.1**

No new feature or enhancements in this release.

**Version 3.0**

* TVSDK 3.0 supports HEVC streams.

* Just In Time - Resolving ads closer to ad markers.

Added `enableDelayAdLoading` property of Boolean type on App level interface to enable JIT. If `enableDelayAdLoading` is NO, it will `setadMetadata.delayAdLoading`to True (property of PTAdMetadata interface).

With this property enabled, TVSDK resolves each ad breaks prior to its position based on the tolerance value defined. By default, `delayAdTolerance` is set to five seconds.

**Version 1.4.45**

To comply with Xcode10, TVSDK has moved from `libstdc++` to `libc++`, and as a result the minimum supported version is iOS 7. Earlier it was iOS 6.

**Version 1.4.44**

No new feature or enhancements in this release.

**Version 1.4.43**

* TV-like experience of being able to join in the middle of an ad without triggering partial ad's tracking.  
  Example: User joins in the middle (at 40 seconds) of a 90-second ad break consisting of three 30-second ads. This is 10 seconds into the second ad in the break.

  * The second ad plays for the remaining duration (20 sec) followed by the third ad.
  * Ad trackers for the partial ad played (second ad) are not triggered. The trackers for only the third ad are triggered.

* Added `enableVodPreroll` property of Boolean type in PTAdMetadata interface. The property can be used to enable pre-roll on a VoD stream. If `enableVodPreroll` is NO, PSDK does not play pre-roll. This, however, has no impact on the mid-rolls. The default value of `enableVodPreroll` is YES.
* `closedCaptionDisplayEnabled` API of `PTMediaPlayer` interface is marked as deprecated from iOS v1.4.43 onwards. To determine whether closed captions are available for a given `PTMediaPlayerItem`, examine the `subtitlesOptions` property of `PTMediaPlayerMediaItem`.

**Version 1.4.42**

No new features are added in this release. For a list of issues fixed, see [Resolved issues](#resolved-issues).

**Version 1.4.41**

API changes:

* **isSecure**: A new API is introduced isSecure to secure the player from recording and throwing an error. The default value is true.

* **allowExternalRecording**: A new API is introduced to allow airplay mirroring for a secure content. Airplay mirroring is treated as recording therefore `allowExternalRecording` value must be set to `True`, to allow airplay mirroring or set to `False` to stop the airplay mirroring for secure content. By default, `value` is true.

**Version 1.4.40**

No new features.

**Version 1.4.39**

* iOS  TVSDK  is certified with VHL 2.0.1 and with VHL 2.0.1 with Nielsen.

* iOS  TVSDK  is updated to make CRS requests from new Akamai host `primetime-a.akamaihd.net`.

* New hostname configuration provides CRS asset delivery via both HTTP and HTTPS (SSL) at greater scale.

**Version 1.4.36**

Integrate and certify VHL 2.0 in iOS  TVSDK : Reduce the barrier in the `VideoHeartbeatsLibrary` implementation by decreasing the complexity of the APIs.

**Version 1.4.34**

**Network Ad Information**

TVSDK APIs now provide additional information on third-party VAST responses. Ad ID, Ad System and VAST Ad Extensions are provided in `PTNetworkAdInfo` class accessible through  `networkAdInfo`  property on an Ad Asset. This information can be used for integrating with other Ad Analytics platforms such as **Moat Analytics**.

**Version 1.4.31**

* **Billing Metrics** To accommodate customers who want to pay only for what they use, rather than a fixed rate regardless of actual use, Adobe collects usage metrics and uses these metrics to determine how much to bill the customers.

  Every time TVSDK generates a stream start event, the player starts to send HTTP messages periodically to Adobe's billing system. The period, known as billable duration, can be different for standard VOD, pro VOD (mid-roll ads enabled), and live content. The default duration for each content type is 30 minutes, but your contract with Adobe determines the actual values.

* **Multi-CDN Support for CRS Ads** TVSDK now supports Multi-CDN for CRS ads. By providing FTP details for CRS ads, you can specify CDN locations, other than the default Adobe-owned CDN such as [!DNL Akamai].

**Version 1.4.29**

In the `PTSDKConfig` class, the `forceHTTPS` API has been added.

The `PTSDKConfig` class provides methods to enforce SSL on requests made to Adobe Primetime ad decisioning, DRM, and Video Analytics servers. For more information, see the `forceHTTPS` and `isForcingHTTPS` methods on this class. If a manifest is loaded over HTTPS, TVSDK preserves the content use of HTTPS and respects this usage when loading any relative URLs from that manifest.

>[!NOTE]
>
>Requests to third-party domains such as Ad Tracking pixels, Content and Ad URLs, and similar requests are not modified, and it is the responsibility of the content providers and ad servers to provide URLs that are supported through HTTPS.

**Version 1.4.18**

Primetime iOS TVSDK now supports VPAID 2.0 JavaScript creatives to enable a rich interactive in-stream ad experience. For more information about VPAID 2.0, see VPAID ad support.

**Version 1.4.17**

* tvOS

  The TVSDK supports tvOS native applications.
* The following types of content can be played:

  * VOD
  * Live
  * AES-128
  * Alternate audio and subtitles
  * FER

* The following types of ads can be displayed:

  * Basic
  * VAST2
  * VAST3
  * VMA

* The following features are currently not supported:

  * Digital Rights Management (DRM)
  * Ad banners
  * TV Markup Language (TVML)

**Version 1.4.13**

>[!NOTE]
>
>The Nielsen module has been removed from the TVSDK build, the TVSDK will be updated soon with a new Nielsen integration module.

**Ad Fallback, Daisy chaining in ad selection logic (Zendesk #3103)**

For VAST ads (creatives) with the fallback rule enabled, the TVSDK treats an ad with an invalid MIME type as an empty ad and attempts to use fallback ads in its place. You can configure some aspects of fallback behavior. For more information, see Ad fallback for VAST and VMAP ads.

**Version 1.4.9**

**Blackout Signaling With Alternate Content Replacement**

As part of the 1.4 TVSDK update, Adobe also now supports going into and returning from regional blackouts against linear content. The TVSDK can now process two manifest files in parallel, main and alternate, to monitor for blackout signals even when alternate programming is being shown in place of the original programming.

**Version 1.4.8**

**Video Heartbeats Library (VHL) updated to version 1.5**

* Ability to send metadata with video start or video/ad/chapter start as context data.

* Less network traffic - Heartbeats are fewer on average and smaller in size.

**Version 1.4.7**

* **On-Premise Individualization Support**

Support for on-premise installations of the Adobe Individualization Server to customize the client's individualization request to go to a different endpoint.

* **Resolution-Based output protection**

DRM Policies can now specify the highest resolution permitted, depending on the device's Output Protection capabilities. For example, _If HDCP is available, allow  content  of up to 1080p resolution to be played, and if HDCP is not available, allow  content  of up to 480p resolution to be played._

**Version 1.4.4**

* **Video Heartbeats Library (VHL) update to version 1.4.1.1**

  * Added the ability to bundle different analytics use cases, from other SDKs or players, with the Adobe Analytics Video Essentials.
  * Ad tracking has been optimized by removing the `trackAdBreakStart` and `trackAdBreakComplete` methods. The ad break is inferred from the `trackAdStart` and `trackAdComplete` method calls.
  * The `playhead` property is no longer needed when tracking ads.
  * Added support for the Experience Cloud ID Service.

* **Nielsen SDK Integration**

The TVSDK now supports sending mTVR and MDPR ID3 beacons to the Nielsen SDK without any custom integration. In order to get started, download the 3.1.2.19 Nielsen iOS App SDK, and follow the instructions found here in the iOS Programmers Guide.

**Version 1.4.0**

* **Blackout Signaling With Alternate Content Replacement**

As part of the 1.4 TVSDK update, the TVSDK also now supports going into and returning from regional blackouts against linear content. The TVSDK can now process two manifest files in parallel, main and alternate, to monitor for blackout signals even when alternate programming is being shown in place of the original programming.

* **Remove/Replace C3 Ads**

Now, no additional prep work is required to dynamically insert new ads into video-on-demand (VOD) assets that are coming out of the C3 window. The TVSDK now provides an API to remove custom content ranges and dynamically insert new ads. This powerful new functionality is also useful in cases where live/linear content airs during  broadcast  and is immediately pulled down for use as  on-demand content without proper time to clean the asset.

## Resolved issues {#resolved-issues}

Where resolution is associated with a reported issue, a Zendesk reference is displayed, for example ZD#xxxxx.

<!-- 

Comment Type: draft

 <p>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:</p> 
 <p><span class="code">https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8</span></p> 

-->

<!--
Comment Type: draft

 <p>TVSDK versions earlier than version 1.4.28 sometimes exhibit a long delay in the startup time when ad-enabled content is played on devices that are running on iOS 10. To resolve this issue, upgrade to version 1.4.28 or later. Version 1.4.28 was released on August 31, 2016, and iOS 10 was released on September 13, 2016.</p> 
-->

**iOS TVSDK 3.13**

* (ZD 42085) - Issues with playback on CMAF streams.

* (ZD-43215) - Crash when dismissing the player while an ad is in progress.

* (ZD 43210) - iOS HLS playback freezes when WebVTT subtitle is enabled.

**iOS TVSDK 3.12**

* Live stream fails after 15 minutes of playback when using TVSDK for iOS 3.10.

### Resolved issues in the previous releases {#resolved-issues-previous}

**iOS TVSDK 3.11**

* (ZD#40998) - The `isFallbackOnInvalidCreativeEnabled` causes the application to crash.

* (ZD#41289) - `NSInvalidArgumentException` is observed with the method `customParams` leading to application crash.

**iOS TVSDK 3.10**

(ZD#40943) - TVSDK player does not fire `PTMediaPlayerStatusError` notification when network is unavailable.

**iOS TVSDK 3.9**

(ZD#40272) - iOS TVSDK fails to play VTT subtitles with 101001 error and leads to app freeze.

**iOS TVSDK 3.8**

* (ZD#40087) - iOS crashes with player error for expired VOD content.

* (ZD#40083) - Pre-Roll ads do not play for livestream with `OpportunityGenerator` and player gives error.

* (ZD#39828) - `CurrentItem` property is missing the nullability annotation, causing player crash when the player status contained in the notification is `PTMediaPlayerStatusStopped`.

**iOS TVSDK 3.7**

(ZD#38961) - Content fails to play in the Picture-in-Picture (PiP) window after one content completes playback, when multiple content is configured to be played in the PiP.

**iOS TVSDK 3.6**

No new issues in this release.

**iOS TVSDK 3.5**

No new issues in this release.

**Version 3.3**

(ZD#37820) - Added allow listing for custom header HS-Id, HS-SSAI-TAG.

**Version 3.2**

* **Ticket#36588** - Player crash is observed when the MediaPlayer STOP method is called.

Fixed intermittent crash observed when STOP method is called for a few streams with subtitles.

* **Ticket#37080** - Duplicate requests seen for Manifest calls.
Fixed the duplicate requests made for Manifest URLs during playback. TVSDK now makes one call per manifest.

* **Ticket#37** - CRS normalization rule fails with eq match type
Fixed a case where the player used to crash when encountered with last normalization rule set for hostnames with an "eq" match type.

**Version 3.1**

**Ticket #36313** - Intermittent unpredictable results during Linear Ad Breaks
Fixed intermittent playback during linear ad breaks in Live stream.

**Version 3.0.1**

**Ticket36948** - CRS - Asset selection order inconsistent on iOS 12
The asset selected for CRS is not always the highest-quality variant returned in a VAST or VMAP response.

**Version 3.0**

* **Ticket35311** - Player status doesn't become PAUSED during a phone call interruption
Added interrupt handler to stop the player from interrupting. On interruption, the player status becomes PAUSED and, then resume playback on clicking the play button.

* **Ticket36685** - Live assets - Time mismatch with player time progress and SCTE marker time
Correct time is calculated for the SCTE markers that are ahead of live point.

* **Ticket36492** - `currentTime` and `localTime` aren't updated when seeking to a new position during paused status
Player's current time can now be set to zero in case player is in paused state; earlier the current time used to be set to zero only in play state.

**Version 1.4.45**

* **Ticket36294** - iOS TVSDK not functional with Xcode 10
Fixed the compilation issues with TVSDK on XCode 10. Due to XCode ten requirements, apps build on TVSDK for iOS 1.4.45 onwards require minimum deployment target as iOS 7.0

* **Ticket36321** - Discrepancy observed in seek-able range between `PTMediaPlayer` and `AVPlayer` instance in _Playing_ state.

* **Ticket36493** - `libstdc++` support on iOS 12
Fixed the compilation issues with TVSDK on iOS 12. Apps build on TVSDK for iOS 1.4.45 onwards require minimum deployment target as iOS 7.0

**Version 1.4.44**

* **Ticket34683** - Ad Playback Progress Time Is Going In Negative

Additional checks put in to handle the case when there is a mismatch between the duration reported by the ad server and actual ad content.

* **Ticket34801** - `currentTime` and `localTime` were not getting updated when seeking to a new position during paused status
Player's current time can now be set to zero in case player is in paused state; earlier the current time used to be set to zero only in play state.

* **Ticket35037** - Play back stalls with bad URL when returning from signal-based ad insertion.
Improved fix provided for closed issue #34385 in 1.4.42 release. Added isCancelled check and exception handling code to make operation queue more robust.

**Version 1.4.43**

* (ZD#32990) - iOS: Content playing instead of ads on some cue-points. `selectedMediaOptionInMediaSelectionGroup` API which was part of AVPlayerItem interface has now moved under `AVMediaSelection` in iOS 11. The issue got resolved using this new API.

* (ZD#33683) TVSDK removed `==` suffix from the metadata strings. The issue is fixed in the parsing logic.

* (ZD#33905) - iOS TVSDK making calls to the manifest files with two user agents. The user agent issue has been fixed in first m3u8 call (fresh install case). M3u8's have the same user-agents for all the calls now.

* (ZD#34293) - Pre-rolls inserted on LINEAR streams do not play correctly on iOS11. The issue is fixed for pre-roll ads.

* (ZD#34684) - When the ad skip policy is applied, pre-roll ad frames are shown for few seconds. A new API, `enableVodPreroll` has been introduced to disable pre-roll playback in vod playback. The default value for this API is _Yes_. The API ensures skipping of ad content stitching in the main content.

* (ZD#34765) - After calling `stop()`, few Transport Streams segments still get downloaded. Enhanced the `Stop()` API to avoid download of the extra segments.

* (ZD#34865) - Pre-roll ads for [!DNL Livestream] are truncated on iOS. Related to iOS11, and adding an extra check to confirm if the stream is pre-roll or main-content, addresses this issue.

* (ZD#35093) - Fixed a failover scenario where, if Primary variant of the stream fails at startup (returns 404), playback does not switch to backup stream.

**1.4.42 (1.4.42.118)**

* (ZD#34385) - Playback stalls with a bad URL when returning from signal-based ad insertion.

  Increase the maximum concurrent counts for `CustomAVAssetLoaderOperations`, so that the manifest reads can continue to execute.

* (ZD#34373) - End users are not able to stream to HDMI-connected devices, when stream recording is disallowed.

* (ZD#32678) - TVSDK does not collect the correct ad IDs on iOS.

  Ad ID of the final Ad creative is now picked up in VHL pings if there are VAST/VMAP redirects.

* (ZD#33904) -  TVSDK  is not Registered for AVFoundation notifications `AVAudioSessionMediaServicesWereLostNotification` and `AVAudioSessionMediaServicesWereResetNotification`.

  `PTMediaServicesWereLostNotification` and `PTMediaServicesWereResetNotification` can now be registered on the player App to get the notifications when Media services are reset or lost.

* (ZD#33815) - Customers are not able to update their prioritization and normalization CRS rules without requiring an app update.

  Added the `getCRSRulesJsonURL` and `setCRSRulesJsonURL` APIs to the iOS  TVSDK .

**Version 1.4.41 (1.4.41.76)**

* (ZD #34464) - Issues building Reference App with TVSDK Version 1.4.41

  Starting this version, Xcode 9 is required for compiling  TVSDK  for iOS.
* (ZD #29456) - Airplay Starts in Paused State

  Fixed the pause issue that is when Video Pauses when Entering Airplay.
* (ZD #30371) - AdBreak start time changes when we insert more than two ads in linear stream

  Fixed the Error when attempting to playback content on Apple TV, which  prevents  playback completely
* (ZD #32146)- No `PTMediaPlayerStatusError` is received for HLS Live content on blocking iOS 11 dev beta

  No `PTMediaPlayerStatusError` is received for HLS Live and VOD content on blocking using Charles (Drop connection and 403).
  
* (ZD #29242) - Airplay Video Playback Fails with Ads Enabled.

  When ads are enabled and AirPlay is enabled starting playing a video, video playback never starts and no error is shown.

* (ZD#33341) - `DRMInterface.h` triggers build warnings in Xcode 9.

  Fixed two block prototypes in `DRMInterface.h` which were missing the word 'void' in their parameter lists.

* (ZD#31979) - Does not compile/run when it is iOS 10 or later for iPhone 7/iPhone7+.

  Fixed Compiling IB documents for earlier than iOS 7 is no longer supported.

* (ZD#32920) - Blank screen within an Ad break and no Ad break completion.

  When an Ad break is presenting Ad instances and after an ad instance is finished, a blank screen is shown.

* (ZD#32509) - Disable iOS 11 screen recoding Disable screen recording on iOS 11.

* (ZD#33179) - Intermittent event failure on iOS11.

  Fixed the event failure on iOS 11.

**Version 1.4.40** (1.4.40.72)

* (ZD #32465) - Player cannot handle merged playlists.

  Call `finishLoadingWithError`(with: Error) for AV foundation to try alternate streams / trigger failover.

* (ZD #31951) - TVSDK Error during License Rotations.

  Fixed the license rotation issue.
* (ZD #31951) - Blank screen within an Ad break and no Ad break completion.

  Handled an issue where Facebook VPAID ads were often returning multiple CDATA blocks in a single `<AdParameters>` VAST node.
* (ZD #33336) - iOS TVSDK - Ad pods not being filled, despite enough ads being returned by Freewheel.

  Created parent-child relation between sequence ad and fallback ad and sorting based on parent sequence and index.

**Version 1.4.39** (1.4.39.43)

* (ZD #32178) - iOS TVSDK version is incorrect.

  The TVSDK version output in the log files was 1.0.211. It is fixed to output the correct version.

* (ZD #32199) - Lazy Ad loading - Video is not displayed for the content.

  Local Adbreak timeline that was not getting initialized previously, is now refreshed before usage.

* (ZD #27528) - Video, audio, or both freeze 1-45 seconds after an asset starts playing, if the secondary audio is set to non-default on iOS 1.2.

  Prepare and inform audio tracks in  Ready  state.

* (ZD #30411) - You may get unexpected results like no audio or incorrect  audio, if you choose a secondary Sap language.

  Prepare and inform audio tracks in  Ready  state.

* (ZD #32199) - Lazy Ad loading - Video is not displayed for the content.

  Local  Adbreak timeline that was not getting  initialized  previously, is now refreshed before usage.

* (ZD #27528) - Video, audio, or both freeze 1-45 seconds after an asset starts  playing,  if the secondary audio is set to non-default on iOS 1.2.

  Prepare and inform audio tracks in  Ready  state.

* (ZD #30411) - You may get unexpected results like no audio or incorrect  audio,  if you choose a secondary Sap language.

  Prepare and inform audio tracks in  Ready  state.

**Version 1.4.38** (1.4.38.860)

* (ZD #29281) - iOS: Add AdSystem and Creative Id to CRS requests

Usage of creative Id and AdSystem in CRS request based on CRS normalization rules

* (ZD #29176) - Crash on `PTAdPolicyDeligate` `satAdBreakAsWatched:position`

Crash due to empty AdBreak is handled now.

* (ZD #30125) - Programmatic ads are not working  in  iOS platform

Added Programmatic ads support in iOS.

* (ZD #30782) - #EXT-X-PROGRAM-DATE-TIME Notification

Timed metadata event is not fired for  # EXT-X-PROGRAM-DATE-TIME tag with LIVE DRM streams.

**Version 1.4.37 (1.4.37.842)**

* (ZD #28950 ) - VOD playback issue

Playback issue when  # EXT-X-PLAYLIST-TYPE tag in the stream is set to Event rather than VOD

* (ZD #29281) - iOS: Add AdSystem and Creative Id to CRS requests

Usage of Creative Id and AdSystem in CRS request based on CRS normalization rules.

* (ZD #29462) - TremorHub ad in A&E VOD causing a crash in iOS apps

**Version 1.4.36 (1.4.36.835)**

* (ZD #29418) - Cues with duration 0 (#EXT-X-CUE-OUT:0.000) are causing iOS TVSDK to stop or crash the playback.

The issue is fixed and playback starts correctly.

* (ZD #29462) - Ad in VOD causing a crash on iOS  TVSDK .

The issue is fixed. iOS  TVSDK  is raising an `exception(AUDNetworkAdInfo::initWithAdId)` and not handling it. The exception is due to empty Ad ID.

* (ZD #29281)- Add AdSystem and Creative id to CRS requests.

Include AdSystem and  CreativeId  as new parameters in the 1401 and 1403 requests (all other parameters remain the same).

**Version 1.4.35** (1.4.35.830)

* (ZD #27830) - Need to determine programmatically the difference between closed-captions and subtitle in iOS.

TVSDK now exposes the two types which can be used to filter out the required caption type.

* (ZD #29160) - EXT-X-CUE-OUT ad cues are not spliced-in correctly on TVSDK iOS.

With EXT-X-CUE-OUT midroll ad is playing now.

* (ZD #29100) - The app crashes when the user scrubs to the end of a movie.

Fixed multiple crashes related to synchronization.

* (ZD #28785), (ZD #27712), and (ZD #25076) - iOS app is crashing during the large live events.

Fixed multiple crashes related to synchronization.

**Version 1.4.34** (1.4.34.815 for iOS 6.0+)

* (ZD #28481) - FER outage due to the incorrect key being appended at the end of an ad break for those FER streams

For an FER stream, the key before the ad break is inserted after the end of the ad break. This issue was resolved by appending the *last seen key* at the end of the ad break.

**Version 1.4.33** (1.4.33.803 for iOS 6.0+)

* (ZD# 21701) Enable CRS for Sub-accounts

Enabled by sending the original creative URL for the 1401 CRS request instead of the normalized URL, as per the requirement for CRS back end.

* (ZD# 26218) - `PSDKResources.bundle` loading issue

This issue was resolved by updating resource loading to look from all available bundles.

* (ZD# 27460) Midroll first Ad call - POST to `cdn.auditude.com` returning 403.

The new CDN account is unable to handle a POST CDN request. This issue was resolved by updating the code to make the `cdn.auditude.com` ad request to be GET instead of POST.

**Version 1.4.32** (1.4.32.792 for iOS 6.0+)

* (ZD# 27132) Support for decimal values for VMAP Ad Breaks.

When content was not segmented along the defined ad breaks, integers were causing unexpected ad placements. The issue was resolved by not converting the decimal values to integers.

* (ZD# 27189) AES content with the EXT-X-DISCONTINUITY-SEQUENCE tag are not playing correctly.

The issue was resolved by placing the tag at the beginning of the playlist.

**Version 1.4.31** (1.4.31.785 for iOS 6.0+)

* (ZD# 24528) Implement TVSDK Usage Metrics for Billing

For more information, see [Billing Metrics].

* (ZD# 24642) Picture-in-Picture support for  TVSDK

The picture-in-picture feature, which was not working properly sometimes, has been fixed.

* (ZD# 25246) Incorrect Ad Break Signals

This issue was resolved by aligning discontinuity tags across variant manifests.

* (ZD# 26218) The application build process gets complicated when trying to include `PSDKLibrary.framework` in the client's application framework

This issue was resolved by packaging the `PSDKLibrary.framework` as requested.

* (ZD# 26364) Multi-CDN Support for CRS Ads

For more information, see Multiple CDN support for CRS Ad Delivery.

* (ZD# 27028) Delay in playback of some streams in iOS 10.

This issue was resolved by providing a workaround for streams that do not have an M3U8 extension.

**Version 1.4.30** (1.4.30.754 for iOS 6.0+)

The following issues were resolved for TVSDK in this release:

* (ZD# 24180) Add a custom header to allowlist.

A new custom header has been added to the TVSDK allowlist.

* (ZD# 25016) Failover stream is selected randomly when ABR control parameters are set

This issue was resolved by maintaining the ABR streams in order when the ABR settings are provided with the `initialBitrate` setting on a stream that includes failover URLs. This avoids playing the failover streams instead of primary.

* (ZD# 25076) Crash on `PTAuditudeAdResolver loadComplete`

The issue where a crash was occurring during rapid start/stop of multiple PTMediaPlayer instances with ads has been fixed.

* (ZD# 25960) No additional subscribed tags tare triggering metadata change notification broadcasts

The issue where a subscribed tag is not notified when it appears before the first segment in the manifest has been fixed.

* (ZD# 26084) PSDK throwing a 106000.101000.-11833 decoder not found error when transitioning from the last ad break back to entertainment content

When the last ad break start time from the VMAP falls before the total duration is complete, in certain conditions, the key is not inserted until after the end of the last ad break. This issue has been fixed.

* The Video Heartbeat Library (VHL) has been updated to version 1.5.9 to resolve the following issues:

* (ZD #22351) VHL - Analytics: Live video asset duration

This issue was resolved by adding the  `assetDuration`  API to `PTVideoAnalyticsTrackingMetadata` to update the asset duration for Live/Linear streams and provide a logic for checking the live stream.

* (ZD# 22675) VHL - Analytics: Updating live video asset duration

This issue is the same as ZD #22351.

* (ZD #25908) VHL - Analytics: Adobe Heartbeat Event Crash

This issue was resolved by updating the implementation to use the latest version of VHL for iOS version 1.5.9 to improve stability and performance.

* (ZD #25956) VHL - Analytics: Crash when repeatedly playing videos

This issue is the same as ZD #25908.

**Version 1.4.29** (1.4.29.743)

* (ZD# 23901) Third-party ads are not playing

This issue was resolved by moving to CRS v3 URL structure to include the zone ID in the repackaged URL.

* (ZD #25183) Issues with DRM playback on tvOS and iOS

This issue was resolved by providing support for multiple key tags that are needed for multi-DRM support.

* (ZD# 25334) TVSDK fails to play a  cDVR  shared content

This issue was resolved by preventing TVSDK from converting empty strings to absolute URLs.

* (ZD# 25347) Set custom HTTP header on AVURLAsset

Support for custom headers on ts segment requests through the `PTNetworkConfiguration` class has been added.

**Version 1.4.28** (1.4.28.722)

* (ZD #24549) Multiple Ad tracking calls

This issue was resolved by updating the timeline manager to listen for notifications on a specific object when multiple players are created.

* (ZD #24758) `PTManifestLogger` does not support iOS 8

This issue was resolved by updating the logger utility library to the version 7.0 deployment target.

* (ZD #24775) Delayed stream due to Ads

This issue was resolved by correctly calculating the duration drift on event playlists.

* (ZD #24799) Some of the episodes are not playing on iOS APP

This issue was resolved by using local web server for subtitles when the WebVTT files are geo-restricted.

**Version 1.4.27** (1.4.27.711) for iOS 6.0+

* (ZD #24089) - Optimizations for ad resolving on long DVR streams

This issue was resolved by adding multiple optimizations to reduce the time that is required to process the DVR window in live/linear streams.

* (ZD #21554) - TVSDK error beacons not fired for `application-type = video/mp4`

This issue was resolved by enabling the player to ping the correct error tracking URLs on invalid asset formats.

* (ZD #24424) - Crash of type `EXC_BAD_ACCESS KERN_INVALID_ADDRESS` is originating from inside `PSDKLib` for iOS on newer hardware devices.

The crash that occurred because of a de-allocated media player instance, when playback is switched rapidly between different streams, has been fixed.

* (ZD #24575) - Crash in TVSDK on 32-bit devices when `enableDebugLog=true`

The issue in the log format that caused the crash on 32-bit devices when logging is enabled has been fixed.

**Version 1.4.26** (1.4.26.702) for iOS 6.0+

* (ZD# 20213) - TVSDK FW must be dynamic/modularized for XCode7

Fixed by updating the libraries with module support

**Version 1.4.25** (1.4.25.684) for iOS 6.0+

* (ZD #19629) - Live Video Pauses when Entering Airplay to ATV 4

This issue was resolved by adding a waiting period after removing old items but before adding new items to the `AVQueuePlayer`. Without the waiting period, notifications are sent to the incorrect item.

* (ZD #19856) - No subtitles display when enabled by default

The issues in the webvtt playlist, which was causing the subtitles to not display correctly, has been fixed.

* (ZD #21590) - Video Performance and Tracking in Latest Origin Builds

The issue about the missing video length in `VideoAnalytics` has been fixed.

* (ZD #20202) - Setting custom subtitles styling crashes the iOS app

This issue was resolved by adding additional null object checks while setting subtitle styles.

* (ZD #20709) - video length reported as 0 in video start tracking

This issue is the same as (ZD #21590).

* (ZD #22280) - Analytics Video Length being set to 0

This issue is the same as (ZD #21590).

* (ZD #22592) - Issues with Airplay in Primetime

This issue is the same as (ZD #19629).

* (ZD#22922) - Manual bitrate switching for iOS

This issue was resolved by providing an option to specify the max bitrate.

* (ZD #23084) - Apple Compliance for IPv6-Only Networks

The symbols that were not recommended by Apple for IPv6 compatibility have been removed.

**Version 1.4.24** (1.4.24.661) for iOS 6.0+

* ZD #2548) - Primetime support for interactive advertising on mobile - VPAID 2.0

This issue was resolved by updating the logic to un-hide player view if a VPAID ad fails to play.

* (ZD #20101) - Custom Chapter implementation fires chapter start event during ad playback

This issue was resolved by updating `VideoAnalyticsTracker` to properly detect chapter start/complete when transitioning between chapter  and non-chapters boundaries.

* (ZD #20784) - Analytics: Triggering content completes for live video transitions

This issue was resolved by adding a logic to manually trigger the completion of content during a video tracking session.

The following libraries were updated:

* AdobeMobile library to 4.10.0
* VHL library to 1.5.6
* VHL-Nielsen library to 1.6.7
* (ZD #21855) - Subtitles do not play after mid-roll

In this issue, duplicate discontinuity tags were causing subtitles to not appear after mid-roll. This issue was resolved by removing the discontinuity tags that are next to each other.

* (ZD #21994) - String out-of-bounds in `PTHLSUtils`

The most likely cause of the crash is when an EXT-X-KEY has a URL that is surrounded by quotes.

* ZD #22074) - `AUDVAST` Crash happening once a minute on iOS

In version 1.4.23, the crash that was caused by the presence of unsafe characters in a VAST redirect URL was fixed. However, TVSDK was continuing to skip these ads.

This issue was resolved by handling the unsafe characters and by allowing the ads to play.

* (ZD #22694) - `PTMediaPlayer`.  View  is hidden by  player

This issue was resolved by updating the logic to un-hide player view if a VPAID ad fails to play.

**Version 1.4.23** (1.4.23.641) for iOS 6.0+

* (ZD #18016) - No response from Primetime SDK with a bad network condition

This issue was resolved by improving error notification when a fatal error from `AVFoundation` occurs and to allow the app to handle the restart after the error.

* (ZD #20580) - Crash in `PTSplicerManager`

This issue was resolved by providing additional protection from concurrency issues that causes the crash.

* (ZD #21782) - iOS Error Code 10100

The issue where the TVSDK was returning a 101000 error while starting playback on Adobe Access DRM streams has been fixed.

* (ZD #21889) - Online Ads and offline content playback fails

The issue where playback was failing after an ad on AES encrypted offline content has been fixed.

* (ZD #22074) - AUDVAST Crash happening once a minute on iOS

This issue was resolved by improving the handling of third-party VAST ad tags that have invalid characters in the URL.

* (ZD #22257) - The TVSDK fails to play back DRM stream

The issue where the TVSDK that was returning a 101000 error while starting playback on Adobe Access DRM streams has been fixed.

**Version 1.4.22** (1.4.22.627) for iOS 6.0+

* (ZD #18709) - Crash in the TVSDK for iOS

The issue about a crash occurring on some Adobe Access DRM protected streams has been fixed.

* (ZD #18850) - Update creative selection logic based on CRS rules

This issue was resolved by adding a .json configuration file to specify the creative selection priority.

* (ZD #19770) - Protected AES Video feed not playing anymore

The issue where certain 302 redirected streams were failing to play has been fixed.

* (ZD #19629) - Live Video Pauses when Entering Airplay to ATV 4

This issue was resolved by adding a workaround for live video pausing when airplay is turned on for Apple TV 4 devices. The issue appears to be an Apple TV 4 issue.

* (ZD #21119) - The TVSDK is stalled after ad playback

Support has been added for AES encrypted streams with a sequence IV while using ad insertion.

* (ZD #21125) - Return from live/linear ad break early

Support has been added for returning from an ad break early before the ad break is played to completion. Early return is indicated through a custom manifest tag.

* (ZD #21224) - Airplay support for tokenized streams from Akamai

APIs have been added to the `PTNetworkConfiguration` class to append cookies as URL parameters on segments for certain Akamai tokenized streams.

* (ZD #21287) - Extraneous Log

An issue with some log statements shown by default in the  xcode  console even when logging is disabled has been fixed.

* (ZD #21446) - Ad Break events sometimes not triggered by the  TVSDK

On EVENT streams,  ad  breaks are not triggered correctly in the previous release build. This build addresses this issue.

**Version 1.4.21** (1.4.21.605) for iOS 6.0+

* (ZD #20749) - Fallback skips non-empty VAST responses; Extra ad tracking URLs fire

An issue with duplicate pings on fallback ads has been resolved.

**Version 1.4.20** (1.4.20.590) for iOS 6.0+

* (ZD #18639) - The  TVSDK  is using excessive CPU/resources on a lengthy hot-recording asset

The excessive CPU/resources usage has been fixed in the two levels. First by letting the time update function run on a global queue, instead of the main thread, and by optimizing the CPU usage for parsing the manifest with the previously processed and cached m3u8.

* (ZD #19349) - Pre-Roll ads are being skipped when throttling the network connection.

This issue was resolved by providing a timeout event (requestTimeout) to the application and the `adMetadata.adRequestTimeout` API to override the default 10-secs timeout.

* (ZD #19446) - Missing Notification on Live streams

This issue was resolved by allowing the application subscribe to the `EXT-X-PROGRAM-DATE-TIME` on live streams.

* (ZD #19459) - Crash when preparing alternate audio with `PTMediaPlayerItem` `prepareAudioOptionsWithAVMediaSelectionOptions`
* (ZD #19460) - Crash - `[PTMediaPlayerItem prepareSubtitlesOptionsWithAVMediaSelectionOptions:nonForcedOptions:]`

This issue is the same as Zendesk #19459.

* (ZD #19574) - The TVSDK is not returning M3U8 response data for DRM or non-DRM content

In the initial load of the manifest file in `PTMediaPlayerItem.prepareToPlay`, if loading the manifest failed, the TVSDK does not report the body of the failure response to the application.

This issue was resolved by allowing the TVSDK to report the failure response as an error to the application.

* (ZD #19615) - Fallback logic is not working

In the current implementation, fallback ads were skipped and were not repackaged unless these ads are in the m3u8 format. This issue was resolved by also adding the support for repackaging fallback ads.

* (ZD #19770) - The TVSDK fails to play any protected AES content with 302 redirect

The redirect issue was fixed, because the redirect URL was getting wiped out by `cleanConnectionData` before it could be used to parse the manifest.

* (ZD #19856) - Subtitles aren't displaying for some bit-rates when enabled by default

This issue was resolved by handling the error from iOS for the segments of the streams where the subtitles do not display.

* (ZD #19868) - The TVSDK crashes when an invalid creative is trafficked

The crash in the  TVSDK  that was incorrectly de-allocating an instance of the vast parser has been fixed.

* (ZD #20180) - VPAID ads get skipped occasionally

JavaScript mime type was not always being included or considered as a valid mime type. This issue was resolved by including JavaScript as a valid mime type.

* (ZD #20749) - Fallback skips non-empty VAST responses; Extra ad tracking URLs fire

The issue where some of the creatives are not being repackaged has been fixed.

**Version 1.4.19** (1.4.19.563) for iOS 6.0+

* ZD #18639) - The TVSDK uses excessive CPU/resources on a lengthy hot-recording asset

This issue was resolved by optimizing the DRM m3u8 playlist rewrite to cache bits of the playlist that have been previously rewritten. This is most relevant when you play back live m3u8 streams for  which the  m3u8 is downloaded after every segment download.

* (ZD#18956) - `player.drmManager` is nil when the breakpoint is set in iOS Demo Player

This issue was resolved by updating the `PTMediaPlayer.drmManager` API implementation to pick up DRMManager from the DRM framework.

**Version 1.4.18** ( 1.4.18.557) for iOS 6.0+

* (ZD #18844) Tracking playhead for live content in the iOS player.

This issue was resolved by allowing the applications to set their own  playhead  value.

* (Zendesk #18518) - If the video name is not specified, the TVSDK's name defaults to * PSDK-based  player.*

This issue was resolved by removing the default value for the player's name.

**Version 1.4.17** (1.4.17.545) for iOS 6.0+

* (Zendesk #2228) - Enhance the  TVSDK  to return JSON response of the fetching of a manifest

Instead of sending an error when the content is not M3U8, the DRM Framework returns a nil DRMMetadata. The issue was resolved by adding metadata to expose content when the M3U8_PARSER_ERROR notification occurs.

* (Zendesk #2231) - Error returned from fetching the manifest unavailable in MediaPlayerNotification

Same resolution as Zendesk #2228

* (Zendesk #3304) - VAST 3.0 `[ERRORCODE]` macro not being populated

The issue where the [!DNL Auditude] SDK is failing to send a ping when the tracking URL has spaces at the beginning has been resolved.

* (Zendesk #17294) - Crash [!DNL SecKeyRawSign]

A possible crash when the customer's code uses the key chain has been resolved.

* (Zendesk #18008) - Support cookies for iOS8+ to support tokenized streams

Akamai tokenized streams require that cookies be sent on segment requests, and this was not possible on iOS 7 and earlier. Starting in iOS 8, Apple has added an API that allows cookies to be passed for segment requests. This support is now available in the TVSDK. Support has also been added for sending a user-agent, if available.

* (Zendesk #18166) - TVSDK 1.4.15 gives hundreds of warnings when compiling with `DWARF` with `dSYM` file options

All of the warnings have been resolved.

**Note**: tvOS-compatible libraries have been added for TVSDK .

**Version 1.4.16** (1.4.16.1454)

* Zendesk #3875 - Tab S Crashes during playback

Reverting the dependency of OKHTTP on [!DNL Auditude] for CRS because TVSDK is now directly using the `httpurlconnection` instead of curl. The issue was resolved by clearing exceptions before making another JNI call.

* (Zendesk #4487) - Tracking Linear Channel of Content

The issue was resolved by re-initializing the video heartbeat tracker during a linear stream playback session.

* (Zendesk #17919) - Android - content seek causes heartbeat error

The issue was to resolve the heartbeat in an error state when there is a seek in a chapter

* (Zendesk #18053) - Application using the TVSDK crashes on Marshmallow

The TVSDK was crashing on Android™ M OS when the TVSDK library uses neon code that does YUV `->` RGB color conversion. This issue was resolved by updating the functions that are causing this issue by using non-neon version of `code`.

* (Zendesk #18072) - Android M - Application Crash

This crash happens while calling `MediaCodecList` and `MediaCodecInfo` APIs when checking whether the profile and level are supported. Adobe is seeking Google's support for additional insight. This issue was resolved by providing a temporary work-around by loading all the codec info ahead of time to avoid calling these APIs only when codec information is needed.

* (Zendesk #18074) - Arabic subtitles not working on Nexus with Android™ 6.0

This issue was resolved by supporting the Android™ CTS font map.

**Version 1.4.15** (1.4.15.512) for iOS 6.0+

**Note**: The Nielsen module has been removed from the TVSDK build, but the TVSDK will be updated soon with a new Nielsen integration module.

* (ZD #2228) - Error returned from fetching the manifest unavailable in `MediaPlayerNotification`

Added metadata to expose content when the notification `M3U8_PARSER_ERROR` occurs.

* (ZD #4437) - Crashes inside Adobe Primetime SDK

Fixed a reported crash when preparing subtitles/alternate audio.

* (ZD #4487) - Tracking Linear Channel of Content

Allowed re-initializing of the video heartbeat tracker during a linear stream playback session.

**Version 1.4.14** (1.4.14.498) for iOS 6.0+

* (ZD #17260) - Crash on `playlistManagerForURL`

Fixed an intermittent crash due to concurrency issues.

**Version 1.4.13** (iOS 6.0+)

* (ZD #3304) - VAST 3.0 `[ERRORCODE]` macro not being populated

  * Error code 400 is exposed if inline ad has bad creative.
  * `[ERRORCODE]` macro is URL encoded.

* (ZD #3865) Heartbeat integration with IMA ads

Fixed a bug where the video length was being reported incorrectly.

* Updated TVSDK demo player to support iOS 9

To properly support iOS 9, you must configure the exceptions of the Application Transportation Security. For the demo, the ATS is disabled completely.

**Version 1.4.12** (1.4.12.464) for iOS 6.0+

* (ZD #4521) CRS Testing Client Side and SSAI

Fixed incorrect reverse MD5 in 3P URL.

**Version 1.4.12** (1.4.12.463) for iOS 6.0+

* (ZD #2751) CSAI and CRS / Enhance: Handle dynamic elements in certain media file URLs.

Updated Creative Repackaging Service to properly handle ads with dynamic creative URLs.

* (ZD #3654) Memory Leak in PSDK version after 1.3.4.166

Fixed memory leak in `drmFramework` with regular playback on iOS 8.2 devices

* (ZD #3988) Preroll is skipped when seeking back into it after first playback

Fixed a bug so that ad policies could be properly disabled.

* (ZD #4017) Requesting iOS API to force ad playback on backwards seek

Resolved with fix for ZD #4279

* (ZD #4279) HLS TVSDK ad insertion -302 redirect issue on iOS and Desktop

Fixed bug when an Ad asset was using a relative redirect URL

**Version 1.4.9** (1.4.9.427) for iOS 6.0+

* (ZD #3075) Internet Reachability Issue - iOS

Added notification to detect when the playback has stalled.

* (ZD #3193) Request for a Profile change API in  TVSDK

Updated `PTPlaybackInformation` to expose the updated indicated Bitrate. Updated `BITRATE_CHANGE` notification to be more time reliable and accurate to the M3U8 reported bit rates.

* (ZD #3324) Primetime ads reporting issue when no ad media in VMAP

Support for pinging empty ad break tracking URLs, TVSDK now verifies ad break start and complete pings for empty ad breaks.

**Version 1.4.8** (1.4.8.402)

* (ZD #3158) IOS 7 crashes in Full Event Replays

**Version 1.4.7** (1.4.7.382)

* (ZD #2197) Tracking ad errors. Added notification for asset failed to load manifest.
* (ZD #2894) Player Makes four top-level manifest requests during playback.
* (ZD #2992) [!DNL Auditude] Reporting weird durations and identifiers.

**Version 1.4.6**(1.4.6.325)

* (ZD #2197) Tracking ad errors. Added notification for asset failed to load manifest

**Version 1.4.5** (1.4.5.283)

* (ZD #2141) Analytics implementation for [!DNL TreeHouse] app, added `AdobeAnalyticsPlugin.a` library to build  package .
* Video Heartbeats Library update to 1.4.1.2
* (PTPALY-4226) (related to ZD #2423) Performing DRM Reset can result in deletion of Application Document data.

**Version 1.4.4** (1.4.4.242)

* Video Heartbeats Library (VHL) update to 1.4.1.

* (ZD #2435) TV SDK documentation on analytics needs updates

**Version 1.4.2** (1.4.2.210 : iOS 6.0+)

* (ZD #1129) `_player.currentItem.audioOptions` returning empty
* (ZD #2109) Primetime PSDK 1.4.1.125 doesn't work with Xcode 5.1.1
* (ZD #2137) Crash in PSDK on iOS when DRM metadata cannot be loaded

**Version 1.4.1**(1.4.1.125)

* (ZD #1107) [!DNL CocoaLumberjack] duplicate symbols
* (ZD #1644) Modify iOS User Agent for Targeting and Reporting
* (ZD #1850) Cocoa Lumberjack files included in iOS SDK
* (ZD#1908) Custom Tags are ignored by PSDK if there is more than 1

**Version 1.4.0** (1.4.0.32)

* Zendesk #1024 - Feature to remove ad from stream via manifest

## Device certification and support {#device-certification-and-support}

>[!NOTE]
>
>The following features are **not** supported in the  TVSDK :
>
>* Slow motion, on any platform or version.
>* Live trick play.

**Version 1.4.43**

* TVSDK 1.4.43 is certified for iOS 11.

**Version 1.4.29**

* TVSDK 1.4.29 has been certified for iOS 10.

**Version 1.4.28**

* TVSDK 1.4.28 has been certified for iOS 10 Beta 7.
* DRM support to force HTTPS by adding  `forceHTTPS`  and `isForcingHTTPS` APIs.
* Updated VHL libraries to 1.5.8, Adobe Mobile libraries to 4.8.4, and the logger utility library to the version 7.0 deployment target.

**Version 1.4.19**

This version of the  TVSDK  has been certified with the FairPlay Support for iOS and tvOS.

**Version 1.4.17**

* tvOS

  This version of the  TVSDK  includes support for tvOS and has been certified for unencrypted HLS streams.

  **Note**: Remember the following compilation guidelines:

  * TVSDK tvOs support is limited to non-Adobe DRM encrypted streams. You must remove the reference to `drmNativeInterface.framework` in your tvOS build settings. AES encrypted streams are still supported.
  * Apple requires all Apple TV applications to be bitcode enabled, so you must turn on this flag in your project settings.

## Known issues and limitations {#known-issues-and-limitations}

* Due to deprecation of iOS UIWebView class, in iOS TVSDK 3.6 onwards:
  * VPAID ads do not play as expected in iPad 13.
  * Companion ads do not play as expected.

* In iOS TVSDK, all ads are stitched into the content manifest. Ad behaviors are implemented by seeking based on the duration of the content and ad segments. So if segment durations are not accurate, seeking may not always end at the exact frame of the beginning or end of ad break. Even if durations are to the frame, there is a tolerance that the platform itself imposes on seeking and there may be a few frames or ad or content displayed. This is a limitation of the platform and the way ad insertion works with TVSDK on iOS.
* The decision to skip happens on the seek event in this case. However, since the ad segment durations in the manifest do not accurately represent the actual duration of the ad, the seek is not frame accurate. Hence, you see a few frames of ad when the ad policies are applied.
* It might experience that License rotation video does not play on iOS 11 and it will play fine on iOS 9.x and iOS 10.x.
* In VPAID 2.0 support, if the playback is active over AirPlay, VPAID ads are skipped.
* The `drmNativeInterface.framework` does not link correctly when the minimum target is set to iOS7 (or later).
  Workaround: Explicitly specify the `libstdc++.6.dylib` library as follows: Go to **[!UICONTROL Target]** > **[!UICONTROL Build Phases]** > **[!UICONTROL Link Binary With Libraries]** and add `libstdc++.6.dylib`.
* Post-Roll Ad not getting inserted for replace API.
* Seeking in an ad break (without coming out of it) issues a duplicate ad start and ad break notification
* Setting `currentTimeUpdateInterval` does not have any effect.
  Note: In certain iOS versions, the OS doesn't load the resources inside the `PSDKLibrary.framework` automatically. It is important to manually copy the `PSDKResources.bundle` to the application's bundle resources: Go to **Build Phases** and copy bundle resources.
* The Reference App cannot be built using Xcode 8 or lower versions. iOS TVSDK version 1.4.41 onwards, use Xcode 9 to compile.
* VPAID ads do not honor the `delayAdLoadingTolerance` value.
* 24077- For certain HLS contents with subtitles, player crashes on _Stop_ or _Reset_ method.
* Detailed Error notifications are not available in case when Just in Time Ad resolving is enabled.
* Error notifications are logged as per ad resolution time and not as per ad sequence.
* HEVC support has following limitations in this release
  * DRM not supported
  * CC (CEA 608/708) support not available as it is not supported in CMAF.
  * 4K support is not yet present.
  * ID3 tags support not available as it is not supported in CMAF.
  * Unmuxed Live HEVC streams not verified.
  * HEVC Ads support not verified.
* With JIT enabled and tolerance set to 10 seconds, no VAST call is seen for the first midroll ad break if there are VMAP > VAST redirect ads.
* For Ad resolution time-out to work properly, each time the playlist is updated during live stream playback, the player expects a stitched playlist within 20 sec. If it does not receive a stitched playlist within the said interval, an internal error is thrown and the player stops. 

## Helpful resources {#helpful-resources}

* [TVSDK 3.4 for iOS Programmer's Guide](/help/programming/tvsdk-3x-ios-prog/ios-3x-introduction/ios-3x-overview/ios-3x-overview.md)
* [TVSDK iOS 3.4 API reference](https://help.adobe.com/en_US/primetime/api/psdk/appledoc_v34/index.html)
* See complete help documentation at [Adobe Primetime Learn & Support](https://experienceleague.adobe.com/docs/primetime.html) page.
