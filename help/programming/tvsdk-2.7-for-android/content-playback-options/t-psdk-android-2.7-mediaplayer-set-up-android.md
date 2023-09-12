---
description: Instantiate a MediaPlayer and place a view of it into a frame layout.
title: Set up the MediaPlayer
exl-id: e8fb6527-154b-4f7e-a128-525b5a3b3474
---
# Set up the MediaPlayer {#set-up-the-mediaplayer}

TVSDK provides tools for creating an advanced video player application (your Primetime player), that you can integrate with other Primetime components. It also provides a number of features designed to maximize the quality of video playback.

Instantiate a MediaPlayer and place a view of it into a frame layout.

1. Instantiate `MediaPlayer`, passing an `android.content.Context` object to the constructor:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Provide a frame layout ( `android.widget.FrameLayout`) to hold a `ViewGroup` of `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   Below is the code snippet to create `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. Place a view of `mediaPlayer` inside the frame layout:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>The `MediaPlayer` instance ( `mediaPlayer`) is now available and properly configured to display video content on the device screen.
