---
description: You can enable a TV-like experience of being able to join in the middle of an ad, in live streams.
title: Partial Ad break insertion
exl-id: cb0d2f5f-c760-450e-ab34-fd7639d1190b
---
# Partial Ad break insertion {#partial-ad-break-insertion}

You can enable a TV-like experience of being able to join in the middle of an ad, in live streams.

 The Partial Ad Break feature allows you to mimic a TV-like experience where, if the client starts a live stream inside a midroll, it will start within that midroll. It is similar to switching to a TV channel and the commercials run seamlessly.

For example, If a user joins in the middle of a 90-second ad break (three 30-second ads), 10 seconds into the second ad (that is, at 40 seconds into the ad break), the following happens:

* The second ad is played for the remaining duration (20 sec) followed by the third ad. 
* Ad trackers for the partially played ad (the second ad) are not fired. Only the tracker for the third ad is fired.

This behavior is not enabled by default. To enable this feature work in your app, do the following.

1. Disable the live prerolls, using AdvertisingMetadata class's method setEnableLivePreroll. 

   ```
   advertisingMetadata.setEnableLivePreroll(String.valueOf(false))
   ```

1. Switch ON the preference for Partial Ad-break Insertion. Use the new method setPartialAdBreakPref in MediaPlayer interface to switch this feature ON. Use getPartialAdBreakPref method to find the current state of this preference. 

   ```
   MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
        
          mediaPlayer.setPartialAdBreakPref(true); 
   
   ```

