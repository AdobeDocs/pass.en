---
description: You should release a MediaPlayer instance and resources when you no longer need the MediaResource.
title: Release a MediaPlayer instance and resources
exl-id: 2a802754-5c51-4e5f-8c36-843074b487b5
---
# Release a MediaPlayer instance and resources{#release-a-mediaplayer-instance-and-resources}

You should release a MediaPlayer instance and resources when you no longer need the MediaResource.

When you release a `MediaPlayer` object, the underlying hardware resources that are associated with this `MediaPlayer` object are deallocated.

Here are some reasons to release a `MediaPlayer`:

* Holding unnecessary resources can affect performance. 
* If multiple instances of the same video-codec are not supported on a device, playback failure might occur for other applications.

1. Release the `MediaPlayer`.

   ```
   function release():void;
   ```

After the `MediaPlayer` instance is released, you can no longer use it. If any method of the `MediaPlayer` interface is called after it is released, an `IllegalStateException` is thrown.
