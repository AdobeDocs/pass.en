---
description: You can implement a control bar with DVR support for VOD and live streaming. DVR support includes the concept of a seekable window and the client live point.
title: Construct a control bar enhanced for DVR
exl-id: 8e70f03c-880a-48c5-8728-a4b967c19925
---
# Construct a control bar enhanced for DVR{#construct-a-control-bar-enhanced-for-dvr}

You can implement a control bar with DVR support for VOD and live streaming. DVR support includes the concept of a seekable window and the client live point.

* For VOD, the length of the seekable window is the duration of the entire asset. 
* For live streaming, the length of the DVR (seekable) window is defined as the time range starting at the live playback window and ending at the client live point.

  The client live point is calculated by subtracting the buffered length from the live window end. The target duration is a value bigger than or equal to the maximum duration of a fragment in the manifest.

  The default value is 10000 ms.

  The control bar for live playback supports DVR by first positioning the thumb at the client live point when starting playback and by displaying a region that marks the area where seek is not allowed.

<!--<a id="fig_37A39A28BA714BA5A2C461357ED5BD41"></a>-->

![](assets/dvr-window.PNG){width="684"}

1. To implement a control bar with DVR support, follow the steps for displaying a seek scrub bar, with a few minor differences:

    * You can choose to implement a control bar that is mapped only for the seekable range instead of for the playback range. Any user interaction for seek can be considered safe in the seekable range. 
    * You can choose to implement a control bar that is mapped for the playback range but that also displays the seekable range.

       For a control bar:

    1. Add an overlay to the control bar that represents the playback range. 
    1. When the user starts to seek, check whether the desired seek position is within the seekable range using the `MediaPlayer.seekableRange` property.

       For example:     
    
       ```    
       var desiredPosition:Number = // TODO : choose a value 
        
       private function onStatusChange(event:MediaPlayerStatusChangeEvent):void { 
           switch(event.status) { 
               case MediaPlayerStatus.PREPARED: 
                   _mediaPlayer.prepareToPlay(desiredPosition); 
           } 
       }
       ```

       You can also choose to seek to the client live point using the `MediaPlayer.LIVE_POINT` constant.     
    
       ```    
       private function onSeekToLiveClick(event:MouseEvent):void { 
           _player.seek(DefaultMediaPlayer.LIVE_POINT); 
       }
       ```
