---
description: You can control the position and size of the video view using the MediaPlayerView object.
title: Control the position and size of the video view
exl-id: ab88a90f-4493-4f05-8da0-703ab3cf159e
---
# Control the position and size of the video view{#control-the-position-and-size-of-the-video-view}

You can control the position and size of the video view using the MediaPlayerView object.

Browser TVSDK by default attempts to maintain the aspect ratio of the video view whenever the size or the position of the video alters because of a change made by the application, a profile switch, a content switch, and so on.

You can override the default aspect ratio behavior by specifying a different *scale policy*. Specify the scale policy using the `MediaPlayerView` object's `scalePolicy` property. The default scale policy of `MediaPlayerView` is set with an instance of the `MaintainAspectRatioScalePolicy` class. To reset the scale policy, replace the default instance of `MaintainAspectRatioScalePolicy` on `MediaPlayerView.scalePolicy` with your own policy. 

>[!IMPORTANT]
>
>You cannot set the `scalePolicy` property to a null value.

## Non-Flash fallback scenarios {#non-flash-fallback-scenarios}

In non-Flash fallback scenarios, for scale policy to work correctly, the video div element given in the `View` constructor should return non-zero values for `offsetWidth` and `offsetHeight`. To give an example of incorrect function, sometimes when the width and height of the video div elements are not set explicitly in css, then the `View` constructor returns zero for `offsetWidth` or `offsetHeight`.

>[!NOTE]
>
>The CustomScalePolicy has limited support for a few browsers notably IE, Edge and Safari 9. For these browsers, the native aspect ratio of the video cannot be changed. However, the position and dimensions of the video will be enforced according to the scale policy.

1. Implement the `MediaPlayerViewScalePolicy` interface to create your own scale policy.

   The `MediaPlayerViewScalePolicy` has one method: 

   ```js
   /** 
   * Adjust the specified rectangle to match the new video dimensions. 
   * @param viewPort {AdobePSDK.Rectangle}The video rectangle as absolute position. 
   * @param videoWidth {Number}The video width. 
   * @param videoHeight {Number} The video height. 
   * @return {AdobePSDK.Rectangle} an adjusted rectangle. 
   */ 
   function adjustCallbackFunc(viewPort, videoWidth, videoHeight);
   ```

   For example: 

   ```js
   /** 
   Default Constructor 
   */ 
   MediaPlayerViewCustomScalePolicy = function() { 
       return this; 
   }; 
   MediaPlayerViewCustomScalePolicy.prototype = { 
       constructor: MediaPlayerViewScalePolicy, 
       adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
           /* Your Custom Adjustment here. */ 
           [...] 
           return adjustedRectangle; 
       } 
   };
   ```

1. Assign your implementation to the `MediaPlayerView` property.

   ```js
   var view = new AdobePSDK.MediaPlayerView(videoDiv); 
   view.scalePolicy= new MediaPlayerViewCustomScalePolicy();
   ```

1. Add your view to the Media Player's `view` property.

   ```
   mediaplayer.view = view;
   ```

<!--<a id="example_ABCD79AE29DB4A668F9A8B729FE44AF9"></a>-->

**For example: Scale the video to fill the entire video view, without maintaining aspect ratio:** 

```
/** 
 * Default constructor. 
 */ 
MediaPlayerViewCustomScalePolicy = function() { 
    return this; 
}; 
MediaPlayerViewCustomScalePolicy.prototype = { 
    constructor: MediaPlayerViewScalePolicy, 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    adjustCallbackFunc: function(viewPort, videoWidth, videoHeight) { 
        return viewPort; 
    } 
}; 
var view = new AdobePSDK.MediaPlayerView(videoDiv); 
view.scalePolicy = new MediaPlayerViewCustomScalePolicy (); 
mediaPlayer.view = view;
```
