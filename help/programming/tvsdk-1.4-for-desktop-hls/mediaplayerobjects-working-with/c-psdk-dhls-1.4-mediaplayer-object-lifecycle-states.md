---
description: From the moment that you create the MediaPlayer instance to the moment when you terminate (reuse or remove) it, this instance completes a series of transitions between statuses.
title: MediaPlayer object lifecycle
exl-id: 0f2f3699-b745-4b14-8b7e-68696960ccab
---
# MediaPlayer object lifecycle{#mediaplayer-object-lifecycle}

From the moment that you create the MediaPlayer instance to the moment when you terminate (reuse or remove) it, this instance completes a series of transitions between statuses.

Some operations are permitted only when the player is in a particular state. For example, calling `play` in IDLE is not allowed. You can call this status only after the player reaches the PREPARED state.

To work with statuses:

* You can retrieve the current state of the `MediaPlayer` object by using the `MediaPlayer.status` property.

  ```
  function get status():String;
  ```

* The list of statuses is defined in `MediaPlayer.PlayerStatus`.

State-transition diagram for the lifecycle of a `MediaPlayer` instance: 
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-flash-1_2_web.png)

The following table provides additional details:  

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <span class="codeph"> MediaPlayerStatus </span> </th> 
   <th colname="col2" class="entry"> Occurs when </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> IDLE </span> </td> 
   <td colname="col2"> <p> Your application requested a new media player by instantiating <span class="codeph"> MediaPlayer </span>. The newly created player is waiting for you to specify a media player item. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INITIALIZING </span> </td> 
   <td colname="col2"> <p>Your application called <span class="codeph"> MediaPlayer.replaceCurrentResource </span>, and the media player is loading. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INITIALIZED </span> </td> 
   <td colname="col2"> <p>TVSDK successfully set the media player item. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARING </span> </td> 
   <td colname="col2"> <p>Your application called <span class="codeph"> MediaPlayer.prepareToPlay </span>. The media player is loading the media player item and the associated resources. </p> <p>Tip:  Some buffering of the main media might occur. </p> <p>TVSDK is preparing the media stream and attempting to perform ad resolving and ad insertion, (if enabled). </p> <p>Tip:  To set the start time to a non-zero value, call <span class="codeph"> prepareToPlay(startTime) </span> with the time in milleseconds. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARED </span> </td> 
   <td colname="col2"> <p>The content is prepared and ads have been inserted in the timeline, or the ad procedure failed. Buffering or playback can begin. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PLAYING </span> </td> 
   <td colname="col2"> <p>Your application has called <span class="codeph"> play </span>, so TVSDK is trying to play the video. Some buffering might occur before the video actually plays. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PAUSED </span> </td> 
   <td colname="col2"> <p>As your application plays and pauses the media, the media player moves between this state and PLAYING. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> SEEKING </span> </td> 
   <td colname="col2"> <p>The media player is seeking to the correct position while paused or playing. To determine when seeking has started or ended, listen for the <span class="codeph"> SeekEvent.SEEK_BEGIN </span> and <span class="codeph"> SeekEvent.SEEK_END </span> events. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> COMPLETED </span> </td> 
   <td colname="col2"> <p>The player reached the end of the stream, and playback has stopped. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> RELEASED </span> </td> 
   <td colname="col2"> <p>Your application has released the media player, which also releases any associated resources. You can no longer use this instance </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ERROR </span> </td> 
   <td colname="col2"> <p>An error occurred during the process. An error also might affect what your application can do next. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>You can use the status to provide feedback on the process (for example, a spinner while waiting for the next status change) or to take the next step in playing the media, such as waiting for the appropriate status before calling the next method.
