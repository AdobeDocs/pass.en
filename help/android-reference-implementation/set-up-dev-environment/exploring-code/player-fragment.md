---
description: The PlayerFragment class is where you edit the code to create the fully-enabled feature managers.
title: PlayerFragment
exl-id: 9060f0f5-9148-48cd-b89b-718607dd70bc
---
# PlayerFragment {#playerfragment}

The PlayerFragment class is where you edit the code to create the fully-enabled feature managers.

The `PlayerFragment` class contains all the UI components such as the `playerFrame`, `ControlBar`, `playerClickableAdFragment`, and `adOverlay`.

It handles the initialization of all these components as well as creating the player, setting up the views, creating feature managers for the media player, handling media events such as resume, play, and pause and handling the event listeners for `QoSManager`, `DRMManager`, `CCManager`, `AAManager`, `AdsManager`, `PlaybackManager`, and `EntitlementManager`.

The XML file that includes the configuration parameters for the `PlayerFragment` is `res/layout/fragment_player.xml`.

Before you create the feature managers you need to create the media player by making sure the following code is in the `PlayerFragment.java` file: 

```java
private MediaPlayer createMediaPlayer() { 
  MediaPlayer mediaPlayer =  
    DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
  return mediaPlayer; 
}
```
