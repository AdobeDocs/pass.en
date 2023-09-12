---
description: Event handlers allow TVSDK to respond to events.
title: Implement event listeners and callbacks
exl-id: eda5cd4e-4ee8-4b37-a179-242e8697f61f
---
# Implement event listeners and callbacks{#implement-event-listeners-and-callbacks}

Event handlers allow TVSDK to respond to events.

When an event occurs, TVSDK's event mechanism calls your registered event handler and passes the event information to the handler.

TVSDK defines listeners as public internal interfaces in the `MediaPlayer` interface.

Your application must implement event listeners for TVSDK events that affect your application.

For a complete list of the events for video analytics, see Track Core Video Playback.

1. Determine for which events your application must listen.

    * **Required events**: Listen for all playback events.     
    
      >[!IMPORTANT]
      >
      >The playback event `onStateChanged` provides the player state, including errors. Any of the states might affect your player's next step

    * **Other events**: Optional, depending on your application.

      For example, if you incorporate advertising in your playback, implement the AdPlaybackEventListener callbacks.

1. Implement event listeners for each event.

   TVSDK returns parameter values to your event-listener callbacks. These values, provide relevant information about the event that you can use in your listeners to perform appropriate actions.

   `MediaPlayer.EventListener` lists all the callback interfaces. Each interface displays the callback name and parameters that are returned for each event.

   For example:

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. Register your callback listeners with the `MediaPlayer` object by using `MediaPlayer.addEventListener`. 

   ```
   mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, 
    new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onStateChanged( 
    MediaPlayer.PlayerState state, 
    MediaPlayerNotification notification) {...} 
   }
   ```

## Order of playback events {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK dispatches events/notifications in generally expected sequences. Your player can implement actions based on events in the expected sequence.

The following examples show the order of some events that include playback events.

* When successfully loading a media resource through `MediaPlayer.replaceCurrentResource`, the order of events is:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` with state `MediaPlayer.PlayerState.INITIALIZING` 

1. `MediaPlayer.PlaybackEventListener.onStateChanged` with state `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>Load your media resource on the main thread. If you load a media resource on a background thread, this operation or subsequent TVSDK operations, or both, might throw an error (for example, `IllegalStateException`) and exit.

* When preparing for playback through `MediaPlayer.prepareToPlay`, the order of events is:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` with state `MediaPlayerStatus.PREPARING` 

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` if ads were inserted. 
1. `MediaPlayer.PlaybackEventListener.onStateChanged` with state `MediaPlayerStatus.PREPARED`

* For live/linear streams, during playback as the playback window advances and additional opportunities are resolved, the order of events is:

1. `MediaPlayer.PlaybackEventListener.onUpdated` 
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` if ads were inserted 
1. `MediaPlayerItemEvent.ITEM_UPDATED` 
1. `TimelineEvent.TIMELINE_UPDATED` if ads were inserted

The following example shows a typical progression of events:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK,  
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() {...} 
    @Override 
    public void onUpdated() {...} 
    @Override 
    public void onPlayStart() {...} 
    @Override 
    public void onPlayComplete() {...} 
    @Override 
    public void onSizeAvailable(long height, long width) {...} 
    @Override 
    public void onStateChanged(MediaPlayer.PlayerState state,  
      MediaPlayerNotification notification) {...} 
});
```

## Order of advertising events {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

When your playback includes advertising, TVSDK dispatches events/notifications in generally expected sequences. Your player can implement actions based on events in the expected sequence.

When playing ads, the order of events is:

* `AdPlaybackEventListener.onAdBreakStart` 
* The following are dispatched for every ad in the ad break:

    * `AdPlaybackEventListener.onAdStart` 
    * `AdPlaybackEventListener.onAdProgress` (multiple times during an ad's playback) 
    * `AdPlaybackEventListener.onAdClick` (for each click) 
    * `AdPlaybackEventListener.onAdStart` 
    * `AdPlaybackEventListener.onAdBreakComplete`

The following example shows a typical progression of ad playback events:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

When playing ads, the order of events is:

* `AdPlaybackEventListener.onAdBreakStart` 
* The following are dispatched for every ad in the ad break:

    * `AdPlaybackEventListener.onAdStart` 
    * `AdPlaybackEventListener.onAdProgress` (multiple times during an ad's playback) 
    * `AdPlaybackEventListener.onAdClick` (for each click) 
    * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

The following example shows a typical progression of ad playback events:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

## QoS events {#section_9BFF3CD7AA1C4BD6960ACF6B9C0B25CC}

TVSDK dispatches quality of service (QoS) events to notify your application about events that could influence the computation of QoS statistics, such as buffering and seeking events.

The following example shows a typical progression of these events: 

```java
mediaPlayer.addEventListener(MediaPlayer.Event.QOS,  
  new MediaPlayer.QOSEventListener(){ 
    //For buffering activity 
    @Override 
    public void onBufferStart() 
    @Override 
    public void onBufferComplete() 
    // For seeking 
    @Override 
    public void onSeekStart() 
    @Override 
    public void onSeekComplete(long adjustedTime) 
    @Override 
    public void onLoadComplete (MediaPlayerItem mediaplayeritem) 
    @Override 
    public void onLoadInfo(LoadInfo loadInfo) 
    @Override 
    public void onOperationFailed(MediaPlayerNotification.Warning warning) 
});
```

## DRM events {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK dispatches digital rights management (DRM) events in response to DRM-related operations such as when new DRM metadata becomes available. Your player can implement actions in response to these events.

To be notified about all DRM-related events, listen for `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`. TVSDK dispatches additional DRM events through the `DRMManager` class.

The following example shows a typical progression: 

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 

```

## Loader events {#section_5638F8EDACCE422A9425187484D39DCC}

Your player can implement actions based on the following events: 

|  Event  | Meaning  |
|---|---|
|  `onLoadComplete (mediaPlayerItem playerItem)`  | Media resource loading completed successfully.  |
|  `onError`  | A problem occurred with media resource loading.  |
