---
description: The MediaPlayer interface for Android encapsulates the functionality and behavior of a media player.
title: Set up the MediaPlayer
exl-id: 2698fe8d-0b73-4aad-9fee-55d034d8ca64
---
# Set up the MediaPlayer {#set-up-the-mediaplayer}

The MediaPlayer interface for Android encapsulates the functionality and behavior of a media player.

TVSDK provides one implementation of the `MediaPlayer` interface, the `DefaultMediaPlayer` class. When you need video playback functionality, instantiate `DefaultMediaPlayer`.

>[!TIP]
>
>Interact with the `DefaultMediaPlayer` instance only with the methods that are exposed by the `MediaPlayer` interface.

1. Instantiate a MediaPlayer using the public `DefaultMediaPlayer.create` factory method, passing a Java Android application context object.

   ```java
   public static MediaPlayer create(Context context) 
   
   ```

1. Call `MediaPlayer.getView` to get a reference to the `MediaPlayerView` instance.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   
   ```

1. Place the `MediaPlayerView` instance in a `FrameLayout` instance, which places the video on the device's screen.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   
   ```

The `MediaPlayer` instance is now available and properly configured to display video content on the device screen.
