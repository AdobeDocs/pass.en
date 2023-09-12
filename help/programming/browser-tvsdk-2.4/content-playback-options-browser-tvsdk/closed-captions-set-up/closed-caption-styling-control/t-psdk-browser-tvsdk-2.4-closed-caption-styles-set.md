---
description: You can set the format, such as font, size, color, edge, and opacity for closed-caption text.
title: Set closed-caption styles
exl-id: 7ece68ce-0dc5-4899-9834-39940bbd0332
---
# Set closed-caption styles{#set-closed-caption-styles}

You can set the format, such as font, size, color, edge, and opacity for closed-caption text.

1. Wait for the `MediaPlayer` to be at least in the PREPARED state.

   For more information about the states, see [Wait for a valid state](../../../content-playback-options-browser-tvsdk/ui-configure/t-psdk-browser-tvsdk-2.4-ui-state-prepared-wait-for.md).
1. Create a `TextFormat` instance.

   You can provide all the closed-caption styling parameters now or set them later.

   ```js
   new TextFormat( 
       font,   
       fontColor,  
       edgeColor,   
       fontEdge,  
       backgroundColor,   
       fillColor,  
       size,   
       fontOpacity,   
       backgroundOpacity,  
       fillOpacity, 
       bottomInset 
       safeArea) → {AdobePSDK.TextFormat}
   ```

1. (Optional) Get the current closed-caption style settings with `MediaPlayer.ccStyle`.

   The return value is an instance of the `TextFormat` interface.

   If no style was previously set, it returns a TextFormat object with default values for each attribute: 

   ```js
   ccStyle :AdobePSDK.TextFormat
   ```

1. To change the style settings, use `MediaPlayer.ccStyle`, passing an instance of the `TextFormat` interface.

   You can use this method even if the current media stream has no closed captions. 

   ```js
   ccStyle :AdobePSDK.TextFormat 
   ```

   >[!TIP]
   >
   >Setting the closed-caption style is asynchronous, so it might take a few seconds for the changes to appear on the screen.
