---
title: TVSDK 1.4 for Android Release Notes
description: TVSDK 1.4 for Android Release Notes describe what is new or changed, the resolved and known issues and the device issues in TVSDK Android 1.4.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
exl-id: 1e3ec3b7-25be-4640-870e-928e832fe12d
---
# TVSDK 1.4 for Android Release Notes {#tvsdk-for-android-release-notes}

TVSDK 1.4 for Android Release Notes describe what is new or changed, the resolved and known issues and the device issues in TVSDK Android 1.4.

## New features {#new-features}

**Version 1.4.43**

**Secure Ad Loading over HTTPS**

Adobe Primetime provides an option to request first call to primetime ad server and CRS over HTTPS.

**alwaysUseAudioOutputLatency(boolean val) in MediaPlayer class**

When this parameter is set, use the audio output latency in the audio timestamp calculation.

It accepts a Boolean parameters val. If its value is `True`, the client uses the audio output latency in the audio timestamp calculation.

**Version 1.4.42**

**Partial Ad-Break Insertion:**
TV-like experience of joining in the middle of an ad without firing the tracking for the partially watched ad.
Example: User joins in the middle (at 40 seconds) of a 90-second ad break consisting of three 30-second ads. This is 10 seconds into the second ad in the break.
* The second ad plays for the remaining duration (20 sec) followed by the third ad.
* Ad trackers for the partial ad played (second ad) are not fired. The trackers for only the third ad are fired.

**Version 1.4.41**

No new features.

**Version 1.4.40**

No new features.

>[!NOTE]
>
>You will not require the API changes if you are on a version earlier than 1.4.39.

**Version 1.4.39**

* TVSDK is certified with VHL 2.0.1 and with VHL 2.0.1 with Nielsen.
* Android TVSDK is updated to make CRS requests from new Akamai host `primetime-a.akamaihd.net`.
* New hostname configuration provides CRS asset delivery via both HTTP and HTTPS (SSL) at greater scale.
* TVSDK supports Android Oreo release.
* A new function is added to `AdClientFactory` class to support registering multiple Opportunity Detectors:

  ```
  public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
  ```

  This should return an array of PlacementOpportunityDetector. Now you can register multiple Opportunity Detectors. For example for early ad exit feature, two Opportunity Detectors were required - one for ad insertion and another for early exit from ad. You are required to implement this new function only impact if you have implemented your own AdvertisingFactory (and not using DefaultAdvertisingfactory). For getting the existing behavior - you need to create a single Opportunity Detector, as in createOpportunityDetector() function and put into an array and return:

  ```
  public class MyAdvertisingFactory extends AdvertisingFactory {  
  …  
  @Override  
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {  
  List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();  
  opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));  
  return opportunityDetectors;  
  } }
  ```

>[!NOTE]
>
>You will not require the API changes if you are on a version earlier than 1.4.39.

**Version 1.4.36**

Bug fix for Content Skip on Android.

**Version 1.4.35**

* **Network Ad Information**

  TVSDK APIs now provide additional information on third party VAST responses. Ad ID, Ad System and VAST Ad Extensions are provided in the NetworkAdInfo class accessible through the networkAdInfo property on an Ad Asset. This information can be used for integrating with other Ad Analytics platforms such as **Moat Analytics**.

**Version 1.4.31**

**Multi-CDN Support for CRS Ads**
* By default, all transcoded assets will be hosted on Adobe-owned CDN on Akamai. With the latest release, Adobe Creative Repackaging Service (CRS) provides the ability to upload the transcoded creatives to multiple CDNs as specified by the customer.
* New APIs are added to  TVSDK  to enable specifying the final CRS creative  url  when the default  url  is not used. Please refer to the documentation to learn how to use these new APIs.

