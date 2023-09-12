---
description: You can enable or disable the Lazy Ad Resolving feature using the existing Lazy Ad Loading mechanism (Lazy Ad Resolving is disabled by default).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
title: Enable lazy ad resolving
exl-id: a52a1f9a-3bf6-4193-8347-1ef248ba8884
---
# Enable lazy ad resolving {#enable-lazy-ad-resolving}

You can enable or disable the Lazy Ad Resolving feature using the existing Lazy Ad Loading mechanism (Lazy Ad Resolving is disabled by default).

You can enable or disable Lazy Ad Resolving by calling [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) with true or false.

* Use the Boolean *hasDelayAdLoading* and *setDelayAdLoading* methods in AdvertisingMetadata to control the timing of ad resolution and the placement of ads on the timeline:

    * If *hasDelayAdLoading* returns false, TVSDK waits until all ads are resolved and placed before transitioning to the PREPARED state. 
    * If *hasDelayAdLoading* returns true, TVSDK resolves only the initial ads and transitions to the PREPARED state.

        * The remaining ads are resolved and placed during playback.

    * When *hasPreroll *or *hasLivePreroll* return false, TVSDK assumes that there is no preroll ad and starts the playback of the content immediately. These are default set to true.

**APIs relevant to lazy ad resolution:**

```
Class:    com.adobe.mediacore.metadata.AdvertisingMetadata 
Methods: 
    public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
    public final void setDelayAdLoading() // Enable or disable Lazy Ad Resolving 
    public final void setDelayAdLoadingTolerance() // Sets the Lazy Ad Resolving Tolerance level.  This value is added to the BufferControlParameters::playBufferTime and the content's EXT-X-TARGETDURATION to determine when ad breaks should resolve 
    public final double getDelayAdLoadingTolerance() // Gets the Lazy Ad Resolving Tolerance level 
    public final boolean hasPreroll() // Check for existence of pre-roll ads 
    public final void setPreroll() // Set pre-roll true or false 
    public final boolean hasLivePreroll() // Check for live pre-roll ads 
    public final void setLivePreroll() // Set live pre-roll true or false

Class:     com.adobe.mediacore.timeline.TimelineMarker 
Methods: 
    public double getDuration() // Returns the current duration of the TimelineMarker.  This will be zero if the ad break has not yet resolved. 
    public Placement.Type getPlacementType() // Returns whether
```

To accurately reflect ads as cues on a scrub bar, listen for the `TimelineEvent`event and redraw the scrub bar every time you receive this event.

When Lazy Ad Resolving is enabled for VOD streams, all ad breaks are placed on the timeline, however, many of the ad breaks will not be resolved yet. The application can determine whether or not to draw these markers by checking the `TimelineMarker::getDuration()`. If the value is greater than zero, then the ads within the ad break have been resolved.

TVSDK dispatches this event when an ad break has been resolved, and also when the player transitions to the PREPARED status.

```
mediaPlayer.addEventListener(MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
/** 
* ... 
*/ 
public void onTimelineUpdated(TimelineEvent event) { 
for (PlaybackManagerEventListener listener : eventListeners) { 
  listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
}
```
