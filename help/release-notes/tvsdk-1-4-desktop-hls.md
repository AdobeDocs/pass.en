---
title: TVSDK 1.4 for Desktop HLS Release Notes
description: TVSDK for Desktop HLS Release Notes describe what is new or changed, the resolved and known issues in TVSDK DHLS.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 5e227c99-acf6-4b16-a35a-68e2928fdbfd
---
# TVSDK 1.4 for Desktop HLS Release Notes {#tvsdk-for-desktop-hls-release-notes}

TVSDK for Desktop HLS Release Notes describe what is new or changed, the resolved, and known issues in TVSDK DHLS.

## New features {#new-features}

**1.4.31**

* **Multi-CDN Support for CRS Ads**

  * By default, all transcoded assets will be hosted on Adobe-owned CDN on Akamai. With the latest release, Adobe Creative Repackaging Service (CRS) provides the ability to upload the transcoded creatives to multiple CDNs as specified by the customer.
  * New APIs are added to TVSDK to enable specifying the final CRS creative url when the default URL is not used. Please refer to the documentation to learn how to use these new APIs.

### New features in the previous releases {#new-features-previous}

**1.4.30**

* **Billing Metrics**

To accommodate customers who want to pay only for what they use, rather than a fixed rate regardless of actual use, Adobe collects usage metrics and uses these metrics to determine how much to bill the customers. 

**1.4.24**

* **Persistent Network Connection**

Important: You must have at least Adobe Flash Player version 22 or later installed.
Persistent network connections create and store an internal list of network connections that can be reused for multiple requests, instead of opening a new connection for each network request. Persistent network connections should increase efficiency and decrease latency in your networking code.

In this release, this feature is not supported in Apple Safari and Mozilla Firefox on a Mac.

**1.4.19**

* Stream integrity support for VPAID ads.
* Enabled the mute tab option in Flash player FP 20.0.0.267 for Firefox 42 and later by fixing the hang issue.

**1.4.18**

* Primetime Desktop HLS TVSDK now supports VPAID 2.0 Linear SWF creatives to enable a rich interactive in-stream ad experience.

**1.4.10**

