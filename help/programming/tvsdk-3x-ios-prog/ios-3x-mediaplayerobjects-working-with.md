---
description: The PTMediaPlayer object represents your media player. A PTMediaPlayerItem represents audio or video on your player.
title: Work with MediaPlayer objects
exl-id: 57dd455e-e78c-4e5b-80af-070ae7982864
---
# Work with MediaPlayer objects {#work-with-mediaplayer-objects}

The PTMediaPlayer object represents your media player. A PTMediaPlayerItem represents audio or video on your player.

## About the MediaPlayerItem class {#section_B6F36C0462644F5C932C8AA2F6827071}

After a media resource is successfully loaded, TVSDKcreates an instance of the `PTMediaPlayerItem` class to provide access to that resource.

The `PTMediaPlayer` resolves the media resource, loads the associated manifest file, and parses the manifest. This is the asynchronous part of the resource loading process. The `PTMediaPlayerItem` instance is produced after the resource has been resolved, and this instance is a resolved version of a media resource. TVSDK provides access to the newly created `PTMediaPlayerItem` instance through `PTMediaPlayer.currentItem`.

>[!TIP]
>
>You must wait for the resource to be successfully loaded before accessing the media player item.

## MediaPlayer object lifecycle {#section_D87EF7FBC7B442BDBE825156DC2C1CCF}

From the moment that you create the `PTMediaPlayer` instance to the moment when you terminate (reuse or remove) it, this instance completes a series of transitions from one status to another.

Some operations are permitted only when the player is in a particular state. For example, calling `play` in `PTMediaPlayerStatusCreated` is not allowed. You can call this status only after the player reaches the `PTMediaPlayerStatusReady` status.

To work with statuses:

* You can retrieve the current status of the MediaPlayer object with `PTMediaPlayer.status`. 
* The list of statuses is defined in `PTMediaPlayerStatus`.

State-transition diagram for the lifecycle of a MediaPlayer instance: 
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-ios2_web.png)

The following table provides additional details:  

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>PTMediaPlayerStatus</b></th> 
   <th colname="col2" class="entry"><b>Occurs when</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCreated</span> </p> </td> 
   <td colname="col2"> <p>Your application requested a new media player by calling <span class="codeph"> playerWithMediaPlayerItem</span>. The newly created player is waiting for you to specify a media player item. This is the media player's initial status. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusInitializing</span> </p> </td> 
   <td colname="col2"> <p>Your application calls <span class="codeph"> PTMediaPlayer.replaceCurrentItemWithPlayerItem</span>, and the media player is loading. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusInitialized</span> </p> </td> 
   <td colname="col2"> <p>TVSDK successfully set the media player item. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p> <span class="codeph"> PTMediaPlayerStatusReady</span> </p> </td> 
   <td colname="col2"> <p>The content is prepared and ads have been inserted in the timeline, or the ad procedure failed. Buffering or playback can begin. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPlaying</span> </p> </td> 
   <td colname="col2"> <p>Your application has called <span class="codeph"> play</span>, so TVSDK is trying to play the video. Some buffering might occur before the video actually plays. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusPaused</span> </p> </td> 
   <td colname="col2"> <p>As your application plays and pauses the media, the media player moves between this state and <span class="codeph"> PTMediaPlayerStatusPlaying</span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusCompleted</span> </p> </td> 
   <td colname="col2"> <p>The player reached the end of the stream, and playback has stopped. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusStopped</span> </p> </td> 
   <td colname="col2"> <p>Your application has released the media player, which also releases any associated resources. You can no longer use this instance </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p><span class="codeph"> PTMediaPlayerStatusError</span> </p> </td> 
   <td colname="col2"> <p>An error occurred during the process. An error also might affect what your application can do next. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>You can use the status to provide feedback on the process (for example, a spinner while waiting for the next status change) or to take the next step in playing the media, such as waiting for the appropriate status before calling the next method.
