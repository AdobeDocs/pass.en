---
description: The status of the media player determines which actions are legal.
title: Lifecycle and statuses of the MediaPlayer object
exl-id: 6b43f334-bd21-4d0e-a123-fd99403a6082
---
# Lifecycle and statuses of the MediaPlayer object {#lifecycle-and-statuses-of-the-mediaplayer-object}

The status of the media player determines which actions are legal.

For working with media player statuses:

* You can retrieve the current status of the `MediaPlayer` object with `MediaPlayer.getStatus()`. 

* The list of statuses is defined in the [MediaPlayerStatus](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.7/com/adobe/mediacore/MediaPlayerStatus.html) enum.

Status-transition diagram for the lifecycle of a `MediaPlayer` instance: 
<!--<a id="fig_A6425F24C7734DC681D992859D2A6743"></a>-->

![](assets/media_player_statuses.png)

The following table provides details about the lifecycle and statuses of the media player:  

<table id="table_82757A0043EB4AACA474E6B30326A6B7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Status </th> 
   <th colname="col2" class="entry"> Occurs when </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> IDLE </td> 
   <td colname="col2"> <p>The media player's initial status. The player is created and is waiting for you to specify a media player item. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INITIALIZING </td> 
   <td colname="col2"> <p>Your application calls <span class="codeph"> MediaPlayer.replaceCurrentItem() </span>. </p> <p>The media player item is loading. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> INITIALIZED </td> 
   <td colname="col2"> <p>TVSDK successfully set the media-player item. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARING </td> 
   <td colname="col2"> <p>Your application calls <span class="codeph"> MediaPlayer.prepareToPlay() </span>. The media player is loading the media player item and any associated resources. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PREPARED </td> 
   <td colname="col2"> <p>TVSDK has prepared the media stream and has attempted to perform ad resolving and ad insertion (if enabled). The content is prepared and ads have been inserted in the timeline, or the the ad procedure failed. </p> <p>Buffering or playback can begin. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> PLAYING/PAUSED </td> 
   <td colname="col2"> <p>As the application plays and pauses the media, the media player moves between these statuses. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> SUSPENDED </td> 
   <td colname="col2"> <p>If the application navigates away from the playback, shuts down the device, or switches applications while the player is playing or paused, the media player is suspended and resources are released. </p> <p>Calling <span class="codeph"> MediaPlayer.restore() </span> returns the player to the status the player was in before it was SUSPENDED. The exception is if the player is SEEKING when suspended is called, the player is PAUSED and then SUSPENDED. </p> <p>Important:  <p>Remember the following information: 
      <ul id="ul_1B21668994D1474AAA0BE839E0D69B00"> 
       <li id="li_08459A3AB03C45588D73FA162C27A56C">The <span class="codeph"> MediaPlayer </span> automatically calls <span class="codeph"> suspend </span> only when the surface object that is used by the <span class="codeph"> MediaPlayerView </span> is destroyed. </li> 
       <li id="li_B9926AA2E7B9441490F37D24AE2678A1">The <span class="codeph"> MediaPlayer </span> automatically calls <span class="codeph"> restore() </span> only when a new surface object that is used by the <span class="codeph"> MediaPlayerView </span> is created. </li> 
      </ul> </p> </p> <p>If you always want playback to be paused when the MediaPlayer is restored, have your application call <span class="codeph"> MediaPlayer.pause() </span> in the Android Activity's <span class="codeph"> onPause() </span> method. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> COMPLETE </td> 
   <td colname="col2"> <p>The player has reached the end of the stream, and playback has stopped. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> RELEASED </td> 
   <td colname="col2"> <p>Your application released the media player, which also releases any associated resources. You can no longer use this instance. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> ERROR </td> 
   <td colname="col2"> <p>An error occurred during the process. An error also might affect what the application can do next. For more information, see <a href="../../../tvsdk-2.7-for-android/content-playback-options/t-psdk-android-2.7-error-handling-set-up.md#set-up-error-handling" format="dita" scope="local"> Set up error handling </a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!TIP]
>
>You can use the status to provide feedback on the process, or example, a spinner while waiting for the next status change, or take the next steps in playing the media, such as waiting for the appropriate status before calling the next method.

For example: 

```java
mediaPlayer.addEventListener(MediaPlayerEvent STATUS_CHANGED, new StatusChangeEventListener() { 
    @Override  
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        switch(event.getStatus()) { 
            case INITIALIZED: 
                mediaPlayer.prepareToPlay(); 
                break; 
            case PREPARING: 
                showBufferingSpinner(); 
                break; 
            case PREPARED: 
                hideBufferingSpinner(); 
                mediaPlayer.play(); 
                break; 
            ...                
        } 
        ... 
    } 
}); 

```