**Version 1.4.18**
Primetime Android TVSDK now supports VPAID 2.0 Javascript creatives to enable a rich interactive in-stream ad experience. For more information about VPAID 2.0, see [VPAID ad support](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**Version 1.4.17**

AC-3 5.1 is supported only on Amazon FireTV.

**Version 1.4.11**

* **Ad Fallback, Daisy chaining in ad selection logic (Zendesk #3103** For VAST ads (creatives) with the fallback rule enabled, TVSDK treats an ad with an invalid MIME type as an empty ad and attempts to use fallback ads in its place. You can configure some aspects of fallback behavior.

For more information, see [Ad fallback for VAST and VMAP ads](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **Video Heartbeats Library (VHL) updated to version 1.5**
  * Ability to send metadata with video start and/or video/ad/chapter start as context data
  * Less network traffic - Heartbeats are fewer on average and smaller in size

**Version 1.4.7**

* **On-Premise Individualization Support**Support for on-premise installations of the Adobe Individualization Server to customize the client's individualization request to go to a different endpoint.

**Version 1.4.6**

* **Sample AES encryption (requires Flash Player version 17.0.0.134)**Sample-based AES encryption is now supported.

**Version 1.4.2**

* **Video Heartbeats Library (VHL) update to version 1.4.0.1**

  * Added the ability to bundle different analytics use cases, from other SDKs or players, with the Adobe Analytics Video Essentials.
  * Ad tracking has been optimized by removing the trackAdBreakStart and trackAdBreakComplete methods. The ad break is inferred from the trackAdStart and trackAdComplete method calls.
  * The  playhead  property is no longer needed when tracking ads.

* **Nielsen SDK Integration**The TVSDK now supports sending user tracking information to the Nielsen SDK without any custom integration.

**Version 1.4.0**

* **Blackout Signaling With Alternate Content Replacement** As part of the 1.4 TVSDK update, the TVSDK also now supports going into and returning from regional blackouts against linear content. The TVSDK can now process two manifest files in parallel, main and alternate, to monitor for blackout signals even when alternate programming is being shown in place of the original programming.

* **Remove/Replace C3 Ads** Now, no additional prep work is needed to dynamically insert new ads into video-on-demand (VOD) assets that are coming out of the C3 window. The TVSDK now provides an API to remove custom content ranges and dynamically insert new ads. This powerful new functionality is also useful in cases where live/linear content airs during broadcast and is immediately pulled down for use as on demand content without proper time to “clean” the asset.

* The interface PlaybackEventListener has a new method called onReplaceMediaPlayerItem, which you can use to listen for a new event, `ITEM_REPLACED`. This event is dispatched whenever a MediaPlayeritem instance is replaced on MediaPlayer. The client application implementing this PlaybackEventListener must implement or override this new method.
* AdClientFactory has a new function added to  class  to register for multiple Opportunity Detectors:

  ```
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem item);

  For example for early ad exit feature, you need two Opportunity Detectors - one for ad insertion and another for  early  exit from  `ad`.

  To override this new function create a single Opportunity Detector, and put into an array and return:

  @Override

  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

  List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();

  opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

  return opportunityDetectors;
  }

  }
  ```

## TVSDK changes for 1.4 {#tvsdk-changes}

* The interface PlaybackEventListener has a new method called onReplaceMediaPlayerItem, which you can use to listen for a new event, ITEM_REPLACED. This event is dispatched whenever a MediaPlayeritem instance is replaced on MediaPlayer. The client application implementing this PlaybackEventListener must implement or override this new method.

* AdClientFactory has a new function added to class to register for multiple Opportunity Detectors:

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

For example for early ad exit feature, you need two Opportunity Detectors - one for ad insertion and another for early exit from ad.

To override this new function create a single Opportunity Detector, and put into an array and return:

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## Device certification and support in 1.4 {#device-certification-and-support-in}

>[!NOTE]
>
>The following features are **not** supported in the  TVSDK :
>
>* Slow motion, on any platform or version.
>* Live trick play.

**Version 1.4.43**

TVSDK 1.4.43 has been certified with Android Devices having Android 6.0.1/ 7.0 and 8.1 (Oreo).

* **Version 1.4.23:**

  * TVSDK 1.4.23 has been certified for Android Devices with Android N.

* **Version 1.4.18:**

  * Primetime has been certified for Amazon Fire TV.
  * VPAID 2.0 is supported only on devices with Android 4.0 and above.

## Resolved issues in 1.4 {#resolved-issues-in}

>[!NOTE]
>
>All TVSDK customers who use CRS are strongly encouraged to upgrade to TVSDK 1.4.39 or latest on iOS and Android. This upgrade is a drop-in replacement to the existing app implementation. After the upgrade, check for the CRS creative URL requests in a proxy tool (for example, Charles) to verify that the version in the path reflects version 3.1. For example:
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**Version 1.4.43**

* Ticket #27143 - Unable to play 5.1 audio track on FireTV devices

  * TVSDK now able to play AC3 audio on FireTV devices. Playback is always in stereo.

* Ticket #33902 - Secure Ad Delivery over HTTPS

  * Adobe Primetime provides an option to request first call to primetime ad server and CRS over https.

* Ticket #34493 - Bluetooth audio delay

  * Added `alwaysUseAudioOutputLatency` in MediaPlayer class which when set, Will result in using audio output latency in audio timestamp calculation.

* Ticket #34949 - New version of video heartbeat library (VHL) integrated.

**Version 1.4.42 (1791)**

* Zendesk #33719: FireTV 4k Adaptive Bitrate scales slowly. Added support for ABR for FireTV 4K devices.
* Zendesk #33338:  resetDRM  clears all data of the application.  Handled  extra case where exceptions in  non -TVSDK threads  was  causing TVSDK operation queues to fill up.

**Version 1.4.41 (1776)**

* Zendesk #33002 - Companion asset data from TVSDK on Fire TV. Implemented a new class AdBannerAsset which will return the Companion data as List &lt;AdBannerAsset&gt; and AdAsset::id is now a String instead of long.
* Zendesk #32821 - Android Primetime player freezes when it encounters Presentation Timestamp (PTS) for WWE. This issue is fixed in this release.
* Zendesk #33572 - VideoAnalyticsProvider Ad Start Crash. Using the right combination of VHL+Nielsen joint SDK version of VideoHeartbeat.jar fixed this issue.
* Zendesk #33355 - Fire TV: Scrub back 15 second issue. Not any fix from TVSDK side and customer are verifying this at their End and 3rd party.

**Version 1.4.40 (1764)**

* Zendesk #33068 - Amazon lip sync issue on  new  device. Lip sync issue is fixed in this releases.
* Zendesk #32215 - Android TVSDK 1.4.38 Security Issues `[Hotlist]`. Updated to the latest OpenSSL-1.1.0 and curl-7.55.1.
* Zendesk #32920 - Blank screen within an Ad break and no Ad break completion. Fixed an issue where a VPAID container could get into a hung state and handled an issue where Facebook VPAID ads were often returning multiple CDATA blocks in a single \&lt;AdParameters\&gt; VAST node.

**Version 1.4.39 (1744)**

* Zendesk #28976 - Licensing request takes more than a second. While DRM Licence request calls that use POST  are  executing, Curl adds extra "Expect: 100-continue" header. Removed "Expect:" header in  TVSDK .
* Zendesk #27707 - CSAI environments not honoring CUE IN markers for early return or return to content. Provided support for multiple opportunity generators.

**Version 1.4.38 (1722)**

* Zendesk #21590 - Video Performance and Tracking in Latest Origin Builds

Integration and certify VHL 2.0 in TVSDK to reduce the Barrier in the VideoHeartbeatsLibrary implementation by decreasing the complexity of the APIs.

* Zendesk #29688 - Support for Android O Beta customers.

TVSDK support for the new Android Beta release.

**Version 1.4.36 (1713)**

* Zendesk #27392 - Content Skip on Android

To accommodate decryption, the Android TVSDK was incorrectly widening the byte range of non-iframe content by 16 bytes. The widening is needed for Iframe streams but not for non-iframe streams.

**Version 1.4.34 (1702)**

* Zendesk #27638 - Leak in cURL INet object

The Posix cURL INet object was leaking while holding onto the share manager and DNS cache that was used in the cURL connections.

This issue was resolved by deleting the Posix cURL INet object from the INet deconstructor.

**Version 1.4.33 (1694)**

* **OpenSSL library**

The OpenSSL library has been updated with the OpenSSL version 1.0.2j.

* Zendesk #21701 - Send the original creative URL for 1401 CRS request instead of the normalized URL.
    This issue is resolved by sending the original creative URLs.

* Zendesk #25023 - Long duration video playback: video freeze, screen flickers
    This issue was resolved by setting the maximum video format dimensions for CenturyLink set-top box devices.

* Zendesk #27460 - The new Akamai account is unable to handle a POST cdn request.
    The code was updated to make the `cdn.auditude.com` ad request to be GET instead of POST.

* Zendesk #28245 - Playback state is not notified correctly when the app goes from background to foreground
    This issue was resolved by correctly restoring the playback state to play or pause when the application returns to the foreground.

**Version 1.4.32 (1682)**

* Zendesk #25779 - Security vulnerability found with TVSDK
    Android 4.2 and lower has a security vulnerability when JavaScript is enabled in a WebView. Using WebView by TVSDK has been disabled for devices that are running OS 4.2 or lower. This disables the use of VPAID ads in TVSDK on these devices.

* Zendesk #26890 - Issue in SCREEN state (ON/OFF) handling Ref. Player
    When the Adobe Video Engine (AVE) resumes from a SUSPENDED state, the DefaultMediaPlayer does not update its status. As a result, the DefaultMediaPlayer remains in a SUSPENDED state even though the AVE is in a PLAYING state. This issue has been resolved by setting the DefaultMediaPlayer state to PLAYING when receiving a PLAY status from the AVE, even if the current status of the DefaultMediaPlayer is SUSPENDED.

**Version 1.4.31 (1675)**

* Zendesk #21974 - Exceptions due to null objects
  * AdIndex rarely gets incremented when null. This might be due to incorrect API calls received for pre-roll adBreak. Fixed the data types to avoid such exceptions

* Zendesk #24714 - Turn off extraneous logging
  * Updated the TVSDK to turn off extraneous logging

* Zendesk #24488 - AV Sync issues on Fire TV
  * Fixed by improving the handling the AV decoder threads. Specifically, whenever the input or output frame queues are modified, the decoder thread specific to the frame's content type is run.

* Zendesk #26551 - Fix the CRS failures
  * When the request is HEAD (http head), we don't need to read the content because it's empty. While it's ok to try to read it, old Android (4.0.x) hangs while we call read() and newer Android return correct value (-1) when we call read(). Based on this, changed the code to not to read content for "head"

* Zendesk #26696 Null Pointer Exception when accessing TrickPlayManager
  * Fixed by checking if TrickPlayManager object is not null before using it.

**Version 1.4.30 (1659)**

* Zendesk #22675 Asset duration does not get updated for Live/Linear streams
    This issue was resolved by providing a new API, assetDuration, in PTVideoAnalyticsTrackingMetadata that provides the asset duration for Live and Linear streams.

* Zendesk #25853 Memory leak in TVSDK when switching channels
    The issue where a file-read buffer leak when the MediaPlayer is reset or released while downloading a file has been resolved.

**Version 1.4.29 (1653)**

* Zendesk #21200 - Player doesn't recover from suspended state when app was in the background
    When the player was suspended after stream switch was signaled, the resolution allows the player to perform the stream switch when restoring the player from the suspend state, instead of restoring to previous position.

* Zendesk #23412 - Player is stuck with a black box if you click through any Ads within the last 3s of the ad break
    This issue is the same issue as Zendesk #21200.

* Zendesk #23616 - Skipped ad break seeks too far in the future
    Depending on ad insertion type (insert/replace), TVSDK determines whether the ad duration is used in calculation to determine ad break end point.

* Zendesk #25078 - TVSDK DRM Memory leak on Android TV STB
    The memory leak for the DRM adapter object has been located and fixed.

* Zendesk #25067 - Crash in VideoEngineTimeline
    This is happening because objects were not cleaned correctly, and events were called after the objects were destroyed. The issue was resolved by adding checks to prevent null exceptions.

* Zendesk #25352 - Set custom HTTP header
    This issue was resolved by adding a new custom header to the allow list on TVSDK.

* Zendesk #25617 - Live stream PTS rollover causing player discontinuity and memory crash
    This issue was resolved by adding a PTS rollover handling in FragmentedHTTPStreamer when a rollover occurs in the middle of a segment.

**Version 1.4.28 (1637)**

* Zendesk #23618 - Ad break events fire before the ad policy is consulted
    This issue was resolved by not firing the AD_BREAK_START and AD_START events when the ad is skipped because of adForgiveness. The AD_BREAK_SKIPPED event is sent instead.

**Version 1.4.27 (1631)**

* Zendesk #23174 - Performance issue when resizing the video
    This issue was resolved by proving a new API, MediaPlayerView.setSurfaceFixedSize, which allows TVSDK to access SurfaceHolder.setFixedSize() from MediaPlayerView.

* Zendesk #24450 - TVSDK makes duplicate ad requests
    This issue occurred when the elapsed time was converted to long and not double, and this issue has been fixed.

**Version 1.4.26 (1627)**

* Zendesk #21436 - OpenSSL library update to version 1.0.2h Updated the OpenSSL library to OpenSSL Version 1.0.2h
* Zendesk #23825 - Cookies are not being included in the callbacks Fixed by providing the support for android cookies.

**Version 1.4.25 (1620)**

* Zendesk #22900 - Live Adobe Primetime DRM stream is not playing on the Android reference player
    The memory allocation problem has been fixed.
* Zendesk #23176 - Application crashes when it is trying to play VPAID ads
    The crash occurred because the application does not create a custom ad view to render a VPAID Ad. This issue was resolved by ignoring the VPAID ads in the ad server response when there is no custom ad view.

* Zendesk #23153 - SampleAES DRM Stream - Playback stalling in the TVSDK Reference Player
    This issue is the same as Zendesk #22900.

**Version 1.4.24 (1612)**

* Zendesk #20784 - Analytics: Triggering content completes for live video transitions
    This issue was resolved by adding an API (trackVideoComplete) to manually trigger the completion of content during a live/linear video tracking session.

* Zendesk #21977 VideoEngineTimeline Crash during placeAdBreak/acceptAd operation
    * In this issue, the following libraries were updated:
        * AdobeMobile library to version 4.10.0
        * VHL library to version 1.5.6
        * VHL-Nielsen library to version 1.6.7

This issue was resolved by adding a null check before adding ads to the accepted ad list.

* Zendesk #22313 The bitrate for the STBs with Amilogic chipset is not going beyond 1.2M
    This issue was resolved by preloading the media codec capabilities and disabling the seamless switch for Amilogic chipset devices.

* Zendesk #19520 Sample AES HLS asset not playing in TVSDK players
    This issue was resolved by handling multiple PMT descriptors for Sample AES encrypted HLS streams.

**Version 1.4.23 (1602)**

* Zendesk #18852 - Update creative selection logic based on CRS rules
    This issue was resolved by adding a JSON configuration file to specify the creative selection priority.

* Zendesk #20861 - Android N
    This release provides support for Android N by removing the ability to directly use the Android platform native libraries that are no longer accessible to applications that run on Android N.

* Zendesk #21018 - Android N crash
    Same resolution as ZD# 20861.

* Zendesk #21266 - VideoEngineAdapter crashes on an Invalid_Key error
    The Invalid_Key error does not include a description from AVE, so parsing the text resulted into NPE. The issue was resolved by adding a null check for the description during onError before parsing the description.

* Zendesk #22286 - Native library is going on allocating memory reading key/fragment causing crash
    This crash that occurred on Android when attempting to load a manifest with multiple keys simultaneously has been fixed.

**Version 1.4.22 (1581)**

* Zendesk #17236 - Unreliable play head time for HLS videos with DRM
    The time jump with the LBA streams, where the audio segment start time does not match with the video segment start time, has been fixed.

* Zendesk #17680 - Video playback is freezing on the Selevision Andredo box
    The video decoder on this device sometimes returns a significant output time jump when dequeuing video frame from the output buffer, and this output timestamp remains high. This issue was resolved by returning a *video profile not supported* error that does not force the player to retry the same profile or choose a different profile.

* Zendesk #19074 - Video freeze during FFWD and REW trick play
    This issue was resolved by adding a new warning TRICKPLAY_ENDED_DUE_TO_ERROR to notify the application that trickplay has exited and that the video was paused due to an unrecoverable error.

* Zendesk #19574 - TVSDK is not returning M3U8 response data for DRM or non-DRM content
    This issue was resolved in the following ways:

* Zendesk #19986 - OP behavior broken for certain devices like Android TV
* Adding a FILE_NOT_FOUND error to the condition.
* When the error comes from a *file not found* error, separating the URL and response from the error description if the response is available.
    The logic error that was introduced by NVidia shield OP support has been fixed. On non-NVidia shield devices, trust the display secure flags even when the display type is unknown.

* Zendesk #20549 - Handling of stale playlists. This issue was resolved by reducing the interval between the live manifest update to half of the expected segment duration, if the previous fetch does not receive new segments.

* Zendesk #20742 - Memory usage appears to continue increasing when playing back live content on FireTV.The crash is caused by the JNI object reference table that has reached the limit. This issue was resolved by deleting the reference to the MediaFormat object that was created during the decoder restart.

* Zendesk #21125 - Return from live/linear ad break early (CSAI). Added a feature that allows the player to return to main content during an ad break if the player registers the splice in ad cues by using the splice in opportunity detector.

* Zendesk #21334 - TVSDK ad request timeout value for third-party ad request. A adRequestTimeout setting was added to AdvertisingMetadata that enables a global timeout for the ad call.

**Version 1.4.21 (1566)**

* Zendesk #17781 - ADB screencapture no longer working
    This issue was resolved by adding the DefaultMediaPlayer.create(Context context, boolean secureSurface) API, which allows screen capture.
    To allow screen captures, pass false for secureSurface.
Important: We strongly recommend that you do not enable this screen capture feature in a production setting.

* Zendesk #19074 - Video freeze during FFWD and REW trick play
    The following issues that occurred when the trickPlay could freeze in the playbackhave been resolved:

* Zendesk #19532 - Close Caption is appearing out of order
    * FHS starts trickplay, but the first iframe segment did not have a frame in it. 
    * While downloading an iframe segment, if FHS hits an error condition, it exits from trickplay and pauses the playback. 
    * Andorid MediaCodec implementation waits forever for input queue availability while it was asked to flush all the input / out buffers.
    This issue was resolved by reversing the order of WebVTT cues so that multiple overlapping cues appear to "scroll up".

* Zendesk #19574 - The TVSDK does not return M3U8 response data for DRM or non-DRM content
    In the initial load of the manifest file in PTMediaPlayerItem.prepareToPlay, if the loading fails, the TVSDK does not report the body of the failure response to the application.
    This issue was resolved by allowing the TVSDK to report the failure response as an error to the application.

*  Zendesk #19701 - Playback freezing with SAP/Discontinuity
    The player freeze when the audio and video are unaligned at discontinuity has been resolved.

*  Bug #PTPLAY-11162 - OpenSSL library update to version 1.0.2f has been resolved.

**Version 1.4.20 (1546)**

* Zendesk #17384 - Feature Request: ID3 metadata support for AAC playback
    Support for ID3 tags in AAC media has been provided in the TVSDK for Android starting in version 1.4.20.

* Zendesk #18358 - Player freezes on bitrate switch with out-of-sync discontinuities
    This issue was resolved by handling the ABR stitching edge cases appropriately.

* Zendesk #19232 - App using TVSDK 1.4.18 is behaving strangely on older Amazon OS version 4
    This issue was resolved by removing the hidden web view creation in the TVSDK player initialization process to avoid conflict with devices that do not support Android Webview.

* Zendesk #19585 - Slow-Motion playback when adaptive bitrate transition happens.
    During ABR switch, if the new profile has a different audio sample rate than the current profile, the playback becomes fast or slow motion. This is because the video presenter is not notified that the audio format has changed.
    This issue was resolved by making sure that the notify flag is set in the correct place.

* Zendesk #19683 - SAP DAI playback - No audio for few seconds.
    For several cases in the TVSDK's logic, when the timestamp of two rendition segments were compared, RENDITION_TIMEOUT_THRESHOLD was used as an acceptable range of value, because the timestamp cannot always be matched with a 0 ms difference. If the gap is within the range of RENDITION_TIMEOUT_THRESHOLD, the assumption is that it is a match.

The RENDITION_TIMEOUT_THRESHOLD was set to 100ms, but it found to be insufficient for certain streams. This issue was resolved by increasing the RENDITION_TIMEOUT_THRESHOLD to 200ms.

* Zendesk #19699 - The TVSDK fails to switch between VTT subtitle tracks
    This issue was resolved by making the player dump and reload the manifest when a track changes and by correcting the UTF8 string conversion problem that affected the double-byte WebVTT caption track names.

* Zendesk #19717 - CC options display issue
    This issue was resolved by correctly handling the Unicode string.

* Zendesk #19910 - TIT2 ID3 tags not being detected
    This issue was resolved by providing more complete support for ID3 v2.4 string encodings and to support for ID3 v2.3.

* Zendesk #20135 - The TVSDK is triggering multiple onComplete for VOD content.
    This issue was resolved by adding the post_roll_compelete event listener at the right place, instead of at the complete case of the status change event.

**Version 1.4.19 (1521)**

* Zendesk #4180 - The TVSDK is not enforcing HDCP.
     * This is a partial fix for this ticket and addresses only the issue for NVidia shield devices.
    You must use the correctly implemented HDCP detection API in the Nvidia Shield to dynamically track the HDCP status.

* Zendesk #18358 - The TVSDK freezes on bitrate switch with out of sync discontinuities.
     * This issue was resolved by adding a new warning to detect the PTS discontinuity and by forcing the PTS check to redo searching for the correct segment for every ABR switch.
    To fix the freeze, the call to the mediaPlayer.setCustomConfiguration method should include forcePTSCheckForABR as an argument.

* Zendesk #19038 - No live stream on Asus Zenpad 10.

    This issue was resolved by preloading the media codec information, so that you do not query the function at run time.

* The following issues are the same as Zendesk #19038:
    * Zendesk #19483 - The TVSDK is crashing on Intel platform. 
    * Zendesk #19171 - Crashes on Asus Memo Pad 7 with Android 5.0.

**Version 1.4.18 (1503)**

* Zendesk #3324 - Primetime ads reporting does not track ad breaks when there is no ad media in a VMAP.
    When an ad break is empty, the ad break start and complete tracking events were not being pinged. This issue was resolved by sending ad break start pings on empty ad breaks, such as VMAP AdBreak, with a valid AdSource nod.

* Zendesk #18229 - SetCCVisiblity(VISIBLE) is ignored after MediaPlayer.reset() call
    This issue was resolved by adding setCCVisibility(Visibility.INVISIBLE); to the reset() function in the MediaPlayer class.

* Zendesk #18328 - Dropped frame issue on Amazon Fire TV 2nd gen devices for the contents with 60FPS
    This issue was resolved by applying the encoded FPS for the sleep time decision making and with a better encoded FPS prediction logic.

**Version 1.4.17 (1472)**

* Zendesk #2231 - Error returned from fetching the manifest unavailable in MediaPlayerNotification
    This issue was resolved by including the response body of the manifest when there is a parse error.

* Zendesk #17703 - VideoEngineView does not prevent screenshots during video playback
    The setSecure method has been available since API 17, but because API 17 covers 4.2, 4.2.1 and 4.2.2, it is not known which one will throw an exception or whether it's device specific. This issue was resolved by wrapping VideoEngineView.setSecure into the try catch clause.

* Zendesk #17919 - Content seek causes heartbeat error
    An Invalid input data Position error was occurring as a result of the heartbeat call that was generated when seeking was started after the pre-roll. This issue has been resolved.

**1.4.16a** (1454a)

* Zendesk #18215 - Some AES streams are unable to load.
    This issue was resolved by checking the profile DRM metadata size before loading the AES key.

**Version 1.4.16 (1454)**

* Zendesk #3875 - Tab S Crashes during playback
    Reverting the dependency of OKHTTP on Auditude for CRS because TVSDK is now directly using httpurlconnection instead of curl. The issue was resolved by clearing exceptions before making any other JNI call.

* Zendesk #4487 - Tracking Linear Channel of Content
    The issue was resolved by allowing the re-initializing of the video heartbeat tracker during a linear stream playback session.

* Zendesk #17919 - Android - content seek causes heartbeat error
    The issue when the heartbeat is in an error state when there is a seek in a chapter has been resolved.

* Zendesk #18053 - Adobe Primetime crashes on Marshmallow
    The TVSDK was crashing on Android M OS when the TVSDK library used neon code that does the YUV -&gt; RGB color conversion. The issue was resolved by updating the functions that are causing this issue by using the non-neon version of code.

* Zendesk #18072 - Android M - Application Crash
    When checking whether the profile and level are supported, a crash occurs when calling MediaCodecList and MediaCodecInfo APIs. The issue was resolved by providing a temporary work around by loading all the codec info ahead of time to avoid calling these APIs only when codec information is needed.

* Zendesk #18074 - Arabic subtitles not working on Nexus with Android 6.0
    The issue was resolved by providing CTS font map support for Android.

**Version 1.4.15 update (1438)**

* Zendesk #17437 - Long delay in VOD content startup with some AES streams.
    To resolve this issue, if multiple keys listed in manifest, download all AES keys in parallel.

**Version 1.4.15 (1435)**

* Zendesk #4278 - Glitches on Android set top boxes when Adaptive bitrate changes (ABR).
    The fix was to add support for seamless ABR switch with latest Android media codec.

* Zendesk #17063 - Calling mediaPlayer.reset() causes a video engine reset error.
    The fix was to include the original MediaErrorCode from VideoEngineExceptions when dispatching ErrorEvents.

* Zendesk #17130 - A brief but noticeable pause when changing bit rate seen on FireTV.
    (Same as #4278 above) The fix was to add support for seamless ABR switch with latest Android media codec.

* Zendesk #17666 - Additional Ad Markers, Unexpected or No Ads when resuming content.
    The fix was an issue when doing prepareToPlay on video-on-demand (VOD) content, the initial seek performs on the local time instead of virtual time.

* Zendesk #17437 - Long delay in VOD content startup with some AES streams.
    The fix was to download all AES keys in parallel when multiple keys are listed in the manifest.

* Zendesk #17851 - Android TV - Black Frame during ABR
    The fix was to specify KEY_MAX_WIDTH and KEY_MAX_HEIGHT to enable adaptive playback.

**Version 1.4.14 (1415)**

* Zendesk #3875 - Tab S Crashes during playback.
    An additional fix was required to prevent the crash.

* Zendesk #17245 - Fallback on Android TV is not functioning.
    Fixed an additional issue where playback hangs when fallback is enabled, and the VMAP response has an empty ad break.

**Version 1.4.14 (1412)**

* Zendesk #17245 - Fallback on Android TV isn't functioning.
    Removed a restriction for disabling creative repackaging on fallback ads.

**Version 1.4.13 (1388)**

* Zendesk #3502 - HLS client based failover support during an ad break
    Allow failover to the main manifest when updating live profile error occurs during ad break period.

* Zendesk #3875 - Tab S Crashes during playback
    To resolve the conflict between HttpUrlConnection and cURLm, use a third-party library.

* Zendesk #4450 - issue setting custom meta data for a single placement in a content resolver
    Add a setter to the Opportunity settings.

**Version 1.4.12 (1388)**

* Zendesk #2751 - CSAI and CRS | Enhance: Handle dynamic elements in certain media file URLs.
    Updated Creative Repackaging Service to properly handle ads with dynamic creative URLs.

* Zendesk #3965 - Switching back to normal playback from trickplay results in a jump forward a bit before starting playback.
    * Fix includes TVSDK returning the time before the rate change until all the variables are updated, instead of trying to calculate the GetStreamTime. 
    * Fixed crash when changing trick play speed near the end of the stream. 
    * Corrected current time calculation during trick play.

* Zendesk #3978 - Trickplay at 8x and 16x frequently freezes.
    * Always pick the trick play profile with the lowest bit rate to avoid constant buffering. 
    * Increase skip frame interval for high trick-play rate. 
    * Fix an issue that buffer continues to grow after reaching its target length during trick play.

* Zendesk #3992 - Additional Trickplay speeds.
    TrickPlay has been updated to accept rates higher than 16x; +/- 32, +/-64 and +/-128 are now also allowed.

*  Zendesk #4007 - Interpreting the GEOB object as part of the timeline metadata (Android & Web).
    Added setByteArray and getByteArray API.

* PTPLAY-7301 - Instant On start at Random Access Point.
    Instant On has been updated to allow for a non zero starting point.

**Version 1.4.11 (1363)**

* Zendesk #2076 - Frequent stutter when playing video on Motorola Xoom with Android 4.0.3
    Added devices to allow list to prevent them from trying to play high profile content.

* Zendesk #2197 - `[Ads]` Tracking ad errors
    dispatch OperationFailedEvent with warning notification.

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` macro not being populated
    * error code 400 will be exposed if inline ad has bad creative.
    * `[ERRORCODE]` macro will be URL encoded

**Version 1.4.10 (1354)**

* Zendesk #2941 - Live assets don't have "0" in seekable range
    Previously there was a 3 segment buffer when seeking to the beginning of a Live stream, now it is possible to seek to the very beginning of a live stream (i.e. the start of the first segment).

* Zendesk #3169 - Update reference player with Adobe Analytics integrationThe reference player has been updated with the Adobe Analytics library as an example implantation. 
* Zendesk #3299 - Unexplainable trick play behaviour
    * Fixed a bug where returning to play state after stopping trick play could take several seconds (sometimes 25+ seconds). 
    * Fixed a bug where invoking trick play a second time on the same media, can cause the stream to freeze at the current time.
* Zendesk #3433 - Android and Flash - Problems with subtitles

GetLine for WebVTT was not respecting a &lt;CR&gt;&lt;LF&gt; adjusted length for a packet; the last caption could contain characters from previous captions.

* PTPLAY-6243 - Enhance reference player to capture debug information

The Android sample reference players has been enhanced with an option to turn on debug logs and email the results. This option is found under the Log menu in the reference player.

**Version 1.4.9 (1332)**

* Zendesk #2649 - Buffer Complete occurs before initial buffer is full

After a seek, possible case where video engine sets state to PLAYING before video presenter is ready to play. Occurs when buffer state is high before seek. Fix by notifying video engine of low buffer state. With video engine low buffer state, calling Play causes state change to BUFFERING instead of PLAYING. Playback resumes when state changes to PLAYING.

* Zendesk #2846 - Enhancement request: Provide ability to set different user-agent string for calls made by Auditude library

A new API has been added to set the user agent for ad related calls, auditudeSettings.setUserAgent(“user/agent”). If no user agent is set, the default will be used. This only affects the user agent for ad related calls, the user agent for media calls is unchanged which is "Adobe Primetime"+&lt;default useragent&gt;.

**Version 1.4.8 (1324)**

* Zendesk #1218 - 106000.33 Error with local ... If loading manifest in FragmentedHTTPStreamer::ThreadParseManifest() fails, check if URL domain is localhost and if so, change domain to 127.0.0.1 and recall ThreadParseManifest. 
* Zendesk #3072 - Automatic switching to lower bitrates. Changed buffer length calculation to skip zero PTS payload. 
* Zendesk #3168 - WebVTT subtitles only displayed for first 10 secs. 
* Zendesk #3193 - Request for a Profile change API in TVSDK, PlaybackEventListener.onProfileChanged() has been added. 

**Version 1.4.7 (1311)**

* Zendesk #2197 - Tracking ad errors. Added notification for asset failed to load manifest 
* Zendesk #2575 - PSDK ignores MARK custom in-stream ad before video 
* Zendesk #2719 - Win Death with auditude ads, fixed beacon tracking when redirected to relative url in auditude plugin 
* Zendesk #2760 - DISCONTINUITY tag ignored during TrickPlay mode 
* Zendesk #2805 - Player Crash at Beginning of Playback, same fix as Zendesk #2719 
* Zendesk #2817 - Android player - The player sometimes hangs and stops playing, fixed by extending the decode buffers from 2.0 to 3.0 seconds 
* Zendesk #2839 - Does Adobe Primetime PSDK support ARMv8 chipsets?, added fix for crash found on Galaxy S6. 
* Zendesk #2885 - Auditude Crashing playback, same fix as Zendesk #2719 
* Zendesk #2895 - Live HLS failure consistently after 10 minutes of playback 
* Zendesk #2925 - Feedback regarding Android dev build (1.4.5), on certain devices when we queue the packet to the input queue, if the PTS is negative, the decoder goes into a weird state that we always get a negative output PTS for future packets. The fix will set the input PTS to zero if it is negative to avoid this problem. 
* PTPLAY-4645 - Turn off RC4 cipher support in openssl. There are known exploits for RC4. This means that if an attempt is made to connect with a server that only supports RC4, it will fail.

**Version 1.4.6 (1282)**

*  Zendesk #2192 - Bitrate doesn't always lower in poor network conditions, fixed by removing fast switch implementation. 
* Zendesk #2631 - Arabic subtitles on Android: Text on multiple lines appears cut-off, fixed by adjusting font size for Arabic fonts. 
* Zendesk #2844 - Buffering on Note 4 and Fragment download time isn't accurate.

This issue was fixed by adding latency between video segment downloads into bandwidth calculation and having the download time calculation logic use full request cycle time.

* Zendesk #2908 - Arabic subtitles not working on Nexust 5, 6 and 7, fixed by adding 2 more fallback fonts for Arabic scripts. 
* PTPLAY-4627 - update Nielson appsdk to version 1.2.3.7 
* PTPLAY-5084 - Live Master Manifest update failover support

**Version 1.4.5 (1248)**

* Zendesk #1757 - Only audio played or Player crashes for some video bit rate profile, Nexus 4 and Nexus 7 crash fixed 
* Zendesk #2072 - TimedMetadata for AdEvent does not contain full URL just "http" 
* Zendesk #2192 - Bitrate doesn't always lower in poor network conditions 
* Zendesk #2256 - Access to Master Playlist, updated PSDK to dispatch timedMetadata events for subscribed tags on the master playlist. 
* Zendesk #2269 - Two different subtitle languages appear on the screen at the same time with WebVTT 
* Zendesk #2417 - Player trying to download subtitles before playback start, WebVTT was using the wrong segment number variable for segment number matching. Bug would only show up for media that had segment indices starting at zero. 
* Zendesk #2470 - PSDK not returning from SUSPENDED state when bitrate change occurs after suspension. In a special situation when smart seek is called by RestoreGPUResource (restore player from suspend state) and stream switch detected before that, smart seek is unable to complete and result into constant buffering. 
* Zendesk #2451 - Closed captioning 'bottom inset', added 'bottomInset' parameter to caption code 
* Zendesk #2480 - disabling HTTP 302 redirect optimization, Added support for setting useRedirectedUrl property 
* Zendesk #2486 - 3rd party beacons 
* Zendesk #2547 - Arabic subtitles: Text should be aligned right-justified

**Version 1.4.4 (1195)**

* Zendesk #1158 - Playback fails on Huawei Valiant (Y301A1) 
* Zendesk #1709 - Incorrect media size and stretched video 
* Zendesk #1757 - Only audio played after profile switch between streams with identical spa/pps data 
* Zendesk #2095 - HTTP 307 status (redirection) causes Adobe player to stop the playback 
* Zendesk #2126 - Missing TimedMetaData event for last ADEVENT, Subscribed tags which exist after the last segment were not reported to PSDK from AVE 
* Zendesk #2227 - Lockups in VideoEngine nativeReset and nativePause 
* Bug #3921755 - OpenSSL library update to version 1.0.1L

**Version 1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR 
* Zendesk #1870 - Closed Caption Turning On & Off 
* PTPLAY-1818 - Rewind trick play stops at the ad instead of rewinding past it 
* PTPLAY-2736 - A previously displayed WebVTT caption is shown on the screen when a stream with WebVTT caption completes playing 
* PTPLAY-3773 - A mid-roll ad is not played when stream playback is started after the ad position

**Version 1.4.2**

* Zendesk #1561 - HLS client based failover support in primetime. Will use program date time to address failover 
* Zendesk #1590 - LoadInfo.MediaDuration is always 0 (not fixed for audio-only) 
* Zendesk #1626 - Potential Memory Leak in Player. Not actual Memory leak, issue was with NotificationHistory saving last 1000 notifications, this has been reduced to 100. 
* Zendesk #2192 - Bitrate doesn't always lower in poor network conditions

**Version 1.4.1 (1121)**

* Zendesk #1951 - Lockup in VideoEngine.nativeReset() on 4.0.x devices 
* Zendesk #2064 - Native Crash SIGSEGV on specific intel based Android devices 
* Zendesk #2075 - Lockup in VideoEngine.nativeReleaseGPUResource on 4.0.x devices
Note: This build is &#42;&#42;&#42;required&#42;&#42;&#42; for support of Android 5.0 (Lollipop)
* Zendesk #1513 - Android Lollipop support 
* Zendesk #1709 - Incorrect media size and stretched video 
* Zendesk #1871 - WebVTT captions occasionally disappear then reappear when viewing a livestream with WebVTT captions 
* Zendesk #1996 - No timeline markers are seen in PSDK 1.4.0 
* Zendesk #2046 - Crash with PSDK 1.4.1.1113, fixed crash for live streams when no ads are returned from auditude 
* Bug #3769657 - Update the version of curl to 7.38.0 
* PTPLAY-1575 - When ABR playback starts with audio only stream then switches to audio/video stream, the video never renders while the audio continues 
* PTPLAY-2499 - Update to OpenSSL to version 1.0.1j to address recent vulnerabilities 
* PTPLAY-2632 - Video does not recover after mid roll Ad complete on Android Lollipop 
* PTPLAY-2678 - Video stalls during live longevity tests on Android Lollipop

**Version 1.4.0**

* Zendesk #1024 - Feature to remove ad from stream via manifest 
* Zendesk #1293 - Closed Caption Track Selection Issue. 
* Zendesk #1590 - LoadInfo.MediaDuration is always 0, mediaDuration is now showing the correct value. 
* Zendesk #1629 - player/app crashes at end of ad playback on Galaxy S4 
* Zendesk #1674 - ClosedCaption Not showing up, correct 708 caption display when 0x03 ETX codes are missing. 
* PTPLAY-2157 - Default Closed Captioning styles were returned by getters even if after a different styles has been set and verified visually on the stream. The Closed Caption style properties will now show the value they have been set to.

## Known issues in 1.4 {#known-issues-in}

**Version 1.4.31**

* PTPLAY-16803 - Closed Caption will not work with audio only content as the caption system needs video in order to work. Without video, there is no viewport dimension, and without a viewport dimension, we are unable to display any graphics for captions.
* PTPLAY-1634 - Same Subscribed tag has different timestamps in different live windows. When live window moves, the same tag in them should have same timestamps. However, sometimes, even same tags have different timestamps.
* PTPLAY-3197 - Crash with signal 11 SIGSEGV error on Acer Iconia device after ~ 1 hour of continuous playback
* PTPLAY-3310 - With some lower bitrate audio, the audio becomes choppy/stuttery on Acer Iconia
* PTPLAY-3355 - WIN DEATH crash on Motorola Xoom with 4.0.x after ~ 1 hour of continuous playback.
* PTPLAY-3557 - Rewinding at an ad break is causing the stream to complete
* PTPLAY-7079 - Playback Window on android client does not work with Secure Stop/Hard Stop
* Bug #3760144 - Resolution may shift or appear to pulse when stream is paused on some devices such as Kindle Fire 7 and Samsung Galaxy Nexus. Only observable under close inspection
* Bug #3761170 - seekToLocal in Live with Ads cannot seek back into ad content, its best to use the currentTime APIs for Live streams
* Bug #3763370 - Live streams with ads will occasionally show two ad markers close together when there should only be one. These ad markers represent the same ad, and only one will play
* Bug #3763373 - The ad marker may briefly disappear when seeking past an ad in VOD streams. The ad marker restores and there is no other adverse effect on the timeline
* Some devices have known playback issues. See [Known device issues in 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Reference Implementation - Trick play is not implemented in the sample application
* On some Android TV devices a black frame can be seen due to a decoder reset at the following transition points:
   * into and out of trickplay mode
   * switching between late binding audio tracks
   * from an ad to main content.

**Version 1.4.23**

* Closed Caption will not work with audio-only content because the caption system needs video to work. Without video, there is no viewport dimension, and without a viewport dimension, you cannot display any graphics for captions.
* Starting in version 1.4.23, the TVSDK will not support Gingerbread OS 2.3. This is because the TVSDK used the following private Android libraries to gather hardware information about devices with Gingerbread OS:

  * `libstagefright.so`
  * `libcutils.so`

In the Android N release, Google has removed access to these private libraries. The Gingerbread OS currently accounts for less than 1% of Android OS market share globally, so after version 1.4.23, the Gingerbread OS will no longer be supported by the TVSDK.
When you use version 1.4.23 (which includes support for Android N) or later:
* Update your apps to use the minSdkVersion version 11.
* If your end user is running OS 2.3, then the SDK version is lower than the application's minSdkVersion. The system aborts the application's installation or upgrade.
* If your end user is running a version that is higher than OS 2.3, the application will be installed correctly.

If you update the minSdkVersion:

* If your end user is running OS 2.3, the application is installed but playback will not work.
This applies to both update and fresh install.
* If your end user is running a system higher than OS 2.3, the app is installed correctly and the content plays correctly.

**Version 1.4.22**

* The early exit from ads does not work with some of the mid-roll ads when splice-out and splice-in tag are too close to each other.

**Version 1.4.2**

* Rewinding at an ad break is causing the stream to complete.

The Media Player incorrectly sends out MediaPlayer PlayerState.Complete during the Trick Play rewind operation when it reaches an ad boundary. The player should ignore this event when in trick play mode, otherwise the SDK handles the state correctly.

**Version 1.4.0 (1086)**

* PTPLAY-1634 - The same Subscribed tag has different timestamps in different live windows. When live windows move, the same tag in each of them should have the same timestamps. However, sometimes, even the same tags have different timestamps.
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE is sometimes seen after several switches to/from the alternate stream in blackouts
* Bug #3726865 - If a MultiBitrate LBA stream starts from an audio only stream, video will not be displayed if switched to an Audio/Video stream. Starting from an Audio/Video stream will not display this issue, and can successfully switch between Audio and Audio/Video streams
* Bug #3760144 - Resolution may shift or appear to pulse when a stream is paused on some devices such as Kindle Fire 7 and Samsung Galaxy Nexus. Only observable under close inspection
* Bug #3761170 - seekToLocal in Live with Ads cannot seek back into ad content; it is best to use the currentTime APIs for Live streams
* Bug #3763370 - Live streams with ads will occasionally show two ad markers close together when there should only be one. These ad markers represent the same ad, and only one will play
* Bug #3763373 - The ad marker may briefly disappear when seeking past an ad in VOD streams. The ad marker restores and there is no other adverse effect on the timeline
* Some devices have known playback issues. For more information, see [Known device issues in 1.4](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* Reference Implementation - Trick play is not implemented in the sample application.

## Known device issues in 1.4 {#known-device-issues-in}

|Device|Chipset|Issue|Cause|Workaround|
|--- |--- |--- |--- |--- |
|Droid X|TI OMAP3|ABR Delay is expected since it's restarting the decoder.|||
|HTC Desire (different from HTC Desire HD)|QSD8250|Can't play video. Returns VIDEO_PROFILE_NOT_SUPPORTED error.|Desire does not provide a proper HW decoder. It gives Stagefright's SW decoder.|Restart device.|
|HTC EVO 4G|QSD8650|No HW decoder.|Qualcomm does not have a HW decoder.|Upgrade to Android 4.x.|
|Kindle FireSystem version 6.0|TI OMAP4|Does not play HLS streams. Video on AIR does not work.||Upgrade to system version 6.3.|
|Kindle Fire HD|TI OMAP4|Can get into a state where it cannot play video. Returns VIDEO_PROFILE_NOT_SUPPORTED and UNRECOVERABLE_ERROR errors.|The HW decoder gets into an unrecoverable state when the app doesn't shut down the HW decoder fully, e.g., after encountering a crash. Happens on native apps on the device as well.|Restart the device.|
|Kindle Fire HD 8.9|Snapdragon 800|AVE crashes after multiple ABR switches.|||
|Motorola Atrix|Tegra2|Overall performance issues with AVE as opposed to AIR. Audio/video out of synch, video playback freezes after playing between 9 and 15 minutes. Crashes.|Possibly related to openGLES that we enable on AIR. Being investigated.||
|Nexus 7 (2nd gen)|S4Pro APQ8064 (Qualcomm)|Device hangs when a movie is paused for more than 30 minutes.|Device issue that has been reported to Google.|App should timeout so as not to allow a long pause state.|
|Nexus S (GB)|Humming Bird|Cannot play any video using HW decoder.|There is no Stagefright-based HW decoder in Nexus S, so for Android 2.3 we are using a SW decoder.|Upgrade to ICS.|
|Nexus S (ICS)|Humming Bird|Video occasionally flickers.|Bad data can cause the decoder to get into a bad state.|Restart the device.|
|Nook tabletAndroid OS: 2.3|TI OMAP 4|Video doesn't play and app hangs.|Stagefright enters an unstable state after running the app for a few times. Calls to mediaplayer::QueryCodecs hang.|Restart the device to reset the state.|
|Samsung Galaxy ACE|Qualcomm MSM7227|Can't install SampleMediaPlayer app.|Uses ARM v6 instead of the more common ARM v7 chipset. FP/AIR does not support this device.||
|Samsung Galaxy ACE2Android OS: 2.3.6|NovaThor U8500|Can't play video.|This chipset is an unknown decoder for Android pre-ICS in AVE.||
|Samsung Galaxy S2 (GT-I9100)|Exynos|Video performance is not up to par for this device.|The HW decoder is returning decoded frames with the wrong PTS. Looks like the decoder is using decoding time instead of presentation time.||
|Samsung Galaxy S2 GAndroid OS: 2.3.6|TI OMAP4|Crashes when starting video.||Upgrade to Android 2.3.7 or 4.x.|
|Samsung Galaxy S3 (I747)|Qualcomm MSM8960|Intermittently, video freezes and only audio plays, then becomes unresponsive.|||
|Samsung Galaxy S3 I747M|SAMSUNG_M2ATT|Video freezes.|Investigating.||
|Samsung Galaxy Tab 1 v10.1|Tegra 2|MBR transition might take up to three seconds.|As a fix for MBR crashes, we restart the decoder for every stream switch, which can take up to three seconds.||
|Samsung Galaxy Y||Can't install SampleMediaPlayer app.|Uses ARM v6 instead of the more common ARM v7 chipset. FP/AIR does not support this device.||
|Xoom|Tegra|A few frames are dropped for switching. The decoder is not restarted.|OMXAL limitation.||

## Helpful resources {#helpful-resources}

* See complete help documentation at [Adobe Primetime Learn & Support](https://helpx.adobe.com/support/primetime.html) page.
