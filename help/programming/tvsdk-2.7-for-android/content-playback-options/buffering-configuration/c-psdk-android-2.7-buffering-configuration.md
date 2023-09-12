---
description: To provide a smoother viewing experience, TVSDK sometimes buffers the video stream. You can configure how the player buffers.
title: Buffering
exl-id: f4df3084-376e-421c-aaa5-83de2815dabe
---
# Overview {#buffering-overview}

To provide a smoother viewing experience, TVSDK sometimes buffers the video stream. You can configure how the player buffers.

TVSDK defines a playback buffer length of at least 30 seconds and an initial buffer time before the media starts playing, of at least 2 seconds. After the application calls `play`, but before playback begins, TVSDK buffers the media up to the initial time to give a smooth start when it actually starts playing.

You can alter the buffer times by defining new buffering policies, and you can alter when the initial buffering occurs by using instant on.

## Buffering time policies {#section_9B3407D52F1E4CB48E7A4836EBDA8F70}

Depending on your environment (including the device, the operating system, or the network conditions), you can set different buffering policies for your player, such as changing the minimum duration for initial buffering and for ongoing playback buffering.

After you call `play`, the media player begins buffering the video. When the media player has buffered the amount of video specified by the initial buffer time, playback begins. This process improves the start-up time because the player does not wait for the entire playback buffer to fill before starting playback. Instead, after the few initial seconds are buffered, playback begins.

While the video is being rendered, TVSDK continues to buffer new fragments until it is has buffered the amount that is specified by the playback buffer time. If the current buffer length drops below the playback buffer time, the player will download additional fragments. Once the current buffer length is above the playback buffer time by a few seconds, TVSDK will stop downloading fragments.

>[!TIP]
>
>If the initial buffer value is high, it might give your user a long initial buffering time before starting. That might provide smooth playback for a longer time; however, if network conditions are poor, initial playback could be delayed.

If you enable instant on by calling `prepareBuffer`, the initial buffering begins at that moment, instead of waiting for `play`.

## Set buffering times {#section_05CDD927869D47EBA1D2069B1416B2E4}

The `MediaPlayer` provides methods to set and get the initial buffering time and playback buffering time.

>[!TIP]
>
>If you do not set the buffer control parameters before beginning playback, the media player defaults to 2 seconds for the initial buffer and 30 seconds for the ongoing playback buffer time.

1. Set up the `BufferControlParameters` object, which encapsulates the initial buffer time and playback buffer time control parameters.

   This class provides the following factory methods:

    * To set the initial buffer time equal to the play buffer time:     
    
      ```    
      public static BufferControlParameters createSimple(long bufferTime)
      ```    
    
    * To set the initial and play buffer times:     
    
      ```    
      public static BufferControlParameters createDual( 
        long initialBuffer,  
        long bufferTime)
      ```

   If the parameters are not valid, these methods throw `MediaPlayerException` with error code `PSDKErrorCode.INVALID_ARGUMENT`, such as when the following conditions are met:

    * The initial buffer time is less than zero. 
    * The initial buffer time is greater than the buffer time.

1. To set the buffer parameters values, use this `MediaPlayer` method: 

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. To get the current buffer parameter values, use this `MediaPlayer` method: 

   ```java
      BufferControlParameters getBufferControlParameters()  
   
   ```

<!--<a id="example_DE0580B3AD404635825D3301C1F096B6"></a>-->

For example, to set the initial buffer to 5 seconds and the playback buffer time to 30 seconds:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(5000, 30000));
```
