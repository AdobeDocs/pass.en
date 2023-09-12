---
title: Details for the NATIVE_ERROR notification
description: Details for the NATIVE_ERROR notification
copied-description: yes
exl-id: 3819b932-47a2-4adb-830b-0a95a5fec70b
---
# Details for the NATIVE_ERROR notification {#details-for-the-native-error-notification}

When TVSDK handles a native error, it sets some or all of the following metadata key values.  

<table id="table_86A21619515B435DBB65DC4DFBB64B29"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Metadata key name </th> 
   <th colname="col2" class="entry"> Metadata value </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="col2"> 
    <pre>
      Native error code from the AVE. 
    </pre> These codes represent the following: 
    <ul id="ul_330C626DE27B45A09E8851CC24768A07"> 
     <li id="li_0845A9BBB55545BDB49BD4F4802C0E54">DRM errors (codes 3300 to 3367). These are the same as the equivalent Flash Player error codes. </li> 
     <li id="li_98A571480C154CF0AE1DC101FF0834C4">Video playback errors (-1 to 89). </li> 
     <li id="li_D7C19955DEF94DA88B822C8C57D6D2F4">Cryptography errors (300 to 307). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_ERROR_NAME </span> </td> 
   <td colname="col2"> A string that contains the error's name; for example, <span class="codeph"> AAXS_InvalidVoucher </span> or <span class="codeph"> DECODER_FAILED </span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> NATIVE_SUBERROR_CODE </span> </td> 
   <td colname="col2"> For DRM errors, suberror codes are also returned. These codes correspond to the <span class="codeph"> DRMErrorEvents </span> suberror code that is returned by the Flash Player. When reporting errors to Adobe, include this numeric value for troubleshooting assistance. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DRM_ERROR_STRING </span> </td> 
   <td colname="col2"> For DRM, this is your custom error string from your DRM server deployment, if you defined any. Also include this when reporting errors to Adobe. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="col2"> String description of the error. Usually the URL of the media. </td> 
  </tr> 
 </tbody> 
</table>

TVSDK receives these error codes and strings from the video engine.

>[!IMPORTANT]
>
>For a complete list of Adobe Primetime DRM client error codes, see [DRM Client Error Message Reference](https://helpx.adobe.com/content/dam/help/en/primetime/drm/drm_client_error_message_reference.pdf).
