---
description: TVSDK provides tools for creating an advanced video player application (your Primetime player), that you can integrate with other Primetime components. It also provides a number of features designed to maximize the quality of video playback.
title: Set up the Media player
exl-id: 99fdc4c1-0c67-4de5-87a5-b42d76f43ae9
---
# Set up the Media player {#set-up-the-media-player}

TVSDK provides tools for creating an advanced video player application (your Primetime player), that you can integrate with other Primetime components. It also provides a number of features designed to maximize the quality of video playback.

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

Instantiate a `MediaPlayer` and place a view of it into a frame layout.

1. Instantiate `MediaPlayer`, passing an `android.content.Context` object to the constructor: 

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Provide a frame layout ( `android.widget.FrameLayout`) to hold a `ViewGroup` of `mediaPlayer`: 

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >Below is the code snippet to create `_viewGroup`.

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

   >[!NOTE]
   >
   >The `MediaPlayer` instance ( `mediaPlayer`) is now available and properly configured to display video content on the device screen.
