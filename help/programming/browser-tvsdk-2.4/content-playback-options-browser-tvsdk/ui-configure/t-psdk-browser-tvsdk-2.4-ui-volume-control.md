---
description: You can set up a user interface control for sound volume.
title: Provide volume control
exl-id: 5c446081-5491-46b6-9259-293131af80cb
---
# Provide volume control{#provide-volume-control}

You can set up a user interface control for sound volume.

1. Wait for the `MediaPlayer` instance to be in a valid state for this command.

   Any state except for RELEASED or ERROR is valid.
1. Set the volume attribute on the `MediaPlayer` instance to set the audio volume.

   ```js
   player.volume = ...
   ```

   The value for the volume represents the requested volume expressed as a proportion of the maximum volume, where 0 is silent and is the maximum volume.
