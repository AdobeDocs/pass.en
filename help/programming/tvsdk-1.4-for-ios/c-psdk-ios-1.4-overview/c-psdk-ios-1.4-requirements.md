---
description: TVSDK requires specific properties for media content, manifest content, and software versions.
title: Requirements
exl-id: 2b81ae19-7907-4038-80e1-f579a8c04540
---
# Requirements {#requirements}

TVSDK requires specific properties for media content, manifest content, and software versions.

## System and software requirements {#section_61C32A0209C44230B392B113B85643EE}

To use TVSDK, ensure that your hardware, operating system, and application versions all meet the minimum requirements listed below. 

Operating system: iOS 6.0 or later

## Content and manifest requirements {#section_05FA02E2189742008DA09D87E66DCAB7}

Check the restrictions and requirements for streams and playlists (manifests), including DRM encryption keys. 

|  Content segment key frames  | Each content segment must begin with a key frame.  |
|---|---|
|  Sequence numbers in live/linear video  | Must match between all bit-rate renditions for the main content at any given time.  |

## #EXT-X-VERSION requirements {#section_C03D3DCE1D244E26BBD2C1D7144FDFBD}

The version of `#EXT-X-VERSION` in the [!DNL .m3u8] file affects what features are available to your application and what `EXT` tags are valid in your playlist/manifest.

Here is some information about the `#EXT-X-VERSION` tag, which specifies the HLS protocol version:

* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur.

  For more information, see [HTTP Live Streaming specification](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1). 
* If the tag is not included in the master or media playlists, or if no version is specified, version 1 is used by default. Content that does not comply with version 1 will not play. 
* Adobe recommends using at least version 2 for playback in TVSDK-based clients.

Clients and servers must implement the versions in the following way:  

<table id="table_62EB98EDD9DE49EC84CB1C7D59BC40E6"> 
 <thead> 
  <tr> 
   <th colname="1" class="entry"> Use at least this version </th> 
   <th colname="2" class="entry"> To use these features </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:2 </span> </td> 
   <td colname="2"> The IV attribute of the <span class="codeph"> EXT-X-KEY </span> tag. </td> 
  </tr> 
  <tr> 
   <td colname="1"> <span class="codeph"> EXT-X-VERSION:3 </span> </td> 
   <td colname="2"> 
    <ul id="ul_C9500D3F934848639C204BF248F139FF"> 
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Floating-point <span class="codeph"> EXTINF </span> duration values <p>The duration tags ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) in version 2 were rounded to integer values. Version 3 and above require durations to be exact in floating point. </p> </li> 
     <li id="li_8DF5E91F1D5D4E19894595E1FE0A5EDE"> TVSDK features such as ad insertion and seamless ABR </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_99E24D013E3141308B5A57446A9B8033"> 
      <li id="li_F36E65ADD2CA451C82FF18DBD5667927">The <span class="codeph"> EXT-X-BYTERANGE </span> tag </li> 
      <li id="li_8C653168A7B84D11AC233E7548A8D2EF">The <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> tag </li> 
      <li id="li_2922B34717CB4F6189068529CDBE6D10">The <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> tag </li> 
      <li id="li_D015D78E217641D7867EB509E9F9EEE2">The <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
      <li id="li_CA068EA381984F5497FE67617CA8BB34">The <span class="codeph"> AUDIO </span> and <span class="codeph"> VIDEO </span> attributes of the <span class="codeph"> EXT-X-STREAM-INF </span> tag </li> 
      <li id="li_EE78CC7D194A4EB2897F9AE8E4B081B8"> TVSDK alternate audio </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
