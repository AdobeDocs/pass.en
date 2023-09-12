---
description: Use the helper class AuditudeSettings to set up Adobe Primetime ad decisioning metadata.
title: Set up ad insertion metadata
exl-id: 03b2237b-6b3b-46cf-bc0b-691513033463
---
# Set up ad insertion metadata{#set-up-ad-insertion-metadata}

Use the helper class AuditudeSettings to set up Adobe Primetime ad decisioning metadata.

>[!TIP]
>
>Adobe Primetime ad decisioning was previously known as Auditude .

1. Build the `AuditudeSettings` instance.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Set the Adobe Primetime ad decisioning mediaID, zoneID, domain, and the optional targeting parameters.

   ```js
   auditudeSettings.domain = "yourdomain"; 
   auditudeSettings.mediaId = "mediaid"; 
   auditudeSettings.zoneId = "zoneid";
   ```

1. Create a `MediaResource` instance by using the media stream URL and the previously created advertising metadata.

   ```js
   mediaResource = new AdobePSDK.MediaResource ( 
         resourceUrl, 
         resourceType,  
         auditudeSettings);
   ```

1. Load the `MediaResource` object through the `MediaPlayer.replaceCurrentResource(resource)` method.

   The `MediaPlayer` starts loading and processing the media stream manifest. 

1. When the `MediaPlayer` transitions to the INITIALIZED status, get the media stream characteristics in the form of a `MediaPlayerItem` instance through the `MediaPlayer.CurrentItem` attribute.
1. (Optional) Query the `MediaPlayerItem` instance to see whether the stream is live, regardless of whether it has alternate audio tracks.

   This information can help you prepare the UI for the playback. For example, if you know there are two audio tracks, you can include a UI control that toggles between these tracks. 

1. Call `MediaPlayer.prepareToPlay` to start the advertising workflow.

   After the ads have been resolved and placed on the timeline, the `  MediaPlayer ` transitions to the PREPARED state.
1. Call `MediaPlayer.play` to start the playback.
Browser TVSDK now includes ads when your media plays.
