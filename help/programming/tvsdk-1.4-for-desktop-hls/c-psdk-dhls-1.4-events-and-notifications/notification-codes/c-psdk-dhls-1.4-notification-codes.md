---
description: The TVSDK notification system produces various error, warning, and informational notices that provide diagnostic metadata.
title: Notification codes
exl-id: 7ea079f1-658d-45ab-891d-044b7b4ff4ec
---
# Overview {#notification-codes-overview}

The TVSDK notification system produces various error, warning, and informational notices that provide diagnostic metadata.

 Notification objects provide information related to the player's status. TVSDK provides a chronologically sorted list of notification objects, and each notification contains the following metadata: 

<table frame="all" colsep="1" rowsep="1" id="table_DBA8CACF02DB4AF2B053E560850B49CE"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Element </th> 
   <th colname="2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> type </td> 
   <td colname="2"> The notification type. Depending on the platform, this property refers to an enumerated type with possible values of INFO, WARN, or ERROR. This is the top-level grouping for notifications. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> code </td> 
   <td colname="2">The numerical representation assigned to the notification: 
    <ul id="ul_31AB497C6FFA452496DD09B0D78687B9"> 
     <li id="li_53E75022C50246E0982E315D04EFD8B3">Error notification events, from 100000 to 199999 </li> 
     <li id="li_11AE91D1325E4F718228E662C9C55F9A">Warning notification events, from 200000 to 299999 </li> 
     <li id="li_6D3EA03845294DC2BAD1ACF507639E51">Information notification events, from 300000 to 399999 </li> 
    </ul> <p>Each top-level range, such as errors, is divided into subranges, such as 101000 through 101999 representing playback errors. </p>
    <pre>
     The enumeration 
     <span class="codeph"> mediacore.PSDKErrorCode</span> lists the possible values.
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> name </td> 
   <td colname="2">A string that contains a human-readable description of the code, such as <span class="codeph"> SEEK_ERROR</span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> metadata </td> 
   <td colname="2">Key/value pairs that contain additional relevant information about the notification. For example, a key named <span class="codeph"> URL</span> would be paired with a value that is a URL related to the notification, such as an invalid URL that caused an error. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> innerNotification </td> 
   <td colname="2">A reference to another <span class="codeph"> MediaPlayerNotification</span> object that directly affected this notification. An example might be a notification about an ad-insertion failure that directly corresponds to a time-line insertion conflict. Not all notifications provide an inner notification. </td> 
  </tr> 
 </tbody> 
</table>
