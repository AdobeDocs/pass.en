---
description: The methods in the MediaPlayerItem class allow you to obtain information about the content stream that is represented by a loaded MediaResource.
title: MediaPlayer attributes to access MediaResource information
exl-id: 183a2992-06f2-4b1d-84c3-a6c2a7223e32
---
# MediaPlayer attributes to access MediaResource information{#mediaplayer-attributes-to-access-mediaresource-information}

The methods in the MediaPlayerItem class allow you to obtain information about the content stream that is represented by a loaded MediaResource.

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Purpose </th> 
   <th colname="2" class="entry"> Attribute </th> 
   <th colname="3" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Live stream </td> 
   <td colname="2"> <span class="codeph"> live </span> </td> 
   <td colname="3"> True if the stream is live; false if it is VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Closed captions </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions </span> </td> 
   <td colname="3"> True if closed-caption tracks are available. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks </span> </td> 
   <td colname="3"> Provides a list of available closed-caption tracks. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedClosedCaptionsTrack </span> </td> 
   <td colname="3"> Retrieves the closed caption track that was selected with <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Alternate audio </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio </span> </td> 
   <td colname="3"> <p>True if the stream has alternate audio tracks. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks </span> </td> 
   <td colname="3"> Provides a list of available alternate audio tracks. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectedAudioTrack </span> </td> 
   <td colname="3"> 
    <pre>
      Retrieves the currently selected audio track that were selected with 
     <span class="codeph"> selectAudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Timed metadata </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata </span> </td> 
   <td colname="3"> True if the stream has associated timed metadata. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata </span> </td> 
   <td colname="3"> Provides a list of the timed metadata objects that are associated with the stream. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Multiple profiles (bit rates) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> profiles </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> Provides a list of the associated bit rate profiles that are associated with this stream. <p>Note:  You can retrieve the bit rate for each profile and the height and width of the profile. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Media resource </td> 
   <td colname="2"> <span class="codeph"> resource </span> </td> 
   <td colname="3"> Returns the media resource that is associated with this item. </td> 
  </tr> 
 </tbody> 
</table>
