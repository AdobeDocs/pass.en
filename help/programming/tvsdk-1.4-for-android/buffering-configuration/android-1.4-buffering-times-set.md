---
description: To provide a smoother viewing experience, TVSDK sometimes buffers the video stream. You can configure the way the player buffers.
title: Set buffering times
exl-id: 4542d10a-b6f8-430d-8b9a-5a358d1c0e9d
---
# Buffering {#buffering}

To provide a smoother viewing experience, TVSDK sometimes buffers the video stream. You can configure the way the player buffers.

TVSDK defines a playback buffer length of at least 30 seconds and an initial buffer time within that, before the media starts playing, of at least 2 seconds. After the application calls `play` but before playback begins, TVSDK buffers the media up to the initial time to give a smooth start when it actually starts playing.

You can alter the buffer times by defining new buffering policies and you can alter when the initial buffering occurs by using instant-on.

## Set buffering times {#set-buffering-times}

The `MediaPlayer` provides methods to set and get the initial buffering time and playback buffering time.

>[!TIP]
>
>If you do not set the buffer control parameters before beginning playback, the media player defaults to 2 seconds for the initial buffer and 30 seconds for the ongoing playback buffer time.

1. Set up the `BufferControlParameters` object, which encapsulates the initial buffer time and playback buffer time control parameters:

       This class provides two factory methods:

    * To set the initial buffer time equal to the play buffer time:     
    
      ```java    
      public static BufferControlParameters createSimple( 
          long bufferTime)
      ```    
    
    * To set both the initial and play buffer times:     
    
      ```java    
      public static BufferControlParameters createDual( 
          long initialBuffer,   
          long bufferTime)
      ```

       These methods throw an `IllegalArgumentException` if the parameters are not valid, such as when:

    * The initial buffer time is less than zero. 
    * The initial buffer time is greater than the buffer time.

1. To set the buffer parameter values, use this `MediaPlayer` method:

   ```java
   void setBufferControlParameters(BufferControlParameters params)
   ```

1. To get the current buffer parameter values, use this `MediaPlayer` method:

   ```java
      BufferControlParameters getBufferControlParameters()  
   
   ```

   If the AVE cannot set the specified values, the media player enters the `ERROR` state with the error code `SET_BUFFER_PARAMETERS_ERROR`.

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

For example, to set the initial buffer to 2 seconds and the playback buffer time to 30 seconds:

```java
mediaPlayer.setBufferControlParameters(BufferControlParameters.createDual(2000, 30000));
```

The Primetime reference implementation demonstrates this feature; use the application's settings to set the buffer values.
