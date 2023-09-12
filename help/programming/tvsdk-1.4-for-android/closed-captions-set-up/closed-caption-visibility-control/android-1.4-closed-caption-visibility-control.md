---
description: You can control the visibility of closed captions. When visibility is on, the currently selected track is displayed. If you change which track is current, the visibility setting remains the same.
title: Control closed-caption visibility
exl-id: d9428744-1700-4917-b334-d6e0446eaf37
---
# Overview {#control-closed-caption-visibility}

You can control the visibility of closed captions. When visibility is on, the currently selected track is displayed. If you change which track is current, the visibility setting remains the same.

>[!TIP]
>
>If closed caption text is displayed when the player enters the seek mode, the text no longer displays after the seek completes. Instead, after a few seconds, TVSDK displays the next closed caption text in the video after the ending seek position.

>[!NOTE]
>
>The visibility values for closed captions are defined in `MediaPlayer.Visibility`.
>
>```java
>enum Visibility { 
>    VISIBLE,  
>    INVISIBLE 
>}
>```
>

1. Wait for the MediaPlayer to have at least the PREPARED state (see [Wait for a valid state](../../../tvsdk-1.4-for-android/ui-configure/android-1.4-ui-state-prepared-wait-for.md)).
1. To get the current visibility setting for closed captions, use the getter method in MediaPlayer, which returns a visibility value.

   ```java
   Visibility getCCVisibility() throws IllegalStateException;
   ```

1. To change the visibility for closed captions, use the setter method, passing a visibility value from `MediaPlayer.Visibility`.

   For example: 

   ```java
   mediaPlayer.setCCVisibility(Visibility.VISIBLE);
   ```
