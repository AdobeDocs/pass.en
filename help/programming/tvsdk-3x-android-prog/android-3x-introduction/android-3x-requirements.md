---
description: TVSDK has specific requirements for media content, manifest content, DRM, and software versions.
title: Requirements
exl-id: 85bf7b85-5f4b-4ed5-aa4f-765dabc5d4d8
---
# Requirements {#requirements}

TVSDK has specific requirements for media content, manifest content, DRM, and software versions.

## System and software requirements {#section_96E5B079900246E78682AE44D3F23068}

To use TVSDK, ensure that your hardware, operating system, and application versions all meet the minimum requirements listed below.

|  Operating system  | Android 4.0 or later (minimum API level 14)  |
|---|---|
|  CPU  | 1 GHz Single Core or equivalent  |
|  RAM  | 256 MB  |
|  GPU  | Hardware GPU required for playback  |
|  Architecture  | x86 via Houdini, ARM64, ARMv7, and ARMv8  |

## Content and manifest requirements {#section_72DD0E4DA9774DCCADB42887497F1386}

Check the restrictions and requirements for streams and playlists (manifests), including DRM encryption keys. 

|  Adobe Access DRM  | If the DRM-protected stream is multiple bit rate (MBR), the DRM encryption key used for the MBR should be the same as the key used in all the bit-rate streams.  |
|---|---|
|  Ad variant manifests  | Must have the same bit-rate renditions as the renditions of the main content.  |

## #EXT-X-VERSION requirements {#section_49A33664651A46EC9ED888BA9C1C3F6D}

The version of `#EXT-X-VERSION` in the [!DNL .m3u8] manifest file affects which features are available to your application and which `EXT` tags are valid.

Here is some information about the `#EXT-X-VERSION` tag, which specifies the HLS protocol version:

* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur. For more information, see [HTTP Live Streaming specification](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1). 
* Adobe recommends using at least Version 2 of HLS for playback in TVSDK-based clients.

  Clients and servers must implement the versions in the following way:  

<table frame="all" colsep="1" rowsep="1" id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Use at least this version </th> 
   <th colname="2" class="entry"> To use these features </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> The IV attribute of the <span class="codeph"> EXT-X-KEY </span> tag. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Floating-point <span class="codeph"> EXTINF </span> duration values <p>The duration tags ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) in version 2 were rounded to integer values. Version 3 and above require durations to be specified exactly, in floating point. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:4 </span> </td> 
   <td colname="2"> 
    <ul id="ul_3355A6CBBE2141DDB92660BB4B604D70"> 
     <li id="li_5E73D41AF6DC4CEE88D6C029FFCFC350">The <span class="codeph"> EXT-X-BYTERANGE </span> tag </li> 
     <li id="li_BF5141F516F749E5890860D487EB5287">The <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> tag </li> 
     <li id="li_E0D399A13812499B94107CDE62998EE9">The <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> tag </li> 
     <li id="li_A7783AFF99854EFBBAECD2967E4CBF2B">The <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
     <li id="li_15AE652F33C1454AA90DDC65E7D6C2FD">The <span class="codeph"> AUDIO </span> and <span class="codeph"> VIDEO </span> attributes of the <span class="codeph"> EXT-X-STREAM-INF </span> tag </li> 
     <li id="li_DB2A7847D5884F6E91FD9E78101FBCA5">TVSDK alternate audio </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
