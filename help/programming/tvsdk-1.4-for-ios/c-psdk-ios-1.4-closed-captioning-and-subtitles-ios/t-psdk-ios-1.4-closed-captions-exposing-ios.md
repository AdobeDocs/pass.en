---
description: To make closed captions available to your client player, you must enable them. The user can turn closed captions on or off and select the formatting.
title: Expose closed captions
exl-id: 57168c6e-a958-4a89-b22b-0c9f1cab3a49
---
# Expose closed captions {#expose-closed-captions}

To make closed captions available to your client player, you must enable them. The user can turn closed captions on or off and select the formatting.

To expose closed captions: 

1. In `PTMediaPlayer` object, set the `closedCaptionDisplayEnabled` property.

   If the user has enabled closed captions, this step displays the text. 

   >[!NOTE]
   >
   >The client user turns closed captioning on or off by using the iOS Accessibility Settings, and these settings also provide formattng options.

   >[!NOTE]
   >
   >`closedCaptionDisplayEnabled` property is deprecated. Use `subtitlesOptions` property of `PTMediaPlayerItem`. See [Expose subtitles](../../tvsdk-1.4-for-ios/c-psdk-ios-1.4-closed-captioning-and-subtitles-ios/t-psdk-ios-1.4-subtitles-exposing-ios.md) to use closed captions.