* **Ad Fallback, Daisy chaining in ad selection logic (Zendesk #3103)** For VAST ads (creatives) with the fallback rule enabled, the TVSDK treats an ad with an invalid MIME type as an empty ad and attempts to use fallback ads in its place. You can configure some aspects of fallback behavior.

For more information, see [Ad fallback for VAST and VMAP ads](../programming/tvsdk-1.4-for-android/ad-insertion/ad-fallback/android-1.4-ad-fallback.md).

**1.4.8**

* **Video Heartbeats Library (VHL) updated to version 1.5**

  * Ability to send metadata with video start and/or video/ad/chapter start as context data
  * Less network traffic - Heartbeats are fewer on average and smaller in size.

**1.4.7**

* **On-Premise Individualization Support**

Support for on-premise installations of the Adobe Individualization Server to customize the client's individualization request to go to a different endpoint.

**1.4.6**

* **Sample AES encryption (requires Flash Player version 17.0.0.134)**

Sample-based AES encryption is now supported.

**1.4.2**

* **Video Heartbeats Library (VHL) update to version 1.4.0.1**

  * Added the ability to bundle different analytics use cases, from other SDKs or players, with the Adobe Analytics Video Essentials.
  * Ad tracking has been optimized by removing the trackAdBreakStart and trackAdBreakComplete methods. The ad break is inferred from the trackAdStart and trackAdComplete method calls.
  * The playhead property is no longer needed when tracking ads.

**1.4.0**

* **Blackout Signaling With Alternate Content Replacement** As part of the 1.4 TVSDK update, the TVSDK also now supports going into and returning from regional blackouts against linear content. The TVSDK can now process two manifest files in parallel, main and alternate, to monitor for blackout signals even when alternate programming is being shown in place of the original programming.

* **Remove/Replace C3 Ads** Now, no additional prep work is needed to dynamically insert new ads into video-on-demand (VOD) assets that are coming out of the C3 window. The TVSDK now provides an API to remove custom content ranges and dynamically insert new ads. This powerful new functionality is also useful in cases where live/linear content airs during broadcast and is immediately pulled down for use as on demand content without proper time to "clean" the asset.

## Resolved issues {#resolved-issues}

>[!NOTE]
>
>All TVSDK customers who use CRS are strongly encouraged to upgrade to at least TVSDK 1.4.32 on iOS, Android, and Desktop HLS. This upgrade will be a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example,
>
>`https://adunit.cdn.auditude.com/assets/3p/v3.1/218747/94b/c1b/94bc1b964cc67e115a5a6781c7329b90_ee92607938ffff46b083121f044c2746.m3u8`

**Version 1.4.41**

* Zendesk #33777 - Localhost token SWF for DHLS distribution build expired.

  Updating the localhost token for PMP demo on DHLS.

### Resolved issues in the previous releases {#resolved-issues-previous}

**Version 1.4.38** (891)

* Zendesk #30731 - TVSDK does not playing multiple VPAID ads in an AdBreak.

  Fixed Multiple VPAID ads playback in an AdBreak.

* Zendesk #29968 - Double Billboard.

  The video player can repeat the last segment of a period when an ABR switch happens. Due to this, at times, last segment of preroll repeated. This has been fixed.

**Version 1.4.35** (879)

* Zendesk #26058 - Supports Native VPAID events

**Version 1.4.33** (873)

* Zendesk #21701 - Send the original creative URL for 1401 CRS request instead of the normalized url.

  The issue where already repackaged URLs are being requested for transcoding has been fixed, as per the required by the CRS back end.
* Zendesk #26197 - Anamorphic Compression not replayed in desired Display Resolution.

  **Note**: This issue requires Flash player 24.0.0.194 or later.

  The issue where missing entries in the aspect ratio tables were used to calculate the output width has been fixed.

* Zendesk #26840 - HDCP detection failing on IE11 + Windows7 after second attempt.

  **Note**: This issue requires Flash player 24.0.0.218 or later.

  This issue was resolved by modifying AdobeCP's main message queue processing to iterate through the whole queue, instead of just blocking on the very first message.

* Zendesk #27460 - The new Akamai account is unable to handle a POST CDN request.

  The new CDN account is unable to handle a POST CDN request. This issue was resolved by updating the code to make the cdn.auditude.com ad request be GET instead of POST.
* Zendesk #27619 - Flash crash on Windows 10

  **Note**: This issue requires Flash player 24.0.0.218 or later.

  This issue was resolved by preventing a fault as the result of long URLs.

* Zendesk #28218 - Tracking event does not fire while the plackback from the resume point

  This issue is the same issue as in Zendesk #26592. The issue where seek operations were allowed when the media player is in the PREPARED state for VOD streams has been fixed.

**Version 1.4.32** (867)

* Zendesk #26592 Tracking event does not fire when the playback starts from the resume point

The code was not updating the pre-roll ad break item when the resume point was not zero. This issue was resolved by adding logic to refresh the code when the range start times do not match.

* Zendesk #27022 Ads are not being played the second time an asset is played

The exceptions with the array methods have been fixed.

**Version 1.4.30** (855)

The following issues were resolved for TVSDK in this release:

* Zendesk #22898 - Missing subtitles should not cause playback to fail.

**Note**: This issue requires Flash player 23.0.0.185 or later.

This issue was resolved by allowing TVSDK to continue the playback, even if the manifest is missing the WebVTT M3U8, and just register a warning.

* Zendesk #23454 - Third party ads (VPAID) are not handled correctly

This issue was resolved by handling of VPAID ads correctly based on content IDs rather than time ranges.

* Zendesk #24528 - TVSDK Usage Metrics for Billing.

Important: This issue requires Flash player 23.0.0.185 or later.

* Zendesk # 25432 Closed Caption issue during resizing the player.

Important: This issue requires Flash player 23.0.0.185 or later.

The caption display texture map code has been fixed to properly handle the coordinates during the player resizing.

The Video Heartbeat Library (VHL) has been updated to version 1.5.9 to resolve the following issues:

* Zendesk #23730 - Bitrate metrics are empty

This issue was resolved by tracking the bitrate changes in VideoAnalyticsTracker.

* Added a new API, assetDuration, to PTVideoAnalyticsTrackingMetadata to update asset duration for Live/Linear streams.

**Version 1.4.28** (848)

* Zendesk #25027 - Auditude doesn't work in 1.4.27 desktop release

This issue was resolved by adding the code to check the AUDITUDE_METADATA_KEY and by making the AUDITUDE_METADATA_KEY and ADVERTISING_METADATA_KEY interchangeable.

* Zendesk #24428 - Frequent buffering issue using TVSDK to play a DRM HLS

This issue was resolved by taking into account that when there is no ad setup, TVSDK can speed up processing by eliminating the pre-roll ad hold and live reservation hold on the timeline that is designed to synchronize ad insertion.

* Zendesk #24344 - Disable WebVTT files to improve start up times.

**Note**: This issue requires Flash player 23 or later.

This issue was resolved by loading the WebVTT files only when captions are required to be displayed.

* Zendesk #24994 - Closed captioning is dropped off the player when returning from commercial break

**Note**: This issue requires Flash player 23 or later.

The spurious EOC code caused the caption display to disappear. This issue was resolved by forcing the 608 captions codes RU2, RU3 and RU4 to provide the correct visibility in the current active window.

**Version 1.4.27** (844)

* Zendesk #21554 - TVSDK error beacons not fired for application-type = video/mp4

This issue was resolved by enabling TVSDK to ping the correct error tracking URLs on invalid asset formats.

* Zendesk #23402 - Incomplete ad playback

**Note**: This issue requires Flash player 23 or later.

After getting a 404 error on certain requests, a crash might occur. This issue has been resolved by ensuring that the connection does not shut down while the response is being handled. The resolution ensures that the VPAID ad files are not counted incorrectly, so they do not get released while they are downloading.

* Zendesk #23621 - Retry is failing on 400 and 404

**Note**: This issue requires Flash player 23 or later.

Fixed the issue that caused a DRM metadata corruption when switching between different profiles.

* Zendesk #23705 - Video Ads freezing during AdStitched breaks

**Note**: This issue requires Flash player 23 or later.

This issue is the same issue as in Zendesk #23621.

* Zendesk #23905 - Some Ad breaks skip on ad breaks

**Note**: This issue requires Flash player 23 or later.

The Windows native networking code has been fixed to ensure that connections do not close handles that are currently being used by other connections.

* Ticket #24029 - HLS FER streams do not playback all of the mid-roll ads in the mid-roll .json file.

This issue was resolved by allowing clients to set custom parameters separately on Opportunity instance so that clients do not have to override OpportunityGenerator.

**Version 1.4.26** (839)

* Zendesk #18854 - Update creative selection logic based on CRS rules
  * Provided the support to update creative selection logic based on CRS rules

* Zendesk #22725 - playbackManager.beginPlayback() implementation in the sample application for Desktop

  * Fixed by removing this redundant call at the end of startPlaybackFromFlashVars as the method is called from setupVideo()

* Zendesk #22807 - SeekManager null reference exception

  * Fixed by providing the necessary NULL pointer protection inside of SeekManager relating to _dispatcher

* Zendesk #22822 - Frequent buffering when using TVSDK to play a clear HLS

  * Fixed by removing the initial opportunity generated by adSignalingModeOpportunityGenerator if there is no ad

* Zendesk #23378 - Stream integrity blocks rules.xml

  * Fixed by loading rules.xml file through the stream integrity workflow

**Version 1.4.24** (817)

* Zendesk #19851 - When the player adapts to a different bit rate it jumps a few frames back in time on the new bit rate making an awkward experience

**Note**: This issue requires Flash player 22.0.0.175 or later.

The issue where the DRM adapter is reset after downloading a small fraction of a segment does not get restored properly has been resolved.

* Zendesk #20784 - Analytics: Triggering content completes for live video transitions

This issue was resolved by adding an API (trackVideoComplete) to manually trigger the completion of content during a LINEAR/LIVE video tracking session.

The following libraries were updated:

* Zendesk #21643 - VPAID ads do not play in full

    * AdobeMobile library to 4.10.0
    * VHL library to 1.5.6
    * VHL-Nielsen library to 1.6.7

This issue was resolved by using a zero-height viewport to fill the stage when a VPAID ad is playing.

* Zendesk #22110 - Analytics: Add a h:sc:ssl field to the heartbeat tracking calls

The SSL-related issues were fixed, and the VHL library that is used in TVSDK has been updated to the latest version.

* Zendesk #22608 - Video intermittently shows a black screen (requires Flash Player 22.0.0.175 or later)

During adaptive bitrate, with the max bitrate limit, the reloading of the video intermittently shows a black screen even though the client sees updates to position, and the client behaves as though it is playing content.

**Version 1.4.23** (809)

* Zendesk #2887 - Post-roll ad skipping issue when Ad Rule logic applied to the TVSDK

**Note**: This issue requires Flash player 21.0.0.240 or later.

The issue where the post-roll ads were being skipped when the ad rule logic was applied to the TVSDK has been fixed.

* Zendesk #19863 - Ad with VPAID media file discarded

If a vast inline ad has multiple media files with a VPAID ad being the first ad, the inline ad is not played for live streams. This issue was resolved by picking up a different media file instead.

* Zendesk #21021 - Late Binding Audio causing audio segment repeats

**Note**: This issue requires Flash player 21.0.0.240 or later.

The audio repeating issue has been fixed.

* Zendesk #21125 - Return from live/linear ad break early

**Note**: This issue requires Flash player 21.0.0.240 or later.

This release provides support for returning from an ad break early before the ad break is played to completion. Early return is indicated through a custom manifest tag.

* Zendesk # 21369 Late binding audio causes an inconsistent time

**Note**: This issue requires Flash player 21.0.0.240 or later.

The audio repeating issue that was fixed has also fixed this issue.

* Zendesk #21760, 20921 - Audio Video Desync on Seek.

**Note**: This issue requires Flash player 21.0.0.240 or later.

The audio repeating issue was fixed.

* Zendesk #22024 - Error when running the TVSDK

The issue where the reference player not playing any stream and was throwing an exception at start up has been fixed.

**Version 1.4.22** (791)

* Zendesk #17580 - Primetime runtime error with code 3357

**Note**: This issue requires Flash player 21.0.0.197 or later.

The random 3357 errors that occurred by properly initializing the deviceID when storeVoucher() is called has been fixed.

* Zendesk #21334 - TVSDK ad request timeout value for third party ad requests

In this release, global ad request timeout has been added.

**Version 1.4.21** (782)

* Zendesk #19580 TVSDK waits for completion of content resolver before sending `PTTimedMetadataChangedNotification` notifications

**Note**: This issue requires Flash player 21.0.0.182 or later.

This issue was resolved in the Desktop Reference Player by providing the ability to set Ad tags and adding a custom opportunity generator that shows how to subscribe to custom cues and how to process these cues in a VOD file.

* Zendesk #20806 Future mid-roll ads in DVR window won't trigger after Swapping cams

**Note**: This issue requires Flash player 21.0.0.182 or later.

This issue was resolved by updating the app to set _resource.metadata.setValue(DefaultMetadataKeys.ENABLE_LIVE_PREROLL, "false") to disable pre-roll ad insertion in a PIP swap and, as a result, no pre-roll opportunity is generated.

A sorting functionality was introduced to fix the out-of-sequence ad placement that resulted in a negative main content duration.

* Zendesk #20522: Can't skip VPAID 2.0 Ads

**Note**: This issue requires Flash player 21.0.0.182 or later.

* This issue was resolved by skipping VPAID ads during ad forgiveness.
* When the adbreak policy is set to skip, ad and ad break events are still dispatched. The player state is inconsistent.

This issue was resolved to behave correctly and not dispatch events when ad break is skipped.

* Zendesk #20955 Set key-value pairs in the customParameters property through the opportunity generator

**Note**: This issue requires Flash player 21.0.0.182 or later.

The Auditude Request parses the AuditudeSettings for custom parameters when creating an ad unit for advertising requests.

This behavior was changed to include custom parameters from the Opportunity object in the request. Also, multiple opportunities with different custom parameters cannot be packed in one Auditude request.

* Zendesk #21227 - m3u8 fail to play consistently

**Note**: This issue requires Flash player 21.0.0.211 or later.

This issue was resolved by allowing the TVSDK to ignore the manifest (HLS sub profiles) that contains the AC3 codec that the TVSDK does not support (surround).

**Version 1.4.20** (762)

* Zendesk #19181 - Trick play fast forward to live point locks up stream.

**Note**: This issue requires Flash player 20.0.0.306 or later.

* Zendesk #19286 - Flash Player crash occurred while seeking back and forth in a FER stream.

**Note**: This issue requires Flash player 20.0.0.306 or later.

The occasional hangs that occurred when seeking in Google Chrome were resolved by shutting down the queries, if the queries take too long to get a response or if the socket is being shut down.

* Zendesk #19305 - Choppy playback encountered when playing a stream with A/V discontinuities.

**Note**: This issue requires Flash player 20.0.0.306 or later.

This issue was resolved by reporting a warning.

* Zendesk # 19359 - Flash Player crashed due to the position of #EXT-X-FAXS-CM: attribute in set-level manifest.

This issue was resolved when #EXT-X-FAXS-CM tag appears at the top playlist before individual bitrate or segments in the playlist.

* Zendesk #19489 - Fast Forward to Live Point stalls plugin (live stream)

This issue is the same as Zendesk #19181.

* Zendesk #19699 - TVSDK fails to switch between WebVTT subtitle tracks

This issue was resolved by making the player dump and reload the manifest when a track changes and by correcting the UTF8 string conversion problem that affected the double-byte WebVTT caption track names.

**Version 1.4.19** (1.4.19.738)

* Zendesk #18234 - Flash Player crashes playing back the streams with Unicode strings in CC

This issue requires Flash Player FP 20.0.0.267 or later and was resolved by handling the Unicode string correctly.

* Zendesk #18304 - Stream Integrity Support for VPAID Ads

This feature requires Flash Player FP 20.0.0.267 or later and was introduced in release 1.4.19.

* Zendesk #18766 - Reference Player is unable to display non-Latin unicode characters in CC track names

This feature requires Flash Player FP 20.0.0.267 or later and was fixed by correctly handling the Unicode string.

* Zendesk #18804 - Player crashes in Firefox 42

This issue requires Flash Player FP 20.0.0.235 or later and is the same issue as Zendesk #18723.

* Zendesk #18864 - Flash Player full plugin crash

This issue requires Flash Player FP 20.0.0.235 or higher and is the same as Zendesk #18723.

* Zendesk #18998 - If audio & video timestamps do not match, an endless downloading of segments on discontinuity occurred.

This issue was resolved by ignoring the gap between timestamps and just playing the downloaded content.

* Zendesk #19093 - Mid-roll ads can only be watched once with live and full-event replay (FER) content, but these ads could not be watched again when fast-forwarding or seeking past the ads

In Primetime's default adPolicy selector, if a mid-roll ad is watched, the adBreak is not moved to the seeked position when you complete a seek. To play the ad again, after the seek, the application needs to override the selectAdBreaksToPlay() function.

* Zendesk #19101 - Rewinding into unresolved Midroll ads removes the ad placement.

This issue was resolved by allowing the player to update the playbackMetrics time, the minimumOpportunityTime, and the Timeline.

* Zendesk #19102 - Issues with FER and trick mode

This issue requires Flash Player FP 20.0.0.267 or later and was resolved by setting the advertisingMetadata.adSignalingMode correctly.

* Zendesk #19175 - Sometimes preroll ads do not display the first time the stream is played.

This issue was resolved by adding a new API, adRequestTimeout, to the AuditudeSettings for an ad request timeout. Users can now override the default 10s ad request timeout.

**Version 1.4.18** (1.4.18.722)

* Zendesk #3324 - Primetime ads reporting does not track ad breaks when there is no ad media in a VMAP.

When an ad break is empty, the ad break start and complete tracking events were not being pinged. This issue was resolved by sending ad break start pings on empty ad breaks, such as VMAP AdBreak, with a valid AdSource nod.

**Version 1.4.17** (1.4.17.702)

* Zendesk #17168 - Captions don't appear for 10 seconds or so after toggling visibility

This issue was resolved by providing support for the EXT-X-MEDIA-TIME tag for vtt caption files.

* Zendesk #17983 - Failing to download any keys for a manifest causes the entire manifest playback to fail

**Note**: You must have at least Flash Player FP 19.0.0.245 or higher.

When sometimes playing live content, there might be invalid keys in the manifest (for example, for blackout periods), but other time ranges might have valid keys and will still play. Previously, when a key that was listed in a manifest could not be downloaded, the entire manifest failed. Now, the manifest fails only when all of the listed keys cannot be downloaded. If some keys are valid, but some of these keys could not be downloaded, content will play. We will still fail if we try to play a segment that requires a key that we do not have.

* Zendesk #18554 - Stream Integrity trimming down the cookies in some cases

**Note**: You must have at least Flash Player FP 19.0.0.245 or higher.

A bug in the cookie manipulation code that might truncate cookie values was fixed.

**Version 1.4.16** (1.4.16.684)

* Zendesk #3732 - Add support for proxies in Chrome for Stream Integrity (requires Flash Player FP 19.0.0.207 or greater)

This is an enhancement.

* Zendesk #4244 - Streaming issues at PTS rollover

This issue was resolved by detecting rollover and managing the discontinuity per payload type and not generically.

* Zendesk #4487 - Tracking Linear Channel of Content

This issue was resolved by re-initializing video heartbeat tracker during a linear stream playback session.

* Zendesk #17427 - Adobe Stream Integrity not working through a proxy on Chrome (Win7) ()

**Note**: The resolution requires Flash Player FP 19.0.0.207 or greater.

This issue is the same as Zendesk #3732.

* Zendesk #17907 - Lag on pHLS Live Stream with Flash Player 19

**Note**: The resolution requires Flash Player FP 19.0.0.207 or greater.

This issue was resolved by handling the live streams where the domains of the TS files change when reloading the live manifest, and the files were downloaded twice.

* Zendesk #17931 - HLS content with slate at beginning fails playback

**Note**: The resolution requires Flash Player FP 19.0.0.207 or greater.

The issue was resolved by handling streams with no audio in the first 2 seconds of the first TS file.

* Zendesk #17934 - Live Streaming Failure with Flash 19.0.0.185

**Note**: The resolution requires Flash Player FP 19.0.0.207 or greater.

The issue was resolved by handling live streams with time interleaving between audio and video frames on segment boundaries.

* Zendesk #17973 - Latest Flash Player 19.0.0.185 crashes during mid-roll

**Note**: The resolution requires Flash Player FP 19.0.0.207 or greater.

The issue was resolved by handling unmuxed audio with mid-roll ad insertion. (The parser switch occurs, and at any point in playback, the content transitions to the mid-roll ad, or in middle of ad playback, and so on.)

* Zendesk #18049 - Flash 19 crash with Firefox 42 beta

This issue is the same as Zendesk #17973.

**Version 1.4.15** (1.4.15.678)

* Zendesk #4377: Fire AD_BREAK_SKIPPED event when skipping an ad break because of the ad policy.

The fix was to add AD_BREAK_SKIPPED if an ad is skipped.

* Zendesk #4496 - Stream Integrity: Error 102100 with redirects to tokenized streams.

The fix was to add support for setting the AVNetworkConfiguration property useCookieHeaderForAllRequests through the TVSDK.

* Zendesk #17179 - Flash player crashing on multiple SAP changes for encrypted content.

A crash during playback of some encrypted content was fixed.

**Note**: The fix requires Flash Player 19.0.0.200 or higher.

* Zendesk #17499 - how do we not remove midrolls after watch but remove preroll from fer content

Added a type to AdBreakTimelineItem (AdBreakTimelineItem.placementType) so that AdPolicySelector can return a different policy for pre-roll, mid-roll, and post-roll content.

* Zendesk #17665 - Bandwidth Throttling

The fix was to remove the logic to change the target buffer size to the initial buffer size when buffering begins.

**Version 1.14.14** (1.4.14.771)

* Zendesk #17363 - Fix README documentation for reference player

    * Clarify instructions for downloading and installing playerglobal.swc. 
    * Add instructions for updating project configuration with specific flash player version. 
    * Update AdvertisingOverlay project config to use minimum player version. 
    * Update ReferenceCore project config to use specific player version 11.9

* Zendesk #17471 - Player Freezes

Partial fix for an issue where an ad does not play from the beginning after seeking.

* Zendesk #17496 - Podbuster is not resolved when seeking back in DVR window

Provide custom parameters for each ad break.

**Version 1.4.13** (1.4.13.660)

* Zendesk #4037 - No Useable Profile Error (requires Flash Player 18.0.0.232 or greater)

fix url parsing problem when query paramer contains "http"

* Zendesk #4260 - Flash Player 18 crashes in IE11 (requires Flash Player 18.0.0.232 or greater)

Fixed a crash when playing video in fullscreen mode with IE11

* Zendesk #4262 - Adobe Primetime player crashes on windows 10 (requires Flash Player 18.0.0.232 or greater)

Fixed a crash when playing video in fullscreen mode with FireFox on Windows.

* Zendesk #4279 - HLS TVSDK ad insertion -302 redirect issue on iOS and Desktop

Fixed an issue where a URL was not getting its type recognized correctly because it had no extension

* Zendesk #4306 - Flash Player crash when going full screen on Win only (requires Flash Player 18.0.0.232 or greater)

Fixed a crash when playing video in fullscreen mode on Windows.

* Zendesk #4480 - Missing ID3 tag events (requires Flash Player 18.0.0.232 or greater)

**1.4.12 **(1.4.12.656)

* Zendesk #2751 - CSAI and CRS | Enhance: Handle dynamic elements in certain media file URLs.

Updated Creative Repackaging Service to properly handle ads with dynamic creative URLs.

* PTPLAY - 2114 - MP4 playback support.

Basic playback of MP4 content is now supported including play, pause and seek.

The following require Flash Player 18.0.0.225 or greater:

* Zendesk #3992 - Additional TrickPlay speeds.

TrickPlay now accepts rates higher than 16x: +/- 32, +/-64 and +/-128.

* Zendesk #3113 - Flash Player Plugin Crashing

Fixed crash when attempting to play a redirect ad on Mac Firefox.

* Zendesk #4037 - No Useable Profile Error 
* Zendesk #4262 - Adobe Primetime player crashes on windows 10

Fixed crashed in Windows Firefox during playback in fullscreen.

**Version 1.4.11** (1.4.11.648)

* Zendesk #1869 - Issue Changing Font Size (requires Flash Player 18.0.0.200)

Allow caption sizes to be used in WebVTT caption code.

* Zendesk #3113 - Flash Player Plugin Crashing (requires Flash Player 18.0.0.200) 
* Zendesk #3268 - Desktop: Video player starts flickering after +- 40/50 seconds and starts going black after +- 90 seconds (requires Flash Player 18.0.0.200)

Fix stage video bug.

* Zendesk #3670 - INVALID_PARAMETER error in VOD while seeking in the Reference Player (requires Flash Player 18.0.0.200)

InvalidateProfiles in ThreadSeek when new period is detected.

* Zendesk #3896 - Flash Player crash with Stream Integrity set to ON on Chrome (requires Flash Player 18.0.0.200)

Fixed crash in native networking mode in pepper

* Zendesk #3905 - TVSDK player does not load when hosted on CDN

Fixed issues finding wildcard token when the pageDomain is different from the swf domain.

**Version 1.4.10** (1.4.10.642)

* Zendesk #3249 - TVSDK Web Player crashes Flash on Firefox

Fixed a occasional Flash Player crash with Firefox on Mac when a stream, playing on an external monitor, would switch to a higher bitrate stream.(requires Flash Player 18.0.0.160)

* Zendesk #3268 - Desktop: Video player starts flickering after `+-` 40/50 seconds and starts going black after `+-` 90 seconds

Fixed an issue on Mac Chrome where stream would start to flicker an eventually go black. (requires Flash Player 18.0.0.161)

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` macro not being populated

    * error code 400 will be exposed if inline ad has bad creative. 
    * `[ERRORCODE]` macro will be URL encoded

* Zendesk #3601 - Enhancement request: Wrapper companion management

    * TVSDK will display wrappers companion that contains resources (html, iframe or static ) closes to the inline. ( if the inline does not contain one for that size) 
    * Wrappers companions with resource, unless use for display, will be ignore. (not use for tracking ) 
    * Only wrapper companions with NO resource will be used for tracking purposes. ( wrapper companion that only contain tracking )

**Version 1.4.9**

* Zendesk #2615 - issue removing HLS view from desktop display

Added clearVideo() method to MediaPlayer. Clears the displayed video frame by clearing the AVStream from the StageVideo object. Should only be called if the video is paused, and replaceCurrentResource or replaceCurrentItem must be called before play() can be called again.

* Zendesk #3169 - Update reference player with Adobe Analytics integration

Reference player has been updated with Adobe Analytics integration

* Zendesk #3296 - Desktop HLS TVSDK - VAST 3rd Party ads not playing

mime types for HLS format had been case sensitive, this was incorrect and has been changed so they are no longer case sensitive

**Version 1.4.8**

* Zendesk #2737 - Desktop Player - Error 106000 (requires Flash Player 17.0.0.184) 
* Zendesk #3007 - Pre-roll ads not appearing after updating to Flash Player 17 (requires Flash Player 17.0.0.184) 
* Zendesk #3085 - Desktop HLS Player Throws 106000 Error after 60 seconds (requires Flash Player 17.0.0.184)

**Version 1.4.7**

* Zendesk #2760 - DISCONTINUITY tag ignored during TrickPlay mode (requires Flash Player version 17.0.0.158) 
* Zendesk #2760 - DISCONTINUITY tag ignored during TrickPlay mode (requires Flash Player version 17.0.0.158)

**Version 1.4.6**

* Zendesk #2652 - Auditude documentation for desktop HLS, Clarified Auditude media_id for desktop HLS documentation

**Version 1.4.5**

* Zendesk #2256 - Access to Master Playlist, updated PSDK to dispatch timedMetadata events for subscribed tags on the master playlist. (requires Flash Player version 17.0.0.134) 
* Zendesk #2417 - Player trying to download subtitles before playback start, WebVTT was using the wrong segment number variable for segment number matching. Bug would only show up for media that had segment indices starting at zero. (requires Flash Player version 17.0.0.134) 
* Zendesk #2537 - Flash player crashes when using the pepper plugin with Chrome (requires Flash Player version 17.0.0.134) 
* Zendesk #2547 - Arabic subtitles: Text should be aligned right-justified (requires Flash Player version 17.0.0.134)

**Version 1.4.4**

* Zendesk #1561 - Re: `[Adobe Primetime]` Update: HLS client based failover support for PROGRAM-DATE-TIME in Desktop PSDK (requires Flash Player version 16.0.0.305 or greater) 
* Zendesk #2197 - `[Ads]` Tracking ad errors 
* Zendesk #2286 - Feature Request: Provide info on ad loading status (VPAID) 
* Zendesk #2285 - Feature Request: Skip ad after a specified timeout duration 
* Bug #3921755 - OpenSSL library update to version 1.0.1L in Flash Player (requires Flash Player version 16.0.0.305 or greater)

**Version 1.4.2**

* Zendesk #1303 - Vertical Offset for Closed Caption (requires Flash Player version 16.0.0.235 or greater, expected release date: December 2014) 
* Zendesk #1870 - Closed Caption Turning On & Off (requires Flash Player version 16.0.0.235 or greater, expected release date: December 2014) 
* Zendesk #2110 - Playback gets stuck after trying to enter fullscreen during a VPAID ad (requires Flash Player version 16.0.0.235 or greater, expected release date: December 2014) 
* Zendesk #2199 - `[VPAID]` Player not responding when seeking past ad break 
* Zendesk #2358 - Re: `[Analytics]` Incorrect chapter data

**Version 1.4.1**

* Updated Blackouts API to be consistent with Android and iOS implementation.

**Version 1.4.0**

* Zendesk #1024 - Feature to remove ad from stream via manifest 
* Zendesk #1423 - HLS playback failure is locking up Flash Player (with no error reported) 
* Zendesk #1674 - ClosedCaption Not showing up, correct 708 caption display when 0x03 ETX codes are missing.

## Known issues {#known-issues}

* Closed Caption will not work with audio-only content because the caption system needs video to work.
  Without video, there is no viewport dimension, and without a viewport dimension, you cannot display any graphics for captions.
* Stream integrity is slightly slower in Google Chrome because of Chrome sandbox restrictions.
* In TVSDK 1.4, if you disable autoPlay, a DRM error might occur when the player remains idle for at least a minute. To work around this issue, when you disable autoPlay but preload assets, modify `ReferenceCore.as` by changing the contents of `onPlaybackManagerPrepared`:

```
if (_playbackManager.autoPlay) {
_playbackManager.play();
} else {
_playbackManager.play();
_playbackManager.pause();
}
```

* **Version 1.4.13** PTPLAY-8501 - When VMAP returns two direct MP4 non transcoded ads, the same fall back ad plays twice.

* **Version 1.4.2** In the Flash Player version 16 release, an issue was identified with the ABR "switching down" logic, after the player gets into an empty buffering event. The issue prevents the bitrate from switching down in bad bandwidth environments once the player gets into a buffering state. To work around the issue, have your app set the `BufferControlParameters.initialBufferTime` to be the same as `BufferControlParameters.playbackBufferTime` temporarily during the buffering state (that is, on a `BufferEvent.BUFFERING_BEGIN` event) then reset it back to the set values on `BufferEvent.BUFFERING_END` event. The fix for this issue will be available in the next patch release of Flash Player verison 16.

* **Version 1.4.0**

    * PTPLAY-1634 - The same Subscribed tag has different timestamps in different live windows. When live windows move, the same tag in each of them should have the same timestamps. However, sometimes, the same tags have different timestamps.
    * PTPLAY-28 - MediaPlayer timeline does not include empty breaks.
    * A cross-domain policy file (crossdomain.xml) is required for permission to stream content from a different domain. [Setting a crossdomain.xml file for HTTP streaming](https://helpx.adobe.com/adobe-media-server/dev/configure-dynamic-streaming-live-streaming.html).
    * Bug #3694203 - In a DVR stream, seeking from within a playing mid-roll into another mid-roll ad cue may lead to browser freeze
    * Bug #3753725 - selectPolicyForSeekIntoAd doesn't take into account if the ad break has been watched
    * Bug #3754529 - Pre-roll ads are not removed from the stream when seeking back in a live DVR stream
    * Bug #3761896 - If seeking is allowed during ad play, ad markers will re-adjust after seek. Workaround is to not use ITEM_UPDATED callback during seek
    * Bug #3779889 - The complete call is not made when reaching the end in trick play in Video Analytics
    * Bug #VA-779 - The bit-rate change event heartbeat is not sent for Enhanced Video Analytics with Heartbeat Support Reference Implementation - Trick play is not implemented in the sample application.

## Helpful resources {#helpful-resources}

* See complete help documentation at [Adobe Primetime Learn & Support](https://helpx.adobe.com/support/primetime.html) page.
