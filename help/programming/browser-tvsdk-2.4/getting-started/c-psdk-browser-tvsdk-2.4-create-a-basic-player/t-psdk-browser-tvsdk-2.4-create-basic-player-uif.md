---
title: Create a basic player using the UI Framework
description: Create a basic player using the UI Framework
copied-description: yes
exl-id: 78629042-fd87-406b-af42-229e34d48162
---
# Create a basic player using the UI Framework{#create-a-basic-player-using-the-ui-framework}

To create a basic player using the UI Framework: 

1. Create a `<div>` for your player instance.

   For example: 

   ```
   <div id="video1" > 
    </div>
   ```

1. Load the player.

   ```js
   <script> 
       (function(){ 
           var player = ptp.videoPlayer('#video1'); 
       })(); 
   </script>
   ```

   When the player is created, the specified `<div>` element is given a CSS class of `ptp-main-video-div-style`. The resulting DOM appears something like this: 

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <video class="vp-video-element"></video> 
   </div>
   ```

1. Add a UI control.

   For example, add a control bar that appears when the mouse hovers over the player: 

   ```js
   <script> 
       (function(){ 
           function myControlBarBehavior(element, configuration, player) { 
               return ptp.controlBarBehavior(element, configuration, player); 
           } 
           var player = ptp.videoPlayer('#video1', { 
               controlBar: { 
                   behavior: myControlBarBehavior, 
                   classNames: 'ptp-control-bar my_control_bar' 
               } 
           }); 
       })(); 
   </script>
   ```

   The resulting DOM appears as follows: 

   ```
   <div id="video1" class="ptp-main-video-div-style"> 
       <div class="ptp-control-bar my_control_bar"></div> 
       <video class="vp-video-element"></video> 
   </div>
   ```

The object returned from calling `ptp.videoPlayer()` provides a behavior that wraps the TVSDK media player API and allows for programmatic control of playback. When you make calls on the media player instance the user interface updates itself based on events fired by the media player: 

```js
<script> 
    (function(){ 
        var player = ptp.videoPlayer('#video1'); 
        player.loadResource( 'sample.mp4' ); 
    })(); 
</script>
```
