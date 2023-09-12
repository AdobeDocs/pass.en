---
description: Event handlers enable you to respond to TVSDK events.
title: Implement event listeners and callbacks
exl-id: c8825a6c-3d48-412f-81f5-542c7731a122
---
# Implement event listeners and callbacks {#implement-event-listeners-and-callbacks}

Event handlers enable you to respond to TVSDK events.

When an event occurs, TVSDK's event mechanism calls your registered event handler, passing it the event information.

TVSDK defines listeners as public internal interfaces inside the `MediaPlayer` interface.

Your application must implement event listeners for any TVSDK events that affect your application.

1. Determine which events your application must listen for.

    * Required events: Listen for all playback events.     
    
      >[!IMPORTANT]
      >
      >Listen for the status change event, which occurs when the player's status changes in ways that you need to know. The information it provides includes errors that might affect what your player can do next.

    * For other events, depending on your application, see  events-summary .

1. Implement and add an event listener for each event. 

   >[!NOTE]
   >
   >For most events TVSDK passes arguments to the event listeners. Such values provide information about the event that can help you decide what to do next. The `MediaPlayerEvent` enumeration lists all the events that `MediaPlayer` dispatches. For more information, see  events-summary .

   For example, if `mPlayer` is an instance of `MediaPlayer`, here is how you might add and structure an event listener:

   ```java
   mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() { 
       @Override 
       public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
           event.getMetadata(); 
           if (event.getMetadata() != null) {/* Do something */} 
           if (event.getStatus() == MediaPlayerStatus.IDLE) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.INITIALIZED) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.PREPARED) {/* Do something */} 
       } 
   }); 
   
   ```

## Order of playback events {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

TVSDK dispatches events/notifications in generally expected sequences. Your player can implement actions based on events in the expected sequence.

The following examples show the order of some events that occur during playback.

When successfully loading a media resource through `MediaPlayer.replaceCurrentResource`, the order of events is:

1. `MediaPlayerEvent.STATUS_CHANGED` with status `MediaPlayerStatus.INITIALIZING` 

1. `MediaPlayerEvent.STATUS_CHANGED` with status `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>Load your media resource on the main thread. If you load a media resource on a background thread, this operation or subsequent operations might throw an error, such as `MediaPlayerException`, and exit.

When preparing for playback through `MediaPlayer.prepareToPlay`, the order of events is:

1. `MediaPlayerEvent.STATUS_CHANGED` with status `MediaPlayerStatus.PREPARING` 

1. `MediaPlayerEvent.TIMELINE_UPDATED` if ads were inserted. 
1. `MediaPlayerEvent.STATUS_CHANGED` with status `MediaPlayerStatus.PREPARED`

For live/linear streams, during playback as the playback window advances and additional opportunities are resolved, the order of events is:

1. `MediaPlayerEvent.ITEM_UPDATED` 
1. `MediaPlayerEvent.TIMELINE_UPDATED` if ads were inserted

## Order of advertising events {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

When your playback includes advertising, TVSDK dispatches events/notifications in generally expected sequences. Your player can implement actions based on events within the expected sequence.

When playing ads, the order of events is:

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

The following events are dispatched for every ad within the ad break:

* `MediaPlayerEvent.AD_BREAK_START` 
* `MediaPlayerEvent.AD_START` 
* `MediaPlayerEvent.AD_PROGRESS (multiple times)` 
* `MediaPlayerEvent.AD_CLICK (for each click)` 
* `MediaPlayerEvent.AD_COMPLETE` 
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

The following example shows a typical progression of ad playback events:

```
mediaPlayer.addEventListener(MediaPlayerEvent.AD_RESOLUTION_COMPLETE, new AdResolutionCompleteEventListener() { 
        @Override 
        public void onAdResolutionComplete() { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_START, new AdBreakStartedEventListener() { 
         @Override 
        public void onAdBreakStarted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_START, new AdStartedEventListener() { 
         @Override 
        public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_PROGRESS, new AdProgressEventListener() { 
         @Override 
         public void onAdProgress(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_COMPLETE, new AdCompletedEventListener() { 
         @Override 
         public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_COMPLETE, new AdBreakCompletedEventListener() { 
         @Override 
         public void onAdBreakCompleted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
Below event is for tracking ad clicks. 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_CLICK, new AdClickedEventListener() { 
         @Override 
         public void onAdClicked(AdClickEvent adClickEvent) { ... } 
    });
```

## Order of DRM events {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

TVSDK dispatches digital rights management (DRM) events in response to DRM-related operations such as when new DRM metadata becomes available. Your player can implement actions in response to these events.

To be notified about all DRM-related events, listen for `MediaPlayerEvent.DRM_METADATA`. TVSDK dispatches additional DRM events through the `DRMManager` class.

## Order of loader events {#section_5638F8EDACCE422A9425187484D39DCC}

TVSDK dispatches `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` when loader events occur.
