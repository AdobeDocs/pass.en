---
description: You can set up a user interface control to adjust the volume for the video.
title: Provide volume control
exl-id: 0daa87e2-51aa-4459-9a67-135dc54d09c7
---
# Provide volume control {#provide-volume-control}

You can set up a user interface control to adjust the volume for the video.

1. In the callback routine for the volume control interface element, ensure that the player is in a valid status for this command.

   >[!TIP]
   >
   >Any status, except for RELEASED is valid.

1. Call `setVolume` to set the audio volume.

   For example: 

   ```java
   void setVolume(int volume) throws MediaPlayerException;
   ```

   The value for the volume represents the requested volume expressed as a proportion of the maximum volume, where `0` is silent and `1` is the maximum volume.
