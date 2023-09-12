---
description: Complete the following steps to create a basic player using the Browser TVSDK.
title: Create a basic player using TVSDK
exl-id: ea7485e0-5d15-469b-b8b6-f9604d283492
---
# Create a basic player using TVSDK{#create-a-basic-player-using-tvsdk}

Complete the following steps to create a basic player using the Browser TVSDK.

1. Create a new directory in which you can download the compressed files for Browser TVSDK.
1. Download Browser TVSDK from Zendesk, decompress the files, and place the frameworks folder in the new directory.
1. Create a simple HTML boilerplate for the code with a `div` in it.
1. Place this boilerplate in an HTML file in the directory you created in step 1.

   ```
   <!DOCTYPE html> 
    
   <html lang="en"> 
   <head> 
   </head> 
   <body> 
         <div id="videoDiv" width="200" height="200"> 
        <div id="video-controls"></div> 
         </div> 
   </body> 
   </html>
   ```

1. Add the Browser TVSDK libraries in the head section.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. For the body tag, add the `onLoad` section.

   ```
   <body onload="startVideo()">
   ```

1. Start implementing the `startVideo` function.
1. Add a script tag and create the `startVideo` function in the tag.

   This is supposed to be in the head section of the page.

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. Create the `Adobe.MediaPlayer`.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Create the `MediaPlayerView`.

   >[!TIP]
   >
   >This is where the `div` that you created earlier is used.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. Add the player event listener.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implement the event handler and put this before the add event listener.

   ```js
   var onStatusChange = function (event) { 
    console.log(event.status); 
    
    switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.IDLE: 
      console.log("Player Status: IDLE"); 
      break; 
    
     case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
      console.log("Player Status: INITIALIZING"); 
      break; 
    
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
      console.log("Player Status: INITIALIZED"); 
      break; 
    
     case AdobePSDK.MediaPlayerStatus.PREPARING: 
      console.log("Player Status: PREPARING"); 
      break; 
    
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
      console.log("Player Status: PREPARED"); 
      break; 
    
     case AdobePSDK.MediaPlayerStatus.PLAYING: 
      console.log("Player Status: PLAYING"); 
      //update UI play/pause to show pause icon 
      break; 
    
     case AdobePSDK.MediaPlayerStatus.PAUSED: 
      console.log("Player Status: PAUSED"); 
      //update UI play/pause to show play icon & 
      //display pause icon over video 
      break; 
    
     case AdobePSDK.MediaPlayerStatus.SEEKING: 
      console.log("Player Status: SEEKING"); 
      break; 
    
     case AdobePSDK.MediaPlayerStatus.COMPLETE: 
      console.log("Player Status: COMPLETE"); 
      break; 
    
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: RELEASED"); 
      break; 
    
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: ERROR"); 
      break; 
    } 
   }; 
   
   ```

1. Create the `MediaResource`, which passes the M3U8 link (or mpd).

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. Create an empty config and replace the resource.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
    
   player.replaceCurrentResource(mediaResource, config);
   ```

1. When the player is in the INITIALIZED state, call `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. After the player is in the PREPARED state, call `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```
