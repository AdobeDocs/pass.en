---
description: A MediaPlayer object encapsulates the behavior and functionality of a media player.
title: Set up the MediaPlayer
exl-id: f492b2bb-3280-4306-ac4b-8b8d0fd68409
---
# Set up the MediaPlayer{#set-up-the-mediaplayer}

A MediaPlayer object encapsulates the behavior and functionality of a media player.

1. Instantiate a `MediaPlayer` using the following:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Create a `MediaPlayerView` instance:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   where `container` is the target `div` element that contains your `HTMLMediaElement`.

   For example, on an HTML page: 

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   Call: 

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. Attach your `MediaPlayerView` instance to your `MediaPlayer` instance:

   ```js
   player.view = view;
   ```

1. Attach the custom controls `div` element to your MediaPlayer instance.

   For example, in HTML: 

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   Call: 

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

The `MediaPlayer` instance is now available and properly configured to display video content on the device screen.
