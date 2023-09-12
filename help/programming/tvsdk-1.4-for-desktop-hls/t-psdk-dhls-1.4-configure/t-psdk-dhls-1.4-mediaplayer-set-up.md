---
description: The MediaPlayer interface encapsulates the functionality and behavior of a media player.
title: Set up the MediaPlayer
exl-id: eec51f3e-4779-4fb5-b735-d5be412de64e
---
# Set up the MediaPlayer {#set-up-the-mediaplayer}

TVSDK provides tools for creating an advanced video player application (your Primetime player), which you can integrate with other Primetime components.

Use your platform's tools to create a player and connect it to the media player view in TVSDK, which has methods to play and manage videos. For example, TVSDK provides play and pause methods. You can create user interface buttons on your platform and set the buttons to call those TVSDK methods.The MediaPlayer interface encapsulates the functionality and behavior of a media player.

TVSDK provides a single implementation of the `MediaPlayer` interface: the DefaultMediaPlayer class. When you need video-playback functionality, instantiate `DefaultMediaPlayer`.

>[!NOTE]
>
>Interact with the `DefaultMediaPlayer` instance only with the methods exposed by the `MediaPlayer` interface.

1. Instantiate a `MediaPlayerContext` using the application-loaded `authorizedFeatures` instance (see [Load your signed token](../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/t-psdk-dhls-1.4-get-signed-token.md)).

   ```
   var context:MediaPlayerContext =  
       new MediaPlayerContext(authorizedFeatures)
   ```

1. Instantiate a `MediaPlayer` using the public create factory method, passing a `MediaPlayerContext` context object:

   ```
   public static function create(context:Context):MediaPlayer
   ```

   This returns a generic `MediaPlayer` interface. 1. Instantiate a `MediaPlayerView` and specify the StageVideo instance to be used:

   ```
   var view:MediaPlayerView =  
       MediaPlayerView.create(stage.stageVideos[0] )
   ```

1. Associate the `MediaPlayerView` instance with the newly created view:

   ```
   mediaPlayer.view = view;
   ```

1. Place the `MediaPlayerView` instance on the device's screen:

   ```
   container.addChild(view)
   ```

The `MediaPlayer` instance is now available and properly configured to display video content on the device screen.
