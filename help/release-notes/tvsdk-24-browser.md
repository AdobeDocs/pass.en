---
title: Browser TVSDK 2.4 Release Notes
description: Browser TVSDK 2.4 Release Notes describe the new,  supported and unsupported features and the known issues in Browser TVSDK 2.4.
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 83fdf530-5cbb-41d9-ab2a-28e117f04488
---
# Browser TVSDK 2.4 Release Notes {#browser-tvsdk-release-notes}

Browser TVSDK 2.4 Release Notes describe the new,  supported and unsupported features and the known issues in Browser TVSDK 2.4.

## Introduction {#introduction}

Browser TVSDK is a toolkit that allows you to add advanced video playback functionality, content protection, and advertising to your browser-based video player applications.

Browser TVSDK 2.4 provides JavaScript APIs to build browser-based video applications and includes playback support in the following modes:

* HTML5 only
* HTML5 with auto flash fallback
* Flash always

This release includes the following information:

• [Browser TVSDK API documentation](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

• [Browser TVSDK programming guide](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_browser-tvsdk.pdf).

• [TVSDK for 1.4 DHLS to Browser TVSDK 2.4 Migration Guide](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

• [Converting from Browser TVSDK 2.4.6 to version 2.4.7](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-246-to-247-for-javascript.html).

• A reference implementation, which is included in the build.

>[!NOTE]
>
>*For a complete list of the security considerations for this release, see Security considerations.

## What's new and supported features {#what-s-new-and-supported-features}

This release of Browser TVSDK provides new features that you can use to enhance your video applications.

**New in 2.4.12 Update (Build 204)**

The following addition is available as part of Browser TVSDK 2.4.12 Update (Build 204):

* Implementation of volume API of AdobePSDK.MediaPlayer is changed to allow autoplay on iOS when playback is muted.

• A new API, `auditudeSettings.ignoreVPAIDAds`, is added to allow ignoring VPAID ads received from the Auditude server. The API does not work for Flash Fallback.

**Version 2.4.11**

The following enhancements and additions are available as part of Browser TVSDK 2.4.11 release:

• HLS Live segment failover is supported for MSE and Flash fallback modes.

• Support for `AuditudeSettings.creativeRepackagingDomain` API is now available for MSE as well. It was previously supported only with Flash fallback mode.

• The release contains fixes for critical customer issues. See *Issues fixed* a list.

**Version 2.4.10**

The following enhancements and additions are available as part of Browser TVSDK 2.4.10 release:

• TVSDK provides enableLogging() to enable or disable the logging. Refer to the [API documentation](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)for usage.

• TVSDK does not anymore support Default Chapters, when using Adobe Analytics. Define and manage Chapters using your application.

• The release contains fixes for critical customer issues. See *Issues fixed *a list.

**Version 2.4.9**

The following enhancements and additions are available as part of Browser TVSDK 2.4.9 release:

• HLS VOD and Live streams with time discontinuity but without discontinuity markers are supported.

• ID3 v2.4.0 frames are supported with Safari video tag for HLS VOD and Live streams.

• Secure Ad loading implementation ensures that ad server calls are upgraded to secure HTTP based on API configuration. For the details, see AdobePSDK.AdvertisingMetadata and AdobePSDK.ForceHttpsAdConfiguration classes. This feature is not supported in Flash fallback mode.

• Ad ID information and Extension information associated with VAST 3.0 responses are now made available to the application by TVSDK and can be used to implement Moat integration for Ad measurements. For the details, see AdobePSDK.NetworkAdInfo API. This is not supported in Flash fallback mode.

• AdobePSDK.ForceHttpsConfiguration class is not available anymore. It is succeeded by

AdobePSDK.ForceHttpsAdConfiguration class.

• A new API, AdobePSDK.optimizeFlashCalls, is now available to optimize the calls to improve HLS playback experience in Flash fallback mode. This is disabled by default.

**New in 2.4.8 Update (Build 6002)**

This update contains fixes for critical customer issues. See *Fixed Issues*, for the list.

**Version 2.4.8**

The following enhancements and additions are available as part of Browser TVSDK 2.4.8 release:

• The SDK is now compliant with the Chrome EME and the best practices changes available starting Chrome v58. For more details see [https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf](https://storage.googleapis.com/wvdocs/Chrome_EME_Changes_and_Best_Practices.pdf)**

• The UI Framework now supports HLS Access DRM on Flash, Ad only, and Targeting Info workflow.

• The setDRMAuthenticateData API is added to the UI Framework. To play streams protected with Adobe Access DRM, invoke this API. Alternately, drmAuthenticateData attribute can be specified in the player. See [AdobePSDK.videoBehavior ](https://help.adobe.com/en_US/primetime/api/psdk/btvsdk-ui-framework/VideoBehavior.html)for details.

**Version 2.4.7**

The following features are new in version 2.4.7:

• Addition of the UI Configurator in the UI Framework

You can configure the player in one of the following ways:

• Using a JSON object

• Using APIs

To help generate the JSON object, Browser TVSDK provides a **UI Configurator **tool.

In this tool, you can select various settings, click **Test Configuration **to verify the settings, and click **Download Configuration **to download the settings. After downloading the file, you can pass the contents of this file as JSON object, to the ptp.videoPlayer API.

• Addition of the MediaPlayerItemConfig API to the UI Framework

Various features, including advertisingMetadata, advertisingFactory, adSignalingMode, networkConfiguration, customRangeMetadata, useHardwareDecoder, subscribeTags, adTags, thumbnailScrubber, billingMetricsConfiguration, can be configured through MediaPlayerItemConfig. For more information, see the AdobePSDK.MediaPlayerItemConfig documentation in the [Browser TVSDK API](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html)* * [documentation](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

In the UI Framework, the way of passing network configurations through the player configuration has been modified.

**Version 2.4.6**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`networkConfiguration: <network configuration object>`

`}`

`};`

**Version 2.4.7**

`var player = ptp.videoPlayer(‘#videoHolder', {`

`player: {`

`mediaPlayerItemConfig: {`

`networkConfiguration: <network configuration object>`

`}`

`}`

`};`

* Support for DRM and Analytics workflows in the UI Framework

DRM configurations and Analytics Tracking can be enabled through the UI Framework.

* Addition of `AdobePSDK.embedSWFinFullScreenDiv` API

This new API provides flexibility to the player app for selecting the div in which it can embed the FlashFallback.swf file.

* Replaced `getVersion`API from `AdobePSDK.MediaPlayer` class with `AdobePSDK.Version` class for TVSDK version related information. For details, see `AdobePSDK.Version` API [here](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.Version.html).

**Version 2.4.6**

The following features are new in version 2.4.6:

* **Browserify Support**

Browserify allows you to use the node.js style modules in the browser. You can define the dependencies and Browserify bundles everything into one JavaScript file.

* **Billing**

With the help of billing, Browser TVSDK can collect player usage metrics to bill Primetime customers.

>[!NOTE]
>
>The deprecated enum MediaPlayer.Events and deprecated constants in Enum PSDKErrorCode have been removed in version 2.4.6. For more information, see [Converting from Browser TVSDK 2.4.5 to version 2.4.6](https://helpx.adobe.com/primetime/conversion-guides/browser-tvsdk-245-to-246-for-javascript.html).

**Version 2.4.5**

The following features are new in version 2.4.5:

* **Full Event Replays and Ads** 

  HLS Full Event Replay (FER) streams now supports ad resolution and ad behaviors. To enable this support, set the ad signaling mode to `MANIFEST_CUES` when creating the `MediaPlayerItemConfig` object.

* **MediaplayerView ScalePolicy Support**
  
  Application developers can now specify a different scalePolicy for the view using MediaplayerView scalePolicy property.

* **Anamorphic Content Support**

  Anamorphic content playback is now supported when using MSE and Flash playback.

* **Selective application of `withCredentials`**

When `withCredentials` is set to true, the `Access-Control-Allow-Origin` header cannot be set to a wild card. Depending on the response of server, Browser TVSDK will selectively set the `withCredentials` attribute. For more information about this support, see [Browser TVSDK API docs](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/index.html).

**Version 2.4.4**

The following features were new in version 2.4.4:

* **Chromecast sample app**

This release provides support for a sender and receiver app that demonstrates playback of DASH VOD streams and DASH Widevine streams with client side ad insertion.

* **Advanced failover support**

This release contains support for advanced failover use cases (segment and server failover) for HLS VOD streams.

**Version 2.4.3**

The following features were new in version 2.4.3:

* **Custom tags for DASH VOD**

  Inline custom tags (Events) can be subscribed to and received as TimedMetadata object.

* **Playback of streams without extensions**

  HLS and DASH streams without extensions are now supported. For the manifest file, the resourceType needs to be specified when loading the resource. For segments and VTT files, the Content-Type response header is used to determine the content type.

**Version 2.4.2**

The following features were new in version 2.4.2:

* **API Parity**

For a complete list of the API parity, see the [TVSDK for 1.4 DHLS to Browser TVSDK 2.4 Migration Guide](https://helpx.adobe.com/primetime/migration-guides/tvsdk-14-dhls-browser-tvsdk-24.html).

* **Sample-AES support**

  This release adds support for Sample-AES encrypted content playback on MSE and Flash fallback. The requirement to host AES content over secure origin on Google Chrome have been removed.

* **Support for AAC containers**

  The playback of files with the .aac extension is now supported. This can be audio-only streams or alternate audio.

  >[!NOTE]
  >
  >AC3 and enhanced AC3 codecs are not yet supported.

* **Tokenized stream playback**

HLS streams that are delivered through a Content Delivery Network (CDN) can sometimes use authentication tokens on the manifest and segment requests for verification, and these tokens can be provided as URL parameters or as cookie headers. The playback of such streams are now supported.

**Version 2.4.1**

The following features were new in version 2.4.1:

* **UI framework**

This framework, designed to accelerate UI development for JavaScript-based video player applications, consists of APIs for including basic controls like play/pause and volume and for easily adding or removing elements like scrub bar states and closed caption settings. You can specify the behavior associated with controls, create custom controls, and skin the player UI. This all happens through the framework, with no need for manipulating the DOM structure directly.

* **HLS playback enhancements for Live streams**

This release supports discontinuities caused by ad insertion. It uses the EXT-PROGRAM-DATE-TIME tag followed by the EXT-MEDIA-SEQUENCE tag to synchronize across adaptive bitrate profiles for smooth playback.

* **VPAID 2.0 support**

The video player ad-serving interface definition (VPAID), version 2.0, provides a rich media experience for users and allows publishers to better target ads, track ad impressions, and monetize video content. This release supports linear JavaScript VPAID ads for video-on-demand (VOD) content.

* **Custom HLS tags**

Media streams can carry additional metadata in the form of tags in the playlist/manifest file. Browser TVSDK lets you specify and subscribe to additional tags and be notified when those tags appear in the manifest.

* **Ad markers displayed on the player timeline**

This release supports showing ad markers on the player timeline for both VOD and Live content. You can see this behavior in the reference player.

**Supported in 2.4**

The following features were available in version 2.4:

* **MP3 audio playback**

  This release supports MP3 audio playback on browsers with Media Source Extensions (MSE) and with the Safari video tag.

* **MP4 video playback**
  
  The following features are supported:

    * Single stream playback
    * Pre-roll and Post-roll MP4 ads with ad behaviors and tracking
    * Pre-roll and Post-roll HLS ads with ad behaviors and tracking
    * Pre-roll and Post-roll DASH ads with ad behaviors and tracking

## Supported platforms {#supported-platforms}

Browser TVSDK has specific requirements for the levels of platforms and software that it needs to run on. The following platforms and software levels are supported:

### Desktop configurations {#desktop-configurations}

* Microsoft Windows 7:

    * Internet Explorer 11+
    * Chrome 33+
    * Firefox 38+

* Microsoft Windows 8.1

    * Internet Explorer 11+
    * Chrome 33+
    * Firefox 38+

* Microsoft Windows 10

    * Edge+

* Apple OS X

    * Safari 9+
    * Chrome 33+
    * Firefox 38+

### Mobile Web configurations {#mobile-web-configurations}

* Android 4.4

    * Native browser
    * Chrome 33+

* Android 5.0

    * Native Browser
    * Chrome 33+

* Android 6.0

    * • Chrome 33+

* Apple iOS 9

    * Safari 9+
    * Chrome 33+

* Apple iOS 10

    * Safari 9+
    * Chrome 33+

**Google Chromecast (second-generation; for DASH playback only)**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Technology</strong> </p> </td> 
   <td><p><strong>Browser TVSDK Video Tag</strong><sup>1</sup></p> </td> 
   <td><p><strong>Browser TVSDK MSE</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>Default Technology</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>iOS</p> </td> 
   <td><p>MP4 and HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>-</p> </td> 
   <td><p>Video tag</p> </td> 
  </tr> 
  <tr> 
   <td><p>Android</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS and DASH</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Apple Safari 8</p> </td> 
   <td><p>MP4 and HLS</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 and HLS</p> </td> 
   <td><p>Video tag</p> </td> 
  </tr> 
  <tr> 
   <td><p>Google Chrome</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS and DASH</p> </td> 
   <td><p>MP4 and HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
  <tr> 
   <td><p>Mozilla Firefox</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS and DASH</p> </td> 
   <td><p>MP4 and HLS</p> </td> 
   <td><p>MSE<sup>2</sup></p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 7)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>-</p> </td> 
   <td><p>MP4 and HLS</p> </td> 
   <td><p>Flash</p> </td> 
  </tr> 
  <tr> 
   <td><p>Internet Explorer 11</p> <p>(Windows 8.1)</p> </td> 
   <td><p>MP4</p> </td> 
   <td><p>HLS, DASH</p> </td> 
   <td><p>MP4 and HLS</p> </td> 
   <td><p>MSE</p> </td> 
  </tr> 
 </tbody> 
</table>

## Feature matrix {#feature-matrix}

Here is a list of the supported and unsupported features for this release:

* *MP3 Audio Features — Core Playback*
* *MP4 Video Features — Core Playback*
* *MP4 Video Features — Core Ad Insertion*

>[!NOTE]
>
>*In the feature matrix tables below, a 'Y' means that the feature is supported in the current release.*

### MP3 Audio Features {#mp-audio-features}

**Table 1: Core Playback {#table-core-playback}**

|Category|Content Type|Feature|Flash|HTML5: FF, IE, Chrome, Android Chrome|HTML5: Safari, iOS Safari|
|--- |--- |--- |--- |--- |--- |
|Playback|MP3 VOD|General Playback (Play, Pause, Seek)|Not Supported|Y|Y|

1 The Browser TVSDK Video tag does not support streaming and DRM. The codec and container support is not the same across all browsers.

2 Firefox defaults to Flash Player for version 41 or earlier.

### MP4 Audio Features {#mp-audio-features-1}

**Table 2: Core Playback**

|Category|Content Type|Feature|Flash|HTML5: FF, IE, Chrome, Android Chrome|HTML5: Safari, iOS Safari|
|--- |--- |--- |--- |--- |--- |
|Playback|MP4 VOD|General Playback (Play, Pause, Seek)|Not Supported|Y|Y|

**Table 3: Core Ad Insertion**

|Category|Content Type|Feature|Flash|HTML5: FF, IE, Chrome, Android Chrome|HTML5: Safari, iOS Safari|
|--- |--- |--- |--- |--- |--- |
|Ad Insertion|MP4 VOD|Pre-roll (MP4)|Not Supported|Y|Y|
|Ad Insertion|MP4 VOD|Post-roll (MP4)|Not Supported|Y|Y|

For more information about HLS or DASH feature support, see below.

## HLS feature matrix {#hls-feature-matrix}

Here is the feature matrix for the HLS features in Browser TVSDK.

* *HLS Core playback*
* *HLS Advanced playback features*
* *HLS Content protection features*
* *HLS Core ad insertion features*
* *HLS Advanced ad insertion features*
* *HLS Integrations*

>[!NOTE]
>
>*In the feature matrix tables below, a 'Y' means that the feature is supported in the current release.*

### HLS Features {#hls-features}

The following features are supported:

**Table 4: HLS Core playback**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>General playback (play, pause, seek)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>General playback (play, pause, and seek)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Adaptive bit rate</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708 captions</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>VOD only</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Manifest Failover</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Advanced Failover</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>QoS and player notifications</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Limited QoS support</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Support for cookie headers</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Setting buffer control parameters</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Set adaptive</p> <p>bit-rate controls</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Custom tags</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td>Late-binding audio</td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>302 redirect</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 5: HLS advanced playback features**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Playback at offset</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Audio-only playback</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Trick Play</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Smooth Trick Play</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>ID3 parsing</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Discontinuity marker support</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Tokenized streams</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Billing</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 6: HLS Content protection features**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Content Protection</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Content Protection</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Content Protection</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>Adobe Access</p> </td> 
   <td><p>Not Supported</p> </td> 
   <td><p>FairPlay</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 7: HLS Core ad insertion features**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Pre-roll (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Mid-roll (HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Post-roll (MP4/HLS)</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Ad resolution and behaviors</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Default ad policy</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Creative Repackaging (MP4 to HLS)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 8: HLS Advanced ad insertion features**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Ad only</p> </td> 
   <td><p>Not Supported</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Targeting parameters</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Custom parameters</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Custom ad policy</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Lazy ad loading</p> </td> 
   <td><p>Y</p> </td> 
   <td><p>Not Supported</p> </td> 
   <td><p>Platform Limitation</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Companion ads, Banner ads, Clickable ads</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>SWF</p> </td> 
   <td><p>JavaScript</p> </td> 
   <td><p>JavaScript</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 9: HLS Integrations {#table-hls-integrations}**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>Flash</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
   <td><p><strong>HTML5: Safari, iOS Safari</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integrations</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Adobe Analytics VHL integration</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## DASH feature matrix {#dash-feature-matrix}

Here is the feature matrix for the DASH features in Browser TVSDK.

• *DASH Core playback features*

• *DASH Advanced playback features*

• *DASH Content protection features*

• *DASH Core ad insertion features*

• *DASH Advanced ad insertion features*

• *DASH Integrations*

>[!NOTE]
>
>In the feature matrix tables below, a Y means that the feature is supported in the current release.

### DASH Features {#dash-features}

The following features are supported:

**Table 10: DASH Core playback features**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>General playback (play, pause, seek)</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>General playback (play, pause, and seek)</p> </td> 
   <td><p>Not Supported</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Adaptive bit rate</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>608/708 captions</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>WebVTT</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Failover</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>QoS and player notifications</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Support for cookie headers</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Setting buffer control parameters</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Set adaptive bit-rate controls</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Custom tags (EventStream)</p> </td> 
   <td><p>VOD only (Inline)</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Late-bound audio</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>302 redirect</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 11: DASH Advanced playback features**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Playback at offset</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Audio-only playback</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Trick play</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Smooth Trick Play</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>ID3 parsing</p> </td> 
   <td><p>Not Supported</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Multi-period support</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Tokenized streams</p> </td> 
   <td><p>Not Supported</p> </td> 
  </tr> 
  <tr> 
   <td><p>Playback</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Billing</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 12: DASH Content protection features**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Content Protection</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>AES-128</p> </td> 
   <td><p>Not Supported</p> </td> 
  </tr> 
  <tr> 
   <td><p>Content Protection</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Sample-AES</p> </td> 
   <td><p>Not Supported</p> </td> 
  </tr> 
  <tr> 
   <td><p>Content Protection</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>DRM</p> </td> 
   <td><p>• Widevine on Chrome, Firefox 47 and later, and Chromecast</p> <p>• PlayReady on Internet Explorer on Windows 8.1 and Edge</p> <p>• Primetime DRM for Windows Firefox (video only)</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 13: DASH Core ad insertion features**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>HTML5 FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Pre-roll (MP4/DASH)</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Mid-roll (DASH)</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Post-roll (MP4/DASH)</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>FER VOD</p> </td> 
   <td><p>Ad Resolution and Behaviors</p> </td> 
   <td><p>Not Supported</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Default ad policy</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VAST 2.0/3.0</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>VMAP 1.0</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Creative Repackaging (MP4 to DASH)</p> </td> 
   <td><p>Not supported</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 14: DASH Advanced ad insertion features**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>HTML5</strong> FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Ad only</p> </td> 
   <td><p>Y</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Targeting parameters</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Custom Parameters</p> </td> 
   <td><p>VOD only</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Custom ad policy</p> </td> 
   <td><p>Not Supported</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Lazy ad loading</p> </td> 
   <td><p>Not Supported</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>Companion ads,banner ads, clickable ads</p> </td> 
   <td><p>Not Supported</p> </td> 
  </tr> 
  <tr> 
   <td><p>Ad Insertion</p> </td> 
   <td><p>VOD</p> </td> 
   <td><p>VPAID 2.0</p> </td> 
   <td><p>Not Supported</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 15: DASH Integrations**

<table> 
 <tbody> 
  <tr> 
   <td><p><strong>Category</strong></p> </td> 
   <td><p><strong>Content type</strong></p> </td> 
   <td><p><strong>Feature</strong></p> </td> 
   <td><p><strong>HTML5: FF, IE, Chrome, Android Chrome</strong></p> </td> 
  </tr> 
  <tr> 
   <td><p>Integrations</p> </td> 
   <td><p>VOD + Live</p> </td> 
   <td><p>Adobe Analytics VHL integration</p> </td> 
   <td><p><strong> </strong></p> <p>Y</p> </td> 
  </tr> 
 </tbody> 
</table>

## Issues fixed {#issues-fixed}

**Issues fixed in 2.4.12 Update (Build 204)**

The following issues are fixed in Browser TVSDK verison 2.4.12 Update (Build 204):

• **21647**- TVSDK should allow automatic video playback on iOS devices when audio is muted.

• **21465**- Error Key System Access Denied is received when playing a DRM-protected DASH stream after a DASH Live stream is played.

• **21442**- Enable content autoplay on iOS Web, after preroll ad is played with a user gesture.

• **21240**- Provided API to filter VPAID ads parsed from Auditude/VMAP.

**Issues fixed in version 2.4.11**

The following issues are fixed in Browser TVSDK verison 2.4.11:

**Core playback features:**

• **19192**: TVSDK now implements TextFormat:bottomInset and TextFormat:safeArea. Due to these enhancements, closed captions can be re-positioned if the control bar is displayed on the screen.

• **21009**: Closed captions persist on the screen in case of seek across discontinuity till new captions appear.

• **21141**: Seek back is rejected due to a race condition during segment append.

• **21142**: Making seekable playback ranges available when the player is in INITIALIZED state. Due to these changes, start session at position is now supported.

• **21363**: 608/708 closed captions are going out of sync after ad insertion for DASH streams.

**Ad insertion features:**

• **21179**: Mid-roll related issues (long pauses, black frames) with VOD content are now resolved by correctly setting the ad.primaryAsset.adParameters property.

• **21257**: The MP4 file with highest bit rate is selected for transcoding if MP4 is not a valid mime-type and the creative repackaging feature is enabled.

• **21361**: TVSDK now passes ad system and creative ID from the VAST response as query parameters in the creative packaging request in order to support additional normalization rules.

**Issues fixed in version 2.4.10**

The following issues are fixed in Browser TVSDK verison 2.4.10:

**Core playback features:**

• **21060**: Invalid codec error thrown with HLS streams that contain discontinuity and the ISO BMFF boxes run to end of stream.

• **21045**: Auto play not working on iOS after the first video playback in a playlist is completed.

• **20975**: Frame rate is returned as NaN by the QoS provider on Chrome browser.

• **20823**: Unsupported codec error thrown on encountering segments with no data.

• **20769**: SDK now starts with the current bit rate on seek instead of switching immediately based on ABR policy.

• **20031**: When in portrait mode on IE11 (Windows 8.1), the video screen becomes small. Content protection feature:

• **19316**: Skip segments that fail decryption in case of HLS AES-128 streams.

**Issues fixed in version 2.4.9**

The following issues are fixed in Browser TVSDK verison 2.4.9:

**Core playback features:**

• **13407**: DASH streams may stall if Firefox stops sending "ontimeupdate" event during playback.

• **16380**: During Muxed Audio Video Content Playback of segments having non-matching start times via MSE, Audio Sync Error between Representations accumulates on ABR switches, ultimately resulting in Error (Chromium issue #663686).

• **17985**: On playing particular ISO-BMFF stream on Firefox browser, playback gets stuck(Firefox issue #1342913). This is fixed since Firefox v53.

• **19141**: Uncaught (in promise) ReferenceError: width is not define.

• **18997, 19299**: Video flicker issue at segment boundary. This was happening since SDK was not calculating the last sample's Composition time offset correctly.

• **19780**: Playback does not starts for HLS content and HLS Ad on Firefox v53 (Firefox issue #354653).

• **20046**: Program Date Time is received as key instead of value when received as timed metadata object.

• **20047**: useDefaultResizeHandler throws an error with Flash fallback.

• **20179**: Flash Fallback not working with Flash Player v25.0.0.171.

• **20293**: Firefox stops buffering data for certain HLS streams leading to stall.

• **20626**: Player throws media decode error on Chrome due to incorrect handling of video samples with zero duration.

• **20078**: Playback stalls on browser error 'QuotaExceeded'.

• **18639**: In HLS Live stream 608 CC text sometime appear as misspelled.

• **20028**: ClosedCaptions size parameter doesn't change font size.

• **20613**: Closed captions boxes overlap with each other making them illegible.

**Core Ad Insertion (CSAI) features:**

• **20043**: Missing Ad impression and Ad tracking calls with multiple ads and third party redirects.

• **20044**: When using creative repackaging, all ads in the ad break need to be repackaged successfully otherwise the ad break is completely discarded.

• **20097**: Ad playback is skipped and main content resumes immediately rather than wait for timeout of 20 seconds if ad manifest is not available.

**Issues fixed in version 2.4.8 Update (Build 6002)**

The following issues are fixed in Browser TVSDK verison 2.4.8 Update (Build 6002):

• **14126:** Playback may stall on Firefox (issue #1316024) due to internal gap in MSE source buffer. Try seeking in order to resume playback

• **19608:** Fix to honor the timeoffset value from Auditude VMAP response.

• **19635:** Fixes Video Stall in Internet Explorer 11 on Windows 10.

• **19761:** Fixes for ABR issues with HLS.

• **19780:** Fixes the Ad playback with HLS content that was broken in Mozilla Firefox v53.

• **19877 and 19744:** The issues fixes the inconsistency in selecting bitrate after a seek operation. Now the bitrate selection on seek is the lower value of the current bitrate and the bitrate at the start-up.

• **19881:** Playback stuck and buffering overlay appears for infinite time after seeking is performed for 3-4 times.

• **19884:** Confirm compliance with Chrome 59 Beta Verified Media Path (VMP) requirements. bTVSDK was able to playback Widevine DRM content with Chrome 59 Beta.

• **19916:** DRM playback on UI-Framework was broken. Now, it invokes acquireLicense even if there is no policy in the metadata.

**Issues fixed in version 2.4.8**

The following issues are fixed in Browser TVSDK 2.4.8 release:

• **10075**: When seeking ahead of timeline, play complete event was not received on Firefox and Chrome and seek event was not received on Firefox.

• **15775**: Play complete event not received on Windows 8.1 Internet Explorer.

• **17306**: For SSAI streams, playback is supported. Tracking of stitched ad is not supported.

• **19142**: At times rewind causes the video player to remain in buffering state forever.

• **19218**: Ad markers are not available through UI framework.

• **19219**: Ads only playback not works through UI framework.

• **19222**: AES-128 key is requested once for a playlist and subsequent requests are served from the cache. Earlier it was getting requested for each segment.

• **19597**: "Uncaught TypeError: Cannot read property 'log' of undefined" was seen with Chrome canary builds.

• **19605**: adRequestDomain was not available when in Flash Fallback mode.

• **19608**: VMAP ads were not getting inserted for HLS Live streams. SDK now considers the cue markers and does not rely on time offset values in VMAP responses.

• **19637**: Ads only playback leads to script error at end of ad.

• **19732**: CRS playlist requests were failing with 404 error. The 1401 and 1403 requests from Browser TVSDK are now updated to take care of that.

• **19762**: acquireLicense used to be called before setAuthenticationToken because of which a valid license was returned irrespective of the token validity. This is fixed now and acquireLicense is called only after setAuthenticationToken response.

**Issues fixed in version 2.4.7**

The following issues were fixed in version 2.4.7:

• **8397**: HLS Live streams generated through Adobe Media Server might not play if the segments do not start with a Key frame.

• **13606**: Multiple Seek related issues fixed for HLS stream on Chrome browser.

• **14807**: On Chrome browser, if seek or pause is triggered immediately after play(), playback may stop with error DOMException: The play() request was interrupted by a call...(Chromium issue# 593273).

• **19085**: MediaPlayer Params such as volume, abrControlParameters, and ccStyle are not set to Defaults on Resetting the Player.

**Issues fixed in version 2.4.6**

The following issue was fixed in version 2.4.6:

• **18093**: TimedMetadata for the tag next to the subscribed tag is returned when you use Flash Player version 24 in Flash Fallback mode.

**Issues fixed in version 2.4.4**

The following issues were fixed in version 2.4.4:

• **8711**: With MSE, 608/708 captions are left justified by default.

• **13934**: ABR settings for ads are not applicable when playing with HLS Live streams.

• **14079**: Longevity for HLS Live streams with low DVR window may fail since the playback may fall behind due to network latency issues. Click on the live point to resume playback.

• **15037**: The samples shipped with the player UI framework does not work on Microsoft Internet Explorer 10 on Windows 7.

• **15913**: For HLS VOD streams, on Chrome, stream will not play if manifest response is 304 not modified. This is fixed since Chrome v55 (Chromium issue 633696).

• **16103**: On Android Chrome, under low bandwidth conditions, playback may stall with the Uncaught TypeError: Cannot read property 'programDateTime' of undefined error.

• **16265**: For HLS VOD and Live streams, seek across discontinuities do not work.

• **16709**: Resuming HLS Live stream with PDT and discontinuity marker may lead to player getting stuck in buffering.

## Known Issues and Limitations {#known-issues-and-limitations}

The limitations and known issues in Browser TVSDK are mentioned below.

**Table 16: Core Playback Features**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Content type</strong></td> 
   <td><strong>Feature</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (DASH playback only)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>General Playback (Play, Pause, Seek)</td> 
   <td><p>• Media formats other than HLS are not supported.</p> <p>8799: Flash fallback does not take care of mixed content and hence it need to be ensured that Content, Ad and other URLs do not lead to mixed content (secure and unsecure content together).</p> <p>• 19271: Multiview playback via UI framework is not supported in Flash fallback mode.</p> <p>• Flash fallback does not work on Microsoft Internet Explorer 8 and 9 on Windows 7 since these versions are not supported by the SDK.</p> <p>• 20262: Flash fallback adds custom parameters to targeting info list. Also priority order of custom parameters is different in case of Flash and MSE.</p> <p>• 20653:Browser TVSDK Flash fallback does not work on Win10 with Creators Update.</p> <p>• Flash Fallback works with Flash Player version 23 and later.</p> <p>• 20087 - Chrome 59 Beta with</p> <p>Flash 25.0.0.171</p> <p>Beta(default), HLS playback is not working on Flash Fallback mode. It is working fine on Canary.</p> </td> 
   <td><p>• 12563: Dash Streams with audio codec mp4a.40.02 do not playback on Firefox due to unsupported audio codec string in MPD. Audio Codec mp4a.40.2 is supported.</p> <p>15029: While switching between videos in multiView in UI-Framework, play/pause button does not get updated accordingly.</p> <p>• 16034:On Windows 8.1 IE, calling reset() leads to Unknown MIME type error. Please reload the media to resume playback.</p> <p>• 18235: Certain seek issues are observed with DASH vod streams with Ads.</p> <p>• 18727: Error API is not supported for MSE</p> <p>18750: Status Change events might be out of order in some cases for both SDK and UI framework and in UI Framework, IDLE and Initializing StatusChange events might be missing for the event Listeners added after resource has been loaded.</p> <p>• 18889: If MediaPlayer is in ERROR state, the view object is not returned.</p> <p>• 19039: If AdobePSDK. MediaPlayer. seekToLocal() is used with a value greater than EOF, then playback starts from beginning in case of MSE.</p> <p>• 19049: No error state reported for Flash Player on Chrome, IE, Firefox when video is blocked during the playback.</p> <p>• 17205: Video playback stalls on playing unmuxed stream for few hours while audio continues to play (Chromium issue# 664033).</p> <p>• 12308: DASH streams with composition_ time_offset specified may have timeStampOffset applied to it on Chrome browser leading to negative decode time and hence MEDIA_ERR_ SRC_NOT_ SUPPORTED error (Chromium issue #398141).</p> <p>• 14126: Playback may stall on Firefox (issue# 1316024) due to internal gap in MSE source buffer. Try seeking in order to resume playback.</p> <p>• 19115: MS Edge and IE 11 (Win 8.1 and 10) does not set Origin to null on CORS redirect and yet fails because header is not null leading to playback error.</p> <p>• 19861:Issue with append behavior on source buffer for media already played. Chrome rejects the appended fragment including moov, causing subsequent decode error. (Chromium issue #735335)</p> <p>19921: Playback stalls for certain HLS content even though its buffered successfully (Chromium issue #713540)</p> <p>• 20444:Seeking to end of buffered range on IE and Edge may cause playback to stall.</p> <p>• 20511: Sometimes seek reject can be observed for HLS streams with or without ads.</p> <p>• 20743: On Windows 10 Chrome, HLS Live stream plays for few seconds before MP4 pre roll playback.</p> <p>• 21043: Video dimension may not be correct on initial load due to lack of metadata.</p> <p>• 21115: Android User gesture is required to start playback if pre-roll ad is available for videos in a playlist.</p> <p>• HLS Live does not support the time stamp rollover.</p> <p>• AAC-SSR audio is not supported.</p> <p>Audio codecs AC3 and Enhanced AC3 are not supported.</p> <p>• For streams with timestamp discontinuity but without discontinuity markers</p> <p>• Playback might have glitches and incorrect seeking due to jumps.</p> <p>• Content duration and playback duration might not match.</p> <p>• Discontinuities across representations and renditions should match other wise may lead to sync and stall issues.</p> <p>• Captions and WebVTT might not appear close to end of stream.</p> <p>• Audio codec changes are not supported across timestamp jumps.</p> <p>• Ad insertion is not supported.</p> <p>• Fast forward trick mode may lead to playback loop on Win 8.1 IE 11 (MS issue #12446268).</p> <p>DASH:</p> <p>• For Live streams - live profile with dynamic type is supported.</p> <p>• For VoD streams - live profile with static type is supported.</p> <p>For VoD streams - ondemand profile is not certified for ad workflows.</p> </td> 
   <td><p>• DASH Live and DASH Video on Demand streams are not supported.</p> <p>• PIP(Picture in Picture) video playback is not supported on iOS in full screen mode.</p> <p>On Safari (Video Tag) extension less manifest without having correct content type header do not work.</p> </td> 
   <td><p>• applicationID in sender app need to be the same as generated on registering the URL of Receiver as a Custom Receiver app.</p> <p>• Reference player is certified for DASH workflows. UI framework is not certified.</p> <p>For list of supported media codecs, refer <a href="https://developers.google.com/cast/docs/media"><em>here</em></a>.</p> </td> 
  </tr> 
  <tr> 
   <td>FER VOD</td> 
   <td>General Playback (Play, Pause, Seek)</td> 
   <td> </td> 
   <td>18098: Certain seek issues are observed with HLS LBA FER stream.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Adaptive Bitrate</td> 
   <td><p>• 20079: Buffer re-write on seek within buffered range.</p> <p>20080: Flash ABR behavior is in-consistent with MSE.</p> </td> 
   <td><p>• Audio only fallback variant in an ABR stream is ignored due to buffer related limitations.</p> <p>• 12289: ABR control params don't apply for audio in case of unmuxed HLS/DASH streams.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>608/708 Captions</td> 
   <td> </td> 
   <td><p>• 7810: On Android 4.4.4 Chrome does not seem to have support for basic CSS font families used by the player and hence font style change function not working.</p> <p>• The CC channels cannot be changed in case of 608 captions.</p> <p>• Advanced styling features are not supported for 608 captions.</p> <p>Embedded Captions (608/708), signaled via Accessibility tag are supported.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>WebVTT</td> 
   <td> </td> 
   <td><p>• 5206: Region tags in WebVTT file are ignored by the player when displaying the captions.</p> <p>• DASH: Fragmented /Segmented VTT files are not supported.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Manifest failover</td> 
   <td>21056: With Flash Fallback, Failover does not happen for Live stream if the primary stream returns a 404 error during the playback.</td> 
   <td>Manifest failover is applicable only for content and not ads.</td> 
   <td>Missing playlist failover works on Safari only for HTTP error code 404.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Advanced Failover</td> 
   <td> </td> 
   <td><p>• Segment failover does not support skipping unavailable segments and continuing playback.</p> <p>20533: Missing segments in a playlist should be treated as a Discontinuity and playback should resume from next available segment.</p> <p>21267: Stream switching due to fail over may lead to download of older segments..</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>QoS and Player notifications</td> 
   <td>21129: Frame rate is not available in case of Flash Fallback.</td> 
   <td><p>• 11170:</p> <p>Timed_Event is not available for Browser TVSDK with MSE unlike for Browser TVSDK with Flash Fallback.</p> <p>21129: Frame rate is not calculated for Live streams.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Support for Cookie headers</td> 
   <td> </td> 
   <td> </td> 
   <td><p>withCredentials flag and cookie headers are not supported on Safari.</p> <p>21051: To allow cookies in Safari, enable "Cookies and website data" setting from Preferences &gt; Privacy.</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Custom Tags</td> 
   <td>14763: Custom tags other than starting with # should not be supported. Right now TimedMetadata object is created and reported for such tags during Flash Fallback.</td> 
   <td>Streams with inband custom tags are not certified.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Late Binding Audio</td> 
   <td> </td> 
   <td><p>• Ad insertion is not supported with HLS Live LBA streams.</p> <p>• 17273: HLS VOD LBA streams switch to default rendition in case of failover and cannot be switched back to last selected.</p> <p>• 20251: HLS Live LBA stream may stall on seeking.</p> <p>• 20497: Player remains in buffering state if HLS LBA unmuxed streams have missing audio or video frames close to end of stream.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>302 Redirect</td> 
   <td> </td> 
   <td><p>15787: 302</p> <p>redirect optimization is not supported on windows Edge and IE browsers as these do not support the responseURL property in the XMLHttpRequest object.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Table 17: Advanced Playback Features**

<table> 
 <tbody> 
  <tr> 
   <td>Content Type</td> 
   <td>Feature</td> 
   <td>Flash</td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (DASH playback only)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Playback at offset</td> 
   <td><p>Starting playback at particular offset value is not supported MP4 contents.</p> </td> 
   <td>20492: Mid-roll ads preceding the offset are played before content resumes from the offset value.</td> 
   <td>Playback with offset feature is not supported on iOS.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Trick Play</td> 
   <td>Smooth Trickplay does not work for streams having No iFrame renditions.</td> 
   <td><p>• Trick Play adaptations are not supported on Firefox and Internet Explorer and hence reverse trick mode is not available on these browsers.</p> <p>• Trickplay is not available when playing content along with ads.</p> <p>• 10435: During DASH playback, video freezes on forward trick play on Internet Explorer (Win 8.1)</p> <p>intermittently. This is happening since we are using the video elements playbackRate property without the trick play adaptation.</p> <p>14182: At times, during rewind on Chrome browser, seek event may not be received and hence trick mode will not work.</p> <p>• 14942: Playback rates can be set on Chrome for Android even in case of non trick play streams but setting will not be applied and playback will continue at normal rate.</p> <p>• 17308: Seek does not work in Trickplay mode.</p> <p>• 17309: On Chrome browser, reverse trick mode cannot be sustained for more than 2 seconds.</p> <p>19272: Trick play may not recover from buffering on Windows 10 Edge browser in case of DASH streams.</p> </td> 
   <td>Rewind trick mode is not supported.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>ID3 Parsing</td> 
   <td>20346: Text encoding byte of ID3 frames should also be returned by SDK.</td> 
   <td><p>ID3 tags available in audio data transport streams(ADTS) are ignored by the SDK.</p> <p>• 12378: ID3 timed metadata is parsed at different times on Flash and browser with MSE support and hence the display behavior on reference player timeline is also different.</p> <p>• 19247: ID3 parsing is not supported on UI framework.</p> </td> 
   <td><p>• 20323: PRIV ID3 tag used to signal timestamp of first sample of aac segment is not parsed by Safari (Safari issue #32422733)</p> <p>• 20350: On certain devices (including MAC OS X 10.1, iPad10) Safari does not provides cue change event when in trick mode and hence ID3 frames are not received. (Safari issue #32450526)</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Discontinuity marker support</td> 
   <td> </td> 
   <td><p>• Client side ad insertion is not supported with HLS streams containing discontinuity.</p> <p>• Audio Codec change is not allowed across discontinuities in HLS stream.</p> <p>• Audio Track switch is not supported for HLS stream with discontinuity markers</p> </td> 
   <td>Discontinuity sequence number is a requirement for HLS streams with discontinuity in order to playback on Safari.</td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Table 18: Content Protection Features**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Content Type</strong></td> 
   <td><strong>Feature</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (DASH playback only)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>AES-128</td> 
   <td> </td> 
   <td>Byte range is not supported with AES-128 encrypted content.</td> 
   <td>12324: HLS AES-128 encrypted streams fails to playback on Safari if IV tag is not specified.</td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>DRM</td> 
   <td> </td> 
   <td><p>• 12660: HTML5 player throws Internal Server Error for expired PlayReady encrypted dash contents.</p> <p>• 16720: DASH DRM encrypted content wont work if start attribute in period tag is missing.</p> <p>• 18589: Playback is not supported for DRM protected Dash VoD Multiperiod streams with Xlink.</p> <p>• 18653: Playback of Widevine MultiPeriod Content with Multiple Keys, stops at first period and cannot switch to next Period.</p> <p>• 18656: Playready MultiPeriod Stream, encrypted with different keys, wont playback.</p> <p>Playready 2.0 for Dash is not certified.</p> <p> </p> <p> </p> </td> 
   <td>12602: HLS Fairplay DRM metadata is repeatedly refreshed by HTML5 player on Safari</td> 
   <td><p>DASH Widevine DRM content packaged through Bento4 can be played. Content packaged through Offline Packager and Shaka packager do not play. DASH PlayReady DRM is not supported.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Table 19: Core Ad Insertion Features (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Content Type</strong></td> 
   <td><strong>Feature</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (DASH playback only)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Pre/Mid/Post</td> 
   <td> </td> 
   <td><p>• Preroll ads with HLS live content are played in Dual player mode.</p> <p>• DASH ads with HLS contents and HLS ads with DASH contents are not supported.</p> <p>• 19002: In HTML5 Player with MSE adBreak. insertionType does not return correct value to depict correct insertion type i.e. client inserted and or server inserted.</p> <p>7794: On mobile devices (iOS, Android with Chrome 33 or lower or Native Browser) where the default control bar is visible in full screen mode, seek bar and fast forward buttons are available when Ads Play.</p> <p>• 11048: Switch from ad to HLS Live content is not smooth in case of Media Source Extensions.</p> <p>• 16083: On Android 4.4 Chrome v52, At times HLS ad with HLS content may lead to pipeline decode error after stalled playback.</p> <p>• 16097: Errors encountered during Ad break are not handled, may cause the main stream to stop playback.</p> <p>• 18095: MP4 ads are not supported with HLS live content.</p> <p>19120: Multiple seeks on HLS ads with HLS contents may cause the stream to stop playback.</p> <p>• 19131: Buffering overlay may appear while switching from pre-roll ad break to content.</p> <p>• 20296: In case of HLS Live streams, seeking back in DVR window followed by seeking over resolved mid rolls may lead to playback stall.</p> <p>• 20298:HLS Live streams with mid rolls stall the moment first mid roll ad moves out of the DVR window.</p> <p>• 20317: HLS Live streams may stall when switching to next ad or from ad to content in case ad break contains more than one ad.</p> 
    <ul> 
     <li>Ads in the DVR window of HLS Live streams are not resolved.</li> 
    </ul> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>SDK does not honor sequence attribute inside VMAP response for VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VAST 2.0/3.0</td> 
   <td> </td> 
   <td>20779: The SDK does not honor the sequence attribute inside the VMAP response for VAST adSource.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>VMAP 1.0</td> 
   <td> </td> 
   <td>12014: VMAP repeat attribute is not supported.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Creative Repackaging</td> 
   <td> </td> 
   <td>21464: Ad response is discarded completely if creative repackaging fails for one of the ads in the ad break.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Table 20: Advanced Ad Insertion Features (CSAI)**

<table> 
 <tbody> 
  <tr> 
   <td><strong>Content Type</strong></td> 
   <td><strong>Feature</strong></td> 
   <td><strong>Flash</strong></td> 
   <td><strong>HTML5 in Firefox, IE, Chrome, Android Chrome</strong></td> 
   <td><strong>HTML5 in Safari, iOS Safari</strong></td> 
   <td><strong>Chromecast (DASH playback only)</strong></td> 
  </tr> 
  <tr> 
   <td>VOD</td> 
   <td>Ad only</td> 
   <td> </td> 
   <td>20056: Player technology property is not relevant since it is based on main content which is empty in case of Ad Only playback</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>VOD + Live</td> 
   <td>Custom Ad Policy</td> 
   <td> </td> 
   <td><p>• Ad behaviors are not supported with MP4 ads and MP4 content.</p> <p>• 13973: Custom ad behaviors - SKIP policy does not throw complete event when used with MSE.</p> <p>• 14939: Custom ad behavior policies skip and skip ad break are not working for DASH content.</p> <p>• 17131: First frame of the ad is visible and then content resumes in case of SKIP ad break policy.</p> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>Companion ads/ banner ads/ Clickable ads</td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>Banner Ads are not visible when using reference player.</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td>VPAID 2.0</td> 
   <td> </td> 
   <td><p>• Ad behaviors are not supported for VPAID ads.</p> <p>• 15032: VPAID ads in combination with MP4 or HLS ads in an ad break are not supported.</p> <p>• 19001: On Android and iOS when VPAID ad is played with MP4 as main content double audio tracks are audible, one of main content and one of ad.</p> <p>• 20762: VPAID ads are not supported with Picture in Picture (PIP).</p> <p>• 21172: Play complete event is not received for HLS VOD content with VPAID ads.</p> <p>• 21173: onAdBreakCompleteEvent is not received for HLS VOD content and post roll VPAID ads.</p> </td> 
   <td>Player toggles between normal mode and fullscreen mode while switching between VPAID ad and Main content.</td> 
   <td> </td> 
   <td> </td> 
  </tr> 
 </tbody> 
</table>

**Table 21: Integrations**

| **Content Type** |**Feature** |**Flash** |**HTML5 in Firefox, IE, Chrome, Android Chrome** |**HTML5 in Safari, iOS Safari** |**Chromecast (DASH playback only)** |
|---|---|---|---|---|---|
| VOD + Live |Adobe Analytics VHL integration |  |19004: Video Analytics tracking is not available through UI Configurator Tool. |  |  |

## Helpful resources {#helpful-resources}

* See complete help documentation at [Adobe Primetime Learn & Support](https://experienceleague.adobe.com/docs/primetime.html) page.
