---
description: The TVSDK notification system produces various error, warning, and informational notices that provide diagnostic metadata.
title: Notification codes
exl-id: 7bf016c6-8651-413b-a478-ac2d24f9453c
---
# Overview {#notification-codes-overview}

The TVSDK notification system produces various error, warning, and informational notices that provide diagnostic metadata.

 Notification objects provide information that is related to the player's status. TVSDK provides a chronologically sorted list of notification objects. Each notification contains the following metadata: 

<table frame="all" colsep="1" rowsep="1" id="table_1A32EFFE1834438D8261886EC9D7250D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Element </th> 
   <th colname="2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> type</span> </td> 
   <td colname="2"> <p>The notification type. </p> <p>Depending on the platform, this property is an enumerated type with possible values of INFO, WARN, and ERROR. This is the top-level grouping for notifications. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> code</span> </td> 
   <td colname="2"> <p>The following numerical representations are assigned to the notifications: 
     <ul id="ul_A86BF89D6B3B410E81FAD718D3C4A9F0"> 
      <li id="li_8180972D704C40098723734DD4B45643">Error notification events, from 100000 to 199999 </li> 
      <li id="li_0EC29EA5F0034E5EBFEF8E68A6498D39">Warning notification events, from 200000 to 299999 </li> 
      <li id="li_189A53D3D7EF4960A521AB04D00DCF70">Information notification events, from 300000 to 399999 </li> 
     </ul> </p> <p>Each top-level range, such as errors, is divided into subranges, such as 101000 through 101999 representing playback errors. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> name</span> </td> 
   <td colname="2">A string that contains a human-readable description of the notification event, such as <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> metadata</span> </td> 
   <td colname="2"> <p>Key/value pairs that contain additional relevant information about the notification. </p> <p>For example, a key named <span class="codeph"> URL</span> would provide a value that is a URL related to the notification, such as an invalid URL that caused an error. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> innerNotification</span> </td> 
   <td colname="2"> <p>A reference to another <span class="codeph"> MediaPlayerNotification</span> object that directly impacted this notification. </p> <p>An example might be a notification about an ad-insertion failure that directly corresponds to a time-line insertion conflict. Not all notifications provide an inner notification. </p> </td> 
  </tr> 
 </tbody> 
</table>
