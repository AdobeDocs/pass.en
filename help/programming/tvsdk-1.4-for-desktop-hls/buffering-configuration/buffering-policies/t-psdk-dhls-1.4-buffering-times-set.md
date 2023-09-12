---
description: The MediaPlayer provides methods to set and get the initial buffering time and playback buffering time.
title: Set buffering times
exl-id: d2fbae05-2190-4acc-ae63-561db030608a
---
# Set buffering times{#set-buffering-times}

The MediaPlayer provides methods to set and get the initial buffering time and playback buffering time.

>[!TIP]
>
>If you do not set the buffer control parameters before beginning playback, the media player defaults to 2 seconds for the initial buffer and 30 seconds for the ongoing playback buffer time.

1. Set up the `BufferControlParameters` object, which encapsulates the initial buffer time and playback buffer time control parameters:

       This class provides the following factory methods:

    * To set the initial buffer time equal to the play buffer time:     
    
      ```    
      createSimple(bufferTime:uint):BufferControlParameters
      ```    
    
    * To set both the initial and play buffer times:     
    
      ```    
      createDual(initialBufferTime:uint, playbackBufferTime:uint):BufferControlParameters 
      
      ```

       These methods throw an `IllegalArgumentException` if the parameters are not valid, such as when:

    * The initial buffer time is less than zero. 
    * The initial buffer time is greater than the buffer time.

1. To set the buffer parameter values, use this `MediaPlayer` method:

   ```
   public function set bufferControlParameters(value:BufferControlParameters):void
   ```

1. To get the current buffer parameter values, use this `MediaPlayer` method:

   ```
   public function get bufferControlParameters():BufferControlParameters
   ```

<!--<a id="example_B5C5004188574D8D8AB8525742767280"></a>-->

For example, to set the initial buffer to 2 seconds and the playback buffer time to 30 seconds:

```
mediaPlayer.bufferControlParameters = BufferControlParameters.createDual(2000, 30000); 
```

The `psdkdemo` demonstrates this feature; use the application's settings to set the buffer values.
