---
description: This table provides detailed information about INFO type notifications.
title: INFO notification codes
exl-id: c3703871-26cd-4f83-9a01-0993c6ef3d6b
---
# INFO notification codes {#info-notification-codes}

This table provides detailed information about INFO type notifications.

Most informational notifications contain relevant metadata, for example, the URL of the resource that failed to download. Some notifications contain metadata to specify whether the problem occurred in the main video content, in the alternate audio content, or in an ad. 

<table frame="all" colsep="1" rowsep="1" id="table_503463046E764A87B10EB5D8B294EB23"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>Code</b></th> 
   <th colname="2" class="entry"><b>Name</b></th> 
   <th colname="3" class="entry"><b>Inner Notification</b></th> 
   <th colname="4" class="entry"><b>Metadata Keys</b></th> 
   <th colname="5" class="entry"><b>Comments</b></th> 
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
   <td colname="1"><span class="codeph"> 300000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_START </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"> None </td> 
   <td colname="5"> Playback has started. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300001 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_COMPLETE </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"> None </td> 
   <td colname="5"> Playback has completed. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300002 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_START </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"> <p> None </p> </td> 
   <td colname="5"> A seek operation was initiated. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300003 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_COMPLETE </span> </td> 
   <td colname="3"> None </td> 
   <td colname="4"> <p>None </p> </td> 
   <td colname="5"> A seek operation completed. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 300005 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYER_STATE_CHANGE </span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"> <p>None </p> </td> 
   <td colname="5"> The player state has changed. When state is ERROR, the inner notification is the error notification object that triggered the switch to the ERROR state. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Adaptive bit rates (ABR)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 302000 </span> </td> 
   <td colname="2"><span class="codeph"> BITRATE_CHANGE </span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"><span class="codeph"> BITRATE </span> </td> 
   <td colname="5"> The bit rate of the video changed. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Late-binding audio (LBA)</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 304000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"> <p>None </p> </td> 
   <td colname="5"> <p>The audio track has changed. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Subtitles</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 307000 </span> </td> 
   <td colname="2"><span class="codeph"> SUBTITLES_TRACK_CHANGE </span> </td> 
   <td colname="3"> <p>None </p> </td> 
   <td colname="4"> <p>None </p> </td> 
   <td colname="5"> <p>The subtitles track changed. </p> </td> 
  </tr> 
 </tbody> 
</table>
