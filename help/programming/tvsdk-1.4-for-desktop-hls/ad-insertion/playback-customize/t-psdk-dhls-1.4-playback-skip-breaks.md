---
description: By default, TVSDK forces an ad break to play when the user seeks over an ad break. You can customize the behavior to skip an ad break if the time elapsed from a previous break completion is within a certain number of minutes.
title: Skip ad breaks for a period of time
exl-id: 7d5ee788-4a67-4c70-acc7-a950e6b2db8a
---
# Skip ad breaks for a period of time{#skip-ad-breaks-for-a-period-of-time}

By default, TVSDK forces an ad break to play when the user seeks over an ad break. You can customize the behavior to skip an ad break if the time elapsed from a previous break completion is within a certain number of minutes.

>[!IMPORTANT]
>
>When there is an internal seek to skip an ad, here might be a slight pause in the playback.

The following example of a customized ad policy selector skips ads in the next five minutes (wall clock time) after a user has watched an ad break. 

1. Extend the default ad policy selector to override the default behavior.

   ```
   /** 
    * Custom ad policy selector. 
    */ 
   public class CustomAdPolicySelector extends DefaultAdPolicySelector { 
     
       /** 
        * Default constructor. 
        * 
        * @param item Associated media player item. 
        */ 
       public function CustomAdPolicySelector(item:MediaPlayerItem) { 
           super(item); 
     
           item.player.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED,  
                                        onAdBreakCompleted); 
       } 
     
       override public function selectPolicyForAdBreak(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForAdBreak(adPolicyInfo); 
           } 
     
           return AdBreakPolicy.SKIP; 
       } 
     
       override public function selectAdBreaksToPlay(adPolicyInfo:AdPolicyInfo):Vector.<AdBreakTimelineItem> { 
           if (shouldPlayAds()) { 
               return super.selectAdBreaksToPlay(adPolicyInfo); 
           } 
     
           return new Vector.<AdBreakTimelineItem>(); 
       } 
     
       override public function selectPolicyForSeekIntoAd(adPolicyInfo:AdPolicyInfo):String { 
           if (shouldPlayAds()) { 
               return super.selectPolicyForSeekIntoAd(adPolicyInfo); 
           } 
     
           return AdPolicy.SKIP_TO_NEXT_AD_IN_AD_BREAK; 
       } 
     
       private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
           _lastAdBreakPlayedTime = new Date().valueOf(); 
       } 
     
       private function shouldPlayAds():Boolean { 
           var currentTime:Number = new Date().valueOf(); 
           return isNaN(_lastAdBreakPlayedTime) 
                   ||  (currentTime - _lastAdBreakPlayedTime > _minimumInterval); 
       } 
     
       private var _lastAdBreakPlayedTime:Number = NaN; 
       private var _minimumInterval:Number = 300000; // 5 minutes in milliseconds 
   }
   ```

1. Create a new advertising factory that uses your custom selector.

   ```
   public class CustomAdPolicyContentFactory extends DefaultContentFactory { 
     
       private var _adPolicySelector:CustomAdPolicySelector; 
            
       /** 
        * Default constructor. 
        */ 
       public function CustomAdPolicyContentFactory() { 
                
       } 
            
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveAdPolicySelector(item:MediaPlayerItem):AdPolicySelector { 
       if (!_adPolicySelector) { 
           _adPolicySelector = new CustomAdPolicySelector(item); 
       } 
                            
       return _adPolicySelector; 
       } 
   }
   ```

1. Register the new advertising factory class to be used with the MediaPlayer.

   ```
   var mediaResource:MediaResource =  
     MediaResource.createFromUrl("https://example.org/stream.m3u8", null); 
   var mediaPlayerItemConfig:MediaPlayerItemConfig =  
     PSDKConfig.retrieveMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomAdPolicyContentFactory(); 
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
