---
title: TVSDK 2.1 PlayStation 4 Release Notes
description: TVSDK 2.1 for PlayStation 4 Release Notes describe the supported features and the known issues in TVSDK 2.1 PlayStation 4 .
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 32af3fe4-c730-41f6-a558-987bd14c9bae
---
# TVSDK 2.1 PlayStation 4 Release Notes {#tvsdk-playstation-release-notes}

TVSDK 2.1 for PlayStation 4 Release Notes describe the supported features and the known issues in TVSDK 2.1 PlayStation 4 .

## Resolved issues {#resolved-issues}

Here are the resolved issues for TVSDK 2.1 for PlayStation 4:

**Version 2.1.0.638**

* **PTPLAY-10439:**
  When the VMAP wrapper ad link was broken the player was getting stuck in Preparing state (it was not sending `onComplete` to its caller).

* **PTPLAY-10179:**
  `creativeRepackaging` and `fallbackOnInvalidCreative` values are now off by default. Also, when the `creativeRepackaging` flag was set but no `creativeRepackaging` format was provided, the `onRepackagingComplete` was getting called as many times as there were ads in the ad break, causing ad breaks to be created multiple times. 

* **Zendesk #10304**:
  The ad forveness on/off variable was not initialized. We now initialize the variable from `DataSetEntry's` ctor. 

* **PTPLAY-10318:**
  Support for background mode has been introduced. 
* **Zendesk # 17409:**
  When going into trick play mode, then back to normal playback mode, then again into trick play mode, the playback position was jumping. 
* **PTPLAY-9552:**
  After parsing response XML files, error code 1108 is now pinged whenever there are no ads present. 
* **PTPLAY-9551:**
  When there is no ad break after Auditude processing, the CRS calls **onPrefetchComplete** which decrements the groupCount. Since there's no ad break, the **groupCount** is 0 and decremented by 1. Previously the **groupCount** was **uint32_t** because of which it used to change to max value. This is now **int32_t**.

**Version 2.1.0.621**

* **Zendesk #4555**
  Instant on Memory issues leading-Loading errors - `MediaItemLoader` Fix for crash happening while releasing `mediaitemloader` 

* **Zendesk #17223**
  2.x CSAI: Not all ad tracking URLs fire
  * Some VAST ads which in turn pointed to an inline ad were missing tracking urls. 
  * When there are multiple impression tags in an ad in VAST XML, only the first impression url was saved and rest were ignored. Now all the impression urls will be saved and pinged later.
* **Zendesk #17224**
  PS4 User agent move primetime information to the end of UAString 
* **Zendesk #17226**
  2.x CSAI: Not all ads stitched in.   
  Fix is to indicate that timeline has changed due to insertBy or eraseBy operations, and do period switch accordingly. 

* **Zendesk #17284**
  [All platforms] Closed captions do not show up.   
  HLS - support for the `EXT-X-MEDIA-TIME` tag for VTT caption files. 

* **Zendesk #17889**
  Playback "Milky" on PS4   
  applied correct yoffset (for color conversion) 

* **Zendesk #17954**
  Ad fallback logic + handling empty vast   
  Fixed the issue if one of the Vast wrappers were empty, the Vast parser used to keep on processing the wrapper. 

* **Zendesk #17807**
  Cannot get past empty vast
  Same as Zendesk #3103 

* **Zendesk #17865**
  Fallback Logic on PS4 and XBox One   
  Same as Zendesk #3103

**Version 2.1.0.591**

* **Zendesk #3767**
  PS4 Ad code snippet, Ad resolving fails when processing VMAP redirects.
* **Zendesk #4096**
  PS4 CSAI: Segmentation fault
  Fixed crash when TVSDK throws segmentation fault when ad library is processing a VMAP response. 

* **Zendesk #4161**
  Trickplay 16x at the end of the movie freezes
  Fixed deadlock happening when trickplay returns to normal playback

* **Zendesk #4208**
  Random Crash when Closed captions are turned on
  Fixed memory leak when closed captions were enabled

* **Zendesk #4213**
  PS4 CSAI: Change default user-agent string for all ad-related calls
  User-agent string is created using the same UA string that browser is using + add Primetime string 

* **PTPLAY-7675** (internal)
  Transcoded ads are not playing
  Creative Repackaging was failing when it called within a VMAP or VAST response. Fix is to just read the mediafile from ad instead of reading from asset in case of vast ads. 

* **PTPLAY-7895** (internal)
  When `allowMultipleAds=false`, no ads play
  Fixed bug where `allowMultipleAds` parameter was not being followed correctly.

* **PTPLAY-7896** (internal)
  Ads are playing out of sequence order on PS4
  Fixed issue where ads were not in the order in which the ads appeared in the XML responses.

* PS4 TVSDK retested within a mini-app instead of game.

**Version 2.1.0.563**

* **Zendesk #3868**
  Does TVSDK support Playstation SDK 2.5
  The TVSDK is now built with the 2.5 Playstation SDK.

* **Zendesk #4093**
  targetingInfo key-value pairs in Pt Ads request.  
  A newline character separating the key/value pairs was added.

## Supported features {#supported-features}

The following features are supported in TVSDK 2.1 for PlayStation 4:

**Version 2.1.0.621**

* Ad Fallback, Daisy chaining in ad selection logic (Zendesk #3103)
  For VAST ads (creatives) with the fallback rule enabled, the TVSDK treats an ad with an invalid MIME type as an empty ad and attempts to use fallback ads in its place.You can configure some aspects of fallback behavior

**Version 2.1.0.538**

* HLS VOD playback, including play, pause, seek
* Adaptive bitrate streaming
* Encrypted content playback with Primetime DRM and vanilla AES-protected content
* Client side ad Insertion with default ad behaviors and ad forgiveness
* Creative repackaging
* WebVTT closed captions
* Instant on with custom start position
* Trick play with fast forward and fast rewind
* 302 redirect

## Helpful resources {#helpful-resources}

* See complete help documentation at [Adobe Primetime Learn & Support](https://experienceleague.adobe.com/docs/primetime.html) page.
