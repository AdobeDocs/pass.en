---
description: To make closed captions available to your client player, you must enable them. The user can turn closed captions on or off and select the formatting.
title: Expose closed captions
exl-id: 6383a2b2-04e3-4fe1-a573-5e1f1ef486ed
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
   >`closedCaptionDisplayEnabled` property is deprecated. Use `subtitlesOptions` property of `PTMediaPlayerItem`. See [Expose subtitles](../../../tvsdk-3x-ios-prog/c-ios-closed-captioning-and-subtitles-ios/c-ios-closed-captioning-and-subtitles-reqts-ios/t-ios-subtitles-exposing-ios.md) to use closed captions.
