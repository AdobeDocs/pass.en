---
description: To add VPAID 2.0 support, add a custom ad view and appropriate listeners.
title: Implement VPAID 2.0 integration
exl-id: 8a6b81e7-1034-48fc-87aa-4cb8ab305d15
---
# Implement VPAID 2.0 integration {#implement-vpaid-integration}

To add VPAID 2.0 support, add a custom ad view and appropriate listeners.

To add VPAID 2.0 support: 

1. Add the custom ad view to the player interface when the player is in the PREPARED state.

   ```java
   ... 
   private FrameLayout _playerFrame; 
       ... 
       case PREPARED: 
           ... 
           addCustomView(); 
   ... 
   private void addCustomView() { 
       ... 
       WebView view = (WebView)_mediaPlayer.getCustomAdView(); 
       ... 
       _playerFrame.addView(view);
   ```

1. Create listeners and process the events described in  event-listeners .

   >[!IMPORTANT]
   >
   >In a VPAID 2.0 workflow, for custom ad views it is very important to maintain your `CustomAdView` instance across `AdBreak` starts (event `AD_BREAK_START`) and `AdBreak` completes (event `AD_BREAK_COMPLETE`), from the time you create the custom ad view through to when you dispose of it. That is, do not create a custom ad view on every ad break start and dispose of it on every ad break complete. 
   >
   >
   >In addition, you should only create your custom ad view when your player is in the PREPARED state, 
   >
   >
   >Only dispose of the custom ad view when reset is called. For example:
   >
   >```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >    _mediaPlayer.disposeCustomAdView(); 
   >    ... 
   >} 
   >```
   >
   >Finally, before you dispose of your custom ad view, you must remove it from the `FrameLayout`. For example:
   >
   >```
   >if (_playerFrame != null) 
   >    _playerFrame.removeAllViews(); 
   >```
