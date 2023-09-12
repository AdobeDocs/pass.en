---
description: Browser TVSDK supports a number of HLS features that you can implement to add functionality to your video applications.
title: Supported HLS features
exl-id: 111a6683-fb5c-4f0a-8665-5b1aab77056c
---
# Supported HLS features {#supported-hls-features}

Browser TVSDK supports a number of HLS features that you can implement to add functionality to your video applications.

* [HLS Core playback](#hls-core-playback) 
* [HLS Advanced playback features](#hls-advanced-playback) 
* [HLS Content protection features](#hls-content-protection) 
* [HLS Core ad insertion features](#hls-core-ad-insertion) 
* [HLS Advanced ad insertion features](#hls-advanced-ad-insertion) 
* [HLS Integrations](#hls-integrations)

>[!TIP]
>
>In the feature matrix tables below, ![supported icon](assets/supported15.png) means that the feature is supported in the current release.

>[!TIP]
>
>In the Safari column "Platform Limitation" means that the use case is not supported because that platform does not allow implementation of support for it. In the case of a insertion, use SSAI. If there are playback limitations important to you, force fallback to Flash on Safari until the platform supports the ad insertion use case.

<!--<a id="section_9FB9193D5763448CB228B96164661738"></a>-->

The following features are supported: 

<!-- 

Removed Nielsen row 
<table id="table_D9E2D82992554905A0A551CC71AFA189"> 
 <title>HLS integrations</title> 
 <tgroup cols="6"> 
  <colspec colnum="1" colname="col1" colwidth="*" /> 
  <colspec colnum="2" colname="col2" colwidth="*" /> 
  <colspec colnum="3" colname="col3" colwidth="*" /> 
  <colspec colnum="4" colname="col4" colwidth="*" /> 
  <colspec colnum="5" colname="col5" colwidth="*" /> 
  <colspec colnum="6" colname="col7" colwidth="*" /> 
  <thead> 
   <tr> 
    <th colname="col1" morerows="1" class="entry"> Category </th> 
    <th colname="col2" morerows="1" class="entry"> Content type </th> 
    <th colname="col3" morerows="1" class="entry"> Feature </th> 
    <th colname="col4" morerows="1" class="entry"> Flash </th> 
    <th namest="col5" nameend="col7" class="entry"> HTML5 </th> 
   </tr> 
   <tr> 
    <th colname="col5" class="entry"> FF, IE, Chrome, Android Chrome </th> 
    <th colname="col7" class="entry"> Safari, iOS Safari </th> 
   </tr> 
  </thead> 
  <tbody> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Adobe Analytics VHL integration </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
   <tr> 
    <td colname="col1"> Integrations </td> 
    <td colname="col2"> VOD + Live </td> 
    <td colname="col3"> Nielsen support </td> 
    <td colname="col4">![supported icon](assets/supported15.png) </td> 
    <td colname="col5">![supported icon](assets/supported15.png) </td> 
    <td colname="col7">![supported icon](assets/supported15.png) </td> 
   </tr> 
  </tbody> 
 </tgroup> 
</table>

 -->

## HLS integrations {#hls-integrations}

| Category | Content type | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
|Integrations|VOD + Live|Adobe Analytics VHL integration|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|

## HLS advanced ad insertion features (CSAI) {#hls-advanced-ad-insertion}

| Category | Content type | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
|Ad Insertion|VOD|Ad only|Not Supported|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Ad Insertion|VOD + Live|Targeting parameters|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Ad Insertion|VOD + Live|Custom ad policy|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Ad Insertion|VOD + Live|Lazy ad loading|![supported icon](assets/supported15.png)|Not Supported|Platform Limitation|
|Ad Insertion|VOD|Companion ads, Banner ads, and Clickable ads|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Ad Insertion|VOD|VPAID 2.0|SWF|JavaScript|JavaScript|

## HLS core ad insertion features (CSAI) {#hls-core-ad-insertion}

| Category | Content type | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
|Ad Insertion|VOD + Live|Pre-roll|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Ad Insertion|VOD + Live|Mid-roll|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Ad Insertion|VOD + Live|Post-roll|VOD only|VOD only|VOD only|
|Ad Insertion|FER VOD|Ad resolution and Behaviors|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Ad Insertion|VOD + Live|Default ad policy|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Ad Insertion|VOD + Live|VAST 2.0/3.0|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Ad Insertion|VOD + Live|VMAP 1.0|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Ad Insertion|VOD + Live|CRS v3.1|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|

## HLS content protection features {#hls-content-protection}

| Category | Content type | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
|Content Protection|VOD + Live|AES-128|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Content Protection|VOD + Live|Sample-AES|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Content Protection|VOD|DRM|Adobe Access|Not Supported|FairPlay|

## HLS advanced playback features {#hls-advanced-playback}

| Category | Content type | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
|Playback|VOD|Playback at offset|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Playback|VOD|Audio only playback|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Playback|VOD|Trick play|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Playback|VOD|Smooth trick play|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Playback|VOD + Live|ID3 parsing|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Not Supported|
|Playback|VOD + Live|Discontinuity marker support|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Playback|VOD + Live|Tokenized streams|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Playback|VOD + Live|Billing|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Playback|VOD + Live|Browserify|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|

## HLS core playback {#hls-core-playback}

| Category | Content type | Feature | Flash | HTML5: FF, IE, Chrome, Android Chrome | HTML5: Safari, iOS Safari |
|--- |--- |--- |--- |--- |--- |
|Playback|VOD + Live|General playback (Play, Pause, Seek)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Playback|FER VOD|General playback (Play, Pause, Seek)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Playback|VOD + Live|Adaptive bit rate|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Playback|VOD + Live|608/708 captions|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Playback|VOD + Live|WebVTT|![supported icon](assets/supported15.png)|VOD only|VOD only|
|Playback|VOD + Live|Manifest Failover|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|
|Playback|VOD + Live|Advanced Failover|![supported icon](assets/supported15.png)|VOD only|Platform Limitation|
|Playback|VOD + Live|QoS and player notifications|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Limited QoS support|
|Playback|VOD + Live|Support for cookie headers|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Playback|VOD + Live|Setting buffer control parameters|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Playback|VOD + Live|Set adaptive bit rate controls|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Playback|VOD + Live|Custom tags|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Playback|VOD + Live|Late-binding audio|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
|Playback|VOD + Live|302 redirect|![supported icon](assets/supported15.png)|![supported icon](assets/supported15.png)|Platform Limitation|
