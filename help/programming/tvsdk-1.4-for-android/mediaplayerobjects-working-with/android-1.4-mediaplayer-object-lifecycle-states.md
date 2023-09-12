---
description: From the moment that you create the MediaPlayer instance to the moment when you terminate (reuse or remove) it, this instance completes a series of transitions between states.
title: MediaPlayer object lifecycle
exl-id: efb39fea-1050-41e5-93d8-1175a54f81e5
---
# MediaPlayer object lifecycle{#mediaplayer-object-lifecycle}

From the moment that you create the MediaPlayer instance to the moment when you terminate (reuse or remove) it, this instance completes a series of transitions between states.

Some operations are permitted only when the player is in a particular state. For example, calling `play` in `IDLE` is not allowed. You can call this status only after the player reaches the `PREPARED` state.

To work with states:

* You can retrieve the current state of the `MediaPlayer` object with `MediaPlayer.getStatus`.

  ```java
  PlayerState getStatus() throws IllegalStateException;
  ```

* The list of states is defined in `MediaPlayer.PlayerState`.

State-transition diagram for the lifecycle of a `MediaPlayer` instance: 
<!--<a id="fig_1C55DE3F186F4B36AFFDCDE90379534C"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

The following table provides additional details:  

<table id="table_426F0093E4214EA88CD72A7796B58DFD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> MediaPlayer.PlayerState </th> 
   <th colname="col2" class="entry"> Occurs when </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> IDLE </span> </td> 
   <td colname="col2"> <p>Your application requested a new media player by calling <span class="codeph"> DefaultMediaPlayer.create </span>. The newly created player is waiting for you to specify a media player item. This is the media player's initial state. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INITIALIZING </span> </td> 
   <td colname="col2"> <p>Your application called <span class="codeph"> MediaPlayer.replaceCurrentItem </span>, and the media player is loading. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> INITIALIZED </span> </td> 
   <td colname="col2"> <p>TVSDK successfully set the media player item. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> PREPARING </span> </td> 
   <td colname="col2"> <p>Your application called <span class="codeph"> MediaPlayer.prepareToPlay </span>. The media player is loading the media player item and the associated resources. </p> <p>Tip:  Some buffering of the main media might occur. </p> <p>TVSDK is preparing the media stream and attempting to perform ad resolving and ad insertion, (if enabled). </p> <p>Tip:  To set the start time to a non-zero value, call <span class="codeph"> prepareToPlay(startTime) </span> with the time in milliseconds. </p> </td> 
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
   <td colname="col1"> <span class="codeph"> SUSPENDED </span> </td> 
   <td colname="col2"> <p>Your application navigated away from the playback, shut down the device, or switched applications while the player was playing or paused. The media player has been suspended and resources have been released. To continue, restore the media player. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> COMPLETE </span> </td> 
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
>You can use the state to provide feedback on the process (for example, a spinner while waiting for the next state change) or to take the next step in playing the media, such as waiting for the appropriate state before calling the next method.

For example: 

```java
@Override 
public void onStateChanged(MediaPlayer.PlayerState state,  
                           MediaPlayerNotification notification) { 
   switch (state) { 
      // It is recommended that you call prepareToPlay() after receiving  
      // the INITIALIZED state. 
      case INITIALIZED: 
         _mediaPlayer.prepareToPlay(); 
         break; 
      case PREPARING: 
         showBufferingSpinner(); 
         break; 
      case PREPARED: 
         hideBufferingSpinner(); 
      ..... 
    } 
}
```
