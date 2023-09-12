---
description: The behavior of media playback is affected by seeking, pausing, and the inclusion of advertising.
title: Default and customized playback behavior with ads
exl-id: f4b2f317-c580-45a9-ad79-0cfa6c21848b
---
# Default and customized playback behavior with ads {#default-and-customized-playback-behavior-with-ads}

The behavior of media playback is affected by seeking, pausing, and the inclusion of advertising.

To override the default behavior, use `PTAdPolicySelector`.

>[!IMPORTANT]
>
>For VOD and live/linear streaming, timeline adjustments cannot be revised. This means that an advertisement cannot be removed from the timeline after it has played. If the user seeks back, the same ad plays again even if the normal policy would have been to remove it.

>[!IMPORTANT]
>
>TVSDK does not provide a way to disable seeking during ads. Adobe recommends that you configure your application to disable seeking during ads.

The following table describes how TVSDK handles ads and ad breaks during playback: 

<table id="table_466538B1C2A646B89EB4F9AA111203BE"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Video activity</b></th> 
   <th colname="col2" class="entry"><b>Default TVSDK behavior policy</b></th> 
   <th colname="col3" class="entry"><b>Customization available through PTAdPolicySelector</b></th>
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> During normal play, an ad break is encountered. </td> 
   <td colname="col2"></td> 
   <td colname="col3">Specify a different policy for the ad break by using <span class="codeph"> selectPolicyForAdBreak</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Your application seeks forward over ad break(s) into main content. </td> 
   <td colname="col2"> Plays the last unwatched ad break that was skipped over and resumes playback at the desired seek position when the break(s) playback is complete. </td> 
   <td colname="col3">Select which skipped break to play by using <span class="codeph"> selectAdBreaksToPlay</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Your application seeks backward over ad break(s) into main content. </td> 
   <td colname="col2"> Skips to the desired seek position without playing ad breaks. </td> 
   <td colname="col3">Select which skipped break to play by using <span class="codeph"> selectAdBreaksToPlay</span>.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Your application seeks forward into an ad break. </td> 
   <td colname="col2"> Plays from the beginning of the ad in which the seek ended. </td> 
   <td colname="col3">Specify a different ad policy for the ad break and for the specific ad where the seek ended by using <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Your application seeks backward into an ad break. </td> 
   <td colname="col2"> Plays from the beginning of the ad in which the seek ended. </td> 
   <td colname="col3">Specify a different ad policy for the ad break and for the specific ad in which the seek ended by using <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Your application seeks forward or backward over watched ad break(s) into main content. </td> 
   <td colname="col2"> If the last ad break skipped has already been watched, skips to the user-selected seek position. </td> 
   <td colname="col3">Select which of the skipped breaks to play using <span class="codeph"> selectAdBreaksToPlay</span> and determine which breaks have already been watched by using <span class="codeph"> PTAdBreak.isWatched</span>. <p> <p>Important:  By default, TVSDK marks an ad break as watched immediately after entering the first ad in the ad break. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Your application seeks forward or backward over one or more ad breaks and drops into a watched ad break. </td> 
   <td colname="col2"> Skips the ad break and seeks to the position immediately following the ad break. </td> 
   <td colname="col3">Specify a different ad policy for the ad break (with the watched status set to true) and for the specific ad where the seek ended by using <span class="codeph"> selectPolicyForSeekIntoAd</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Your application seeks forward over ads that were inserted using custom ad markers. </td> 
   <td colname="col2"> Skips to the user-selected seek position. </td> 
   <td colname="col3"></td> 
  </tr> 
 </tbody> 
</table>