1. This feature requires you to implement a custom Ad policy selector to customize the behavior. If you do not already have a custom implementation of AdvertisingFactory class, then add a new AdvertisingFactory implementation. Override the createAdPolicySelector method. This method returns a new instance of the implementation of AdPolicySelector.

   A sample implementation is given below for your reference. The following sample implementation is available for use from the com.adobe.mediacore package. However, it is simplified for an easy reference and it is not recommended to be used as is.

    1. Sample Ad policy selector     
    
       ```    
        package com.adobe.mediacore;

       import com.adobe.mediacore.logging.Log; 
       import com.adobe.mediacore.logging.Logger; 
       import com.adobe.mediacore.metadata.*; 
       import com.adobe.mediacore.timeline.advertising.*; 
        
       import java.util.ArrayList; 
       import java.util.List; 
        
       public class PartialAdBreakAdPolicySelector implements AdPolicySelector { 
           private static final String LOG_TAG = "[PSDK]::" + DefaultAdPolicySelector.class.getSimpleName(); 
           private final Logger _logger = Log.getLogger(LOG_TAG); 
        
           private final MediaPlayerItem _mediaPlayerItem; 
           private final AdBreakAsWatched _adBreakAsWatchedPolicy; 
        
           public PartialAdBreakAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
               _mediaPlayerItem = mediaPlayerItem; 
               _adBreakAsWatchedPolicy = extractAdBreakAsWatchedPolicy(_mediaPlayerItem); 
           } 
        
           @Override 
           public AdBreakPolicy selectPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
               _logger.i(LOG_TAG + "#selectPolicyForAdBreak", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                       + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
        
               if (adPolicyInfo.getAdBreakPlacements().size() > 0) { 
                   AdBreakPlacement adBreakTimelineItem = adPolicyInfo.getAdBreakPlacements().get(0); 
                   if (adPolicyInfo.getMode() == AdPolicyMode.SEEK && adBreakTimelineItem.getAdBreak().isWatched()) { 
                       return AdBreakPolicy.SKIP; 
                   } 
               } 
        
               AdSignalingMode adSignalingMode = AdSignalingMode.DEFAULT; 
               if (_mediaPlayerItem != null) { 
                   MetadataNode metadata = (MetadataNode) _mediaPlayerItem.getResource().getMetadata(); 
                   if (metadata != null) { 
                       AdvertisingMetadata advertisingMetadata = (AdvertisingMetadata) metadata.getNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue()); 
                       if (advertisingMetadata != null) { 
                           adSignalingMode = advertisingMetadata.getSignalingMode(); 
                       } 
                   } 
               } 
        
               // can't remove main content due to a ave bug, need to check if stream is live or ad signaling mode is manifest cue 
               if (_mediaPlayerItem.isLive() || adSignalingMode == AdSignalingMode.MANIFEST_CUES) { 
                   return AdBreakPolicy.PLAY; 
               } 
        
               return AdBreakPolicy.REMOVE_AFTER_PLAY; 
           } 
        
           @Override 
           public List<AdBreakPlacement> selectAdBreaksToPlay(AdPolicyInfo adPolicyInfo) { 
               _logger.i(LOG_TAG + "#selectAdBreaksToPlay", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                       + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
        
               List<AdBreakPlacement> adBreakPlacements = adPolicyInfo.getAdBreakPlacements(); 
               if (adBreakPlacements != null) { 
                   int size = adBreakPlacements.size(); 
                   List<AdBreakPlacement> adBreaks = new ArrayList<AdBreakPlacement>(); 
                   if (size > 0 && adPolicyInfo.getCurrentTime() <= adPolicyInfo.getSeekToTime()) { 
                       AdBreakPlacement adBreak = adBreakPlacements.get(size - 1); 
                       if (!adBreak.getAdBreak().isWatched()) { 
                           adBreaks.add(adBreak); 
                           return adBreaks; 
                       } 
                   } 
               } 
        
               return null; 
           } 
        
           @Override 
           public AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo) { 
               _logger.i(LOG_TAG + "#selectPolicyForSeekIntoAd", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                       + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
        
               // If you really want to allow seek during ads (you likely do not). 
               return AdPolicy.PLAY; 
           } 
        
           @Override 
           public AdBreakAsWatched selectWatchedPolicyForAdBreak(AdPolicyInfo adPolicyInfo) { 
               _logger.i(LOG_TAG + "#selectWatchedPolicyForAdBreak", "currentTime=" + adPolicyInfo.getCurrentTime() + " seekToTime=" 
                       + adPolicyInfo.getSeekToTime() + " rate=" + adPolicyInfo.getRate() + " adPolicyMode=" + adPolicyInfo.getMode()); 
        
               return _adBreakAsWatchedPolicy; 
           } 
        
           /** 
            * Extract the ad break watched policy for the specified media player item. 
            * 
            * @param item Associated media player item. 
            * @return a valid ad break watched policy. 
            */ 
           private AdBreakAsWatched extractAdBreakAsWatchedPolicy(MediaPlayerItem item) { 
               AdBreakAsWatched adBreakWatchedPolicy = AdBreakAsWatched.AD_BREAK_AS_WATCHED_ON_BEGIN; 
        
               if (item != null) { 
                   MetadataNode metadata = (MetadataNode) item.getResource().getMetadata(); 
                   if (metadata != null) { 
                       AdvertisingMetadata advertisingMetadata = (AdvertisingMetadata) metadata.getNode(DefaultMetadataKeys.ADVERTISING_METADATA.getValue()); 
                       if (advertisingMetadata != null) { 
                           adBreakWatchedPolicy = advertisingMetadata.getAdBreakAsWatched(); 
                       } 
                   } 
               } 
        
               return adBreakWatchedPolicy; 
           } 
       } 
       
       ```

    1. Sample Advertising factory     
    
       ```    
       private AdvertisingFactory createPartialAdBreakFactory() { 
       return new AdvertisingFactory() { 
       @Override 
                    public AdPolicySelector  
       createAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
                       return new PartialAdBreakAdPolicySelector(mediaPlayerItem); 
                    } 
        
       // Rest of the interface methods can be overridden as per your  
       // customization needs 
       // As shown next 
       @Override 
       public AdPolicySelector  
       createAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
          return new PartialAdBreakAdPolicySelector(mediaPlayerItem); 
         } 
       // . . . 
        
        } 
       } 
       
       ```

    1. Register our AdvertisingFactory with the media player     
    
       ```    
       AdvertisingFactory advertisingFactory = createPartialAdBreakFactory();  
        
       if (advertisingFactory != null) { 
                   mediaPlayer.registerAdClientFactory(advertisingFactory); 
       } 
       
       ```    
    
    1. Override the createAdPolicySelector method     
    
       ```    
       @Override 
       public AdPolicySelector  
       createAdPolicySelector(MediaPlayerItem mediaPlayerItem) { 
          return new PartialAdBreakAdPolicySelector(mediaPlayerItem); 
       } 
       
       ```
