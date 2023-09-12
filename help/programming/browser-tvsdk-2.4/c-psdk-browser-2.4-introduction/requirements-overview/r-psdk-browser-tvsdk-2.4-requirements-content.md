---
description: Check the restrictions and requirements for streams and playlists (manifests).
title: Content and manifest requirements
exl-id: 53fdd771-06ea-496f-9591-6ed4d5011f8d
---
# Content and manifest requirements{#content-and-manifest-requirements}

Check the restrictions and requirements for streams and playlists (manifests).

<table id="table_D7C38CD3B4D24C3D9A3B55D8CEFE7366"> 
 <tbody> 
  <tr> 
   <td colname="col1"> Content segment duration </td> 
   <td colname="col2"> The duration of a segment must not exceed the target duration that is specified in the manifest file. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Content requirement </td> 
   <td colname="col2"> Every TS segment should start with a key frame. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> HLS Content </td> 
   <td colname="col2"> <p>Remember the following: 
     <ul id="ul_B226605345EA46F69DA1380E16826117"> 
      <li id="li_6564DC0E879544BB8513DD2D1CFBA8DE">AAC-SSR audio is not supported. </li> 
      <li id="li_B73CAEBE4347406EA4DB25551B444BDA">Audio codecs AC3 and Enhanced AC3 are not supported. </li> 
      <li id="li_5986DD33C0FE485D99D4C00E2E6012CA">HLS streams with discontinuity, but no discontinuity markers are not supported. </li> 
      <li id="li_FED8686372DF4A39BAABC531BA4EB137">HLS Live does not support the time stamp rollover. </li> 
      <li id="li_565CFBEAD9874BA48F6E25B0893BF131">Ads in the DVR window of HLS Live streams are not resolved. </li> 
      <li id="li_7D22EA32C94240D79EDDA96D9E72FE8F">Byte range is not supported with AES-128 encrypted content. </li> 
     </ul></p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> DASH content </td> 
   <td colname="col2"> <p>Remember the following: 
     <ul id="ul_9D33C2418F9F49DEAE0E642301726F89"> 
      <li id="li_74C69A21A7BD4831B92F0D57900E1CB1">For Live streams - The live profile with dynamic type is supported. </li> 
      <li id="li_0C8743DB152047819D23C9F180998AD7">For VOD streams - The live profile with static type is supported. </li> 
      <li id="li_FBC6828663FB413798A4BDAF0B9831AA">For VOD streams - The on-demand profile is not certified for ad workflows. </li> 
      <li id="li_4393B9B1F6144BDEAE484C879750ED23">Playback of DASH streams with multiple periods is not supported. </li> 
      <li id="li_6A2CEC4E974C4D44A45F5503A1A9D8D0">Embedded Captions (608/708), signaled via the Accessibility tag, are supported. </li> 
      <li id="li_EDE93DF4F3A64A53BA80877F701A8F0D">Fragmented/Segmented VTT files are not supported. </li> 
      <li id="li_8897F73611194030A490A4FF1178364C">Streams with inband custom tags are not certified. </li> 
     </ul></p> </td> 
  </tr> 
 </tbody> 
</table>
