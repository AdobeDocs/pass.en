---
description: From the moment the MediaPlayer instance is created to the moment it is terminated, this instance transitions from one state to the next.
title: Life cycle and states of the MediaPlayer object
exl-id: 26cad982-ef85-42fb-aaa7-e5d494088766
---
# Life cycle and states of the MediaPlayer object{#life-cycle-and-states-of-the-mediaplayer-object}

From the moment the MediaPlayer instance is created to the moment it is terminated, this instance transitions from one state to the next.

Here are the possible states:

* **IDLE**: `MediaPlayerStatus.IDLE` 

* **INITIALIZING**: `MediaPlayerStatus.INITIALIZING` 

* **INITIALIZED**: `MediaPlayerStatus.INITIALIZED` 

* **PREPARING**: `MediaPlayerStatus.PREPARING` 

* **PREPARED**: `MediaPlayerStatus.PREPARED` 

* **PLAYING**: `MediaPlayerStatus.PLAYING` 

* **PAUSED**: `MediaPlayerStatus.PAUSED` 

* **SEEKING**: `MediaPlayerStatus.SEEKING` 

* **COMPLETE**: `MediaPlayerStatus.COMPLETE` 

* **ERROR**: `MediaPlayerStatus.ERROR` 

* **RELEASED**: `MediaPlayerStatus.RELEASED`

The complete list of states is defined in `MediaPlayerStatus`.

Knowing the player's state is useful because some operations are permitted only while the player is in a particular state. For example, `play` cannot be called while in the IDLE state. It must be called after reaching the PREPARED state. The ERROR state also changes what can happen next.

As a media resource is loaded and played, the player transitions in the following way:

1. The initial state is IDLE. 
1. Your application calls `MediaPlayer.replaceCurrentResource`, which moves the player to the INITIALIZING state. 
1. If Browser TVSDK successfully loads the resource, the state changes to INITIALIZED. 
1. Your application calls `MediaPlayer.prepareToPlay`, and the state changes to PREPARING. 
1. Browser TVSDK prepares the media stream and starts the ad resolving and ad insertion (if enabled).

   When this step is complete, ads are inserted in the timeline or the ad procedure has failed, and the player state changes to PREPARED. 
1. As your application plays and pauses the media, the state moves between PLAYING and PAUSED. 

   >[!TIP]
   >
   >While playing or paused, when you navigate away from the playback, shut down the device, or switch applications, the state changes to SUSPENDED and resources are released. To continue, restore the media player.

1. When the player reaches the end of the stream, the state becomes COMPLETE. 
1. When your application releases the media player, the state changes to RELEASED. 
1. If an error occurs during the process, the state changes to ERROR.

Here is an illustration of the life cycle of a MediaPlayer instance: 

<!--<a id="fig_DD3DAE7507C549C8A4720A26DFCFFCCB"></a>-->

![](assets/player-state-transitions-diagram-android_1.2_web.png)

You can use the state to provide feedback to the user on the process (for example, a spinner while waiting for the next state change) or to take the next steps in playing the media, such as waiting for the appropriate state before calling the next method.

For example:

```js
function onStateChanged(state) { 
    switch(state) { 
        // It is recommended that you call prepareToPlay()  
        // after receiving the INITIALIZED state             
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            mediaPlayer.prepareToPlay(); 
            break; 
    } 
} 

```
