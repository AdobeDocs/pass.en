---
description: Use the helper class AuditudeSettings, which extends the MetadataNode class, to set up Adobe Primetime ad decisioning metadata.
title: Set up ad insertion metadata
exl-id: f7d1eb7d-e0be-4f0f-9dec-9336641a8f87
---
# Set up ad insertion metadata {#set-up-ad-insertion-metadata}

Use the helper class `AuditudeSettings`, which extends the `MetadataNode` class, to set up Adobe Primetime ad decisioning metadata.

>[!TIP]
>
>Adobe Primetime ad decisioning was previously known as Auditude.

Advertising metadata is in the `MediaResource.Metadata` property. When starting the playback of a new video, your application is responsible for setting the correct advertising metadata. 

1. Build the `AuditudeSettings` instance.

   ```java
   AuditudeSettings auditudeSettings = new AuditudeSettings();
   ```

1. Set the Adobe Primetime ad decisioning `mediaID`, `zoneID`, `<ph conkeyref="phrases/primetime-sdk-name"/>`, and the optional targeting parameters.

   ```java
   auditudeSettings.setZoneId("yourZoneId"); 
   auditudeSettings.setMediaId("yourVideoId"); 
   auditudeSettings.setDefaultMediaId("defVideoId"); 
   auditudeSettings.setDomain("yourAuditudeDomain"); 
    
   // Optionally set user agent  
   auditudeSettings.setUserAgent("yourUserAgent"); 
    
   Metadata targetingParameters = new Metadata(); 
   targetingParameters.setValue("desired_param", "desired_value"); 
   auditudeSettings.setTargetingParameters(targetingParameters);
   ```

   >[!TIP]
   >
   >The media ID is consumed by TVSDK as a string, that is converted to an md5 value, and is used for the `u` value in the Primetime ad decisioning URL request. For example:
   >
   >`https://ad.auditude.com/adserver? **u**=c76d04ee31c91c4ce5c8cee41006c97d &z=114100&l=20150206141527&of=1.4&tm=15&g=1000002`

1. Create a `MediaResource` instance by using the media stream URL and the previously created advertising metadata.

   ```java
   MediaResource mediaResource = new MediaResource( 
   "https://example.com/media/test_media.m3u8", MediaResource.Type.HLS, Metadata);
   ```

1. Load the `MediaResource` object through the `MediaPlayer.replaceCurrentResource` method.

   The `MediaPlayer` starts loading and processing the media stream manifest. 

1. When the `MediaPlayer` transitions to the INITIALIZED status, get the media stream characteristics in the form of a `MediaPlayerItem` instance through the `MediaPlayer.CurrentItem` method.
1. (Optional) Query the `MediaPlayerItem` instance to see whether the stream is live, regardless of whether it has alternate audio tracks or the stream is protected.

   This information can help you prepare the UI for the playback. For example, if you know there are two audio tracks, you can include a UI control that toggles between these tracks. 

1. Call `MediaPlayer.prepareToPlay` to start the advertising workflow.

   After the ads have been resolved and placed on the timeline, the `MediaPlayer` transitions to the `PREPARED` state.
1. Call `MediaPlayer.play` to start the playback.
TVSDK now includes ads when your media plays.
