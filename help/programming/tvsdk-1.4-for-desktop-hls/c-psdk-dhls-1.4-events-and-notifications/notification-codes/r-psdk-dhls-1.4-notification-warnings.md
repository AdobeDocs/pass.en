---
description: This table proves detailed information about WARN. type notifications.
title: WARNING notification codes
exl-id: 3d76aba4-ace8-4a49-b930-96bbcad41f25
---
# WARNING notification codes{#warning-notification-codes}

This table proves detailed information about WARN. type notifications.

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

Most warnings contain relevant metadata, for example, the URL of the resource that failed to download. Some notifications contain metadata to specify whether the problem occurred in the main video content, in the alternate audio content, or in an ad. 

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Code </th> 
   <th colname="2" class="entry"> Name </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
   <th colname="4" class="entry"> Metadata Keys </th> 
   <th colname="5" class="entry"> Comments </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Playback</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 200000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_OPERATION _FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR </span><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION </span> </td> 
   <td colname="5"> <p>A playback-related operation has failed, but playback may continue. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Ad resolving </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_ RESOLVE_FAIL </span><span class="codeph"> RESOURCE_PLACEMENT_ FAILED </span><span class="codeph"> AD_RESOLVER_ METADATA_INVALID </span> </td> 
   <td colname="4"> <p>None </p> </td> 
   <td colname="5"> <p>The ad-resolver has failed to resolve/insert the ad content. Playback may continue. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Background manifests</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING</span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_ WARNING_ERROR</span> <span class="codeph"> BACKGROUND_MANIFEST_ WARNING_NAME</span> <span class="codeph"> DESCRIPTION</span> </td> 
   <td colname="5"> <p> Error in background manifest download. Any issue in updating the background manifest is dispatched as a TVSDK warning and does not cause the playback to stop. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_ WARNING</span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> DESCRIPTION</span> </td> 
   <td colname="5"> <p> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Native</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"><span class="codeph"> 209100 </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING </span> </td> 
   <td colname="3" morerows="1"> <p>None </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> NATIVE_ERROR_NAME </span><span class="codeph"> DESCRIPTION </span> </p> </td> 
   <td colname="5"> <p>The low-level AVE library issued an error. </p> <p>See <a href=../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md format="html" scope="external"> Details for the NATIVE_ERROR notifications</a> for detailed information about the values for these metadata fields. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_CODE</span> <span class="codeph"> DRM_ERROR_STRING</span> </p> </td> 
   <td colname="5">DRM minor error code and DRM server error string. See <a href=../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md format="html" scope="external"> Details for the NATIVE_ERROR notifications</a> for detailed information about the values for these metadata fields.
   </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Generic</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 299999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_WARNING </span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"> <p>None </p> </td> 
   <td colname="5"> <p>Marks a generic warning event. Not actually issued by TVSDK. It's just a marker for the end of the range of numerical codes corresponding to warning events. </p> </td> 
  </tr> 
 </tbody> 
</table>
