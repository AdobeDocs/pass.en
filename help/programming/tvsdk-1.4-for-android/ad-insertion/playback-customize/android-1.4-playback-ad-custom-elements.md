---
description: TVSDK provides classes and methods you can use to customize the playback behavior of content that contains advertising.
title: API elements for ad playback
exl-id: a976a905-8aa2-4bdb-9e10-addb65a433ef
---
# API elements for ad playback {#api-elements-for-ad-playback}

TVSDK provides classes and methods you can use to customize the playback behavior of content that contains advertising.

The following API elements are useful for customizing playback:  

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> API element </th> 
   <th colname="col2" class="entry"> Content that supports advertising </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdvertisingMetadata</span> </td> 
   <td colname="col2">Control whether an ad break should be marked as having been watched by a viewer, and if yes, when to mark it. Set and get the watched policy using <span class="codeph"> setAdBreakAsWatched</span> and <span class="codeph"> getAdBreakAsWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumerates possible playback policies for ad breaks. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicy</span> </td> 
   <td colname="col2"> Enumerates possible playback policies for ads. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> Interface that allows customization of TVSDK ad behavior. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> Class that implements the default TVSDK behavior. Your application can override this class to customize the default behaviors without implementing the complete interface. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span>. <p>This is the local time of the playback, excluding the placed ad breaks. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>. <p>Here, the seek occurs relative to a local time in the stream. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>The virtual position on the timeline is converted to the local position. </p> </li> 
    </ul> <p>Important:  <span class="codeph"> getLocalTime</span> in <span class="codeph"> MediaPlayer</span> returns the current time relative to the original content, without dynamically spliced ads. <span class="codeph"> getLocalTime</span> in <span class="codeph"> AdBreak</span> returns the start time of the break relative to the original content. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> isWatched</span> property. Indicates whether the viewer has watched the ad. </td> 
  </tr> 
 </tbody> 
</table>
