---
description: The version of EXT-X-VERSION in the .m3u8 file affects what features are available to your application and what EXT tags are valid in your playlist/manifest.
title: EXT-X-VERSION requirements
exl-id: ee778fe1-d050-4c90-af8d-6600fff72e52
---
# EXT-X-VERSION requirements{#ext-x-version-requirements}

The version of #EXT-X-VERSION in the .m3u8 file affects what features are available to your application and what EXT tags are valid in your playlist/manifest.

<!--<a id="section_8850183988124049A001758F117AD3A6"></a>-->

Here is some information about the `#EXT-X-VERSION` tag, which specifies the HLS protocol version:

* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur.

  For more information, see [HTTP Live Streaming specification](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1). 
* The version must match the features and attributes in the HLS playlist; otherwise, playback errors might occur.

  For more information, see [HTTP Live Streaming specification](https://datatracker.ietf.org/doc/draft-pantos-http-live-streaming/?include_text=1). 
* Adobe recommends using at least version 2 for playback in -based clients.

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
     <li id="li_535A7E3FABCB46FE872A7EA5DE2A1784">Floating-point <span class="codeph"> EXTINF </span> duration values <p>The duration tags ( <span class="codeph"> #EXTINF: </span>&lt;duration&gt;,&lt;title&gt;) in version 2 were rounded to integer values. Version 3 and above require durations to be exact in floating point. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <p> <span class="codeph"> EXT-X-VERSION:4 </span> </p> </td> 
   <td colname="2"> <p> 
     <ul id="ul_83D61E909D0C413FBDAB7A4A0BE1F03C"> 
      <li id="li_5071F2BE2DB74BBFB1F23B3B30C5CFD6">The <span class="codeph"> EXT-X-BYTERANGE </span> tag </li> 
      <li id="li_A093F448567D475AB44656D4600BCBD6">The <span class="codeph"> EXT-X-I-FRAME-STREAM-INF </span> tag </li> 
      <li id="li_1084AE3B10FD4EB387D25EEDDFBBC8CD">The <span class="codeph"> EXT-X-I-FRAMES-ONLY </span> tag </li> 
      <li id="li_4FEFA36E300C403DBB77BB4DA46DB4EB">The <span class="codeph"> EXT-X-MEDIA </span> tag </li> 
      <li id="li_E53D81AED45C47AEA346FA3A1B191E5C">The <span class="codeph"> AUDIO </span> and <span class="codeph"> VIDEO </span> attributes of the <span class="codeph"> EXT-X-STREAM-INF </span> tag </li> 
      <li id="li_2E99A4971B8046F3845CF3D4D363CCCF">TVSDK alternate audio </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
