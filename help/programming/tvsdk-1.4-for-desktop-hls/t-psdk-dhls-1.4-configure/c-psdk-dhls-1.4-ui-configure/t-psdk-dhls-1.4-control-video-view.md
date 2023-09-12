---
description: You can control the position and size of the video view using the MediaPlayerView object.
title: Control the position and size of the video view
exl-id: 5e7ae557-7f2b-4697-85eb-e72d1f43a7fc
---
# Control the position and size of the video view{#control-the-position-and-size-of-the-video-view}

You can control the position and size of the video view using the MediaPlayerView object.

TVSDK by default attempts to maintain the aspect ratio of the video view whenever the size or the position of the video changes (due to a change made by the application, or by a profile switch, or a content switch, etc.).

You can override the default aspect ratio behavior by specifying a different *scale policy*. Specify the scale policy using the `MediaPlayerView` object's `scalePolicy` property. The `MediaPlayerView`'s default scale policy is set with an instance of the `MaintainAspectRatioScalePolicy` class. To reset the scale policy, replace the default instance of `MaintainAspectRatioScalePolicy` on `MediaPlayerView.scalePolicy` with your own policy. (You cannot set the `scalePolicy` property to a null value.) 

1. Implement the `MediaPlayerViewScalePolicy` interface to create your own scale policy.

   The `MediaPlayerViewScalePolicy` has one method: 

   ```
   public function adjust(viewPort:Rectangle, 
     videoWidth:Number, videoHeight:Number):Rectangle;
   ```

   >[!NOTE]
   >
   >TVSDK uses a `StageVideo` object for displaying the video, and because `StageVideo` objects are not on the display list, the `viewPort` parameter contains the absolute coordinates of the video. 
   >
   >
   >For example:
   >
   >```
   >public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
   >    /** 
   >     * Default constructor. 
   >     */ 
   >    public function CustomScalePolicy() { 
   >    } 
   > 
   >    public function adjust(viewPort:Rectangle,  
   >                           videoWidth:Number,  
   >                           videoHeight:Number):Rectangle { 
   >        return customAdjustment(); 
   >    } 
   > 
   >    public function customAdjustment():Rectangle { 
   >        /* Your custom adjustment here */ 
   >        [...] 
   >    } 
   >}
   >```
   >

1. Assign your implementation to the `MediaPlayerView` property.

   ```
   var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
   view.scalePolicy = new CustomScalePolicy();
   ```

1. Add your view to the Media Player's `view` property.

   ```
   addChild(view); 
    
   mediaPlayer.view = view;
   ```

<!--<a id="example_7B08ECCDA17B4DD191FC672BD1F4C850"></a>-->

**For example: Scale the video to fill the entire video view, without maintaining aspect ratio:** 

```
package com.adobe.mediacore.samples.utils { 
    import com.adobe.mediacore.view.MediaPlayerViewScalePolicy; 
    import flash.geom.Rectangle; 
 
    /** 
    * A very simple custom scale policy - the video will fill the entire 
    * allocated space. The aspect ratio will not be kept. 
    */ 
    public class CustomScalePolicy implements MediaPlayerViewScalePolicy { 
 
        /** 
        * Default constructor. 
        */ 
        public function CustomScalePolicy() { 
        } 
 
        public function adjust(viewPort:Rectangle, 
                               videoWidth:Number,  
                               videoHeight:Number):Rectangle { 
            return viewPort; 
        } 
    } 
} 
 
var view:MediaPlayerView = MediaPlayerView.create(stage.stageVideos[0]); 
view.scalePolicy = new CustomScalePolicy(); 
addChild(view); 
mediaPlayer.view = view;
```
