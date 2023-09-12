---
description: Your application can monitor the activity in your player and the changing status of the player by listening for the events that are dispatched by TVSDK.
title: Primetime player events summary
exl-id: 3912f140-1600-41fb-9dc4-306646b7cd85
---
# Primetime player events summary {#primetime-player-events-summary}

Your application can monitor the activity in your player and the changing status of the player by listening for the events that are dispatched by TVSDK.

## Events {#events}

TVSDK notifies you when events, to which your application must respond, occur. Each event corresponds to a listener class, with a callback method that you must implement.

>[!TIP]
>
>The event codes are the constants of the `MediaPlayerEvent` enum.

`AdBreakCompletedEventListener`

* **Meaning** The playback of the ad break is complete.

* **Callback to implement** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Event code** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **Meaning** An ad break was skipped during playback.

* **Callback to implement** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Event code** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **Meaning** The playback of ad break has started.

* **Callback to implement** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Event code** `AD_BREAK_START`

`AdClickedEventListener`

* **Meaning** An ad was clicked during playback.

* **Callback to implement** `onAdClicked(AdClickEvent event)`
* **Event code** `AD_CLICK`

`AdCompletedEventListener`

* **Meaning** The playback of the ad is complete.

* **Callback to implement** `onAdCompleted(AdPlaybackEvent event)`

* **Event code** `AD_COMPLETE`

`AdProgressEventListener`

* **Meaning** Reporting progress during playback.

* **Callback to implement** `onAdProgress(AdPlaybackEvent event)`

* **Event code** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **Meaning** Primetime ad decisioningad resolution is complete. This event is only applicable to VOD content.

* **Callback to implement** `onAdResolutionComplete()`

* **Event code** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **Meaning** The playback of the ad has started.

* **Callback to implement** `onAdStarted(AdPlaybackEvent event)`

* **Event code** `AD_START`

`AudioUpdatedEventListener` 

* **Meaning** A new audio track has been detected.

* **Callback to implement** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Event code** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **Meaning** The player has started buffering.

* **Callback to implement** `onBufferingBegin(BufferEvent event)`

* **Event code** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **Meaning** The player has stopped buffering.

* **Callback to implement** `onBufferingEnd(BufferEvent event)`

* **Event code** `BUFFERING_END`

`BufferPreparedEventListener`

* **Meaning** The buffer is prepared.

* **Callback to implement** `onBufferPrepared()`

* **Event code** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **Meaning** A new caption track has been detected.

* **Callback to implement** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Event code** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **Meaning** A new DRM metadata has been detected in the media stream.

* **Callback to implement** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Event code** `DRM_METADATA`

`ItemCreatedEventListener`

* **Meaning** A new media player item has been created.

* **Callback to implement** `onItemCreated(MediaPlayerItemEvent event)`

* **Event code** `ITEM_CREATED`

`ItemLoadCompleteEventListener` 

* **Meaning** New load information has been created for the current item.

* **Callback to implement** `onLoadComplete(MediaPlayerItemEvent event)`

* **Event code** `ITEM_UPDATED`

`LoadInformationEventListener`

* **Meaning** A new segment has been loaded.

* **Callback to implement** `onLoadInformation(LoadInformationEvent event)`

* **Event code** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **Meaning** The main manifest or playlist has been updated.

* **Callback to implement** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Event code** `MANIFEST_UPDATED`

`NotificationEventListener`

* **Meaning** The operation has failed.

* **Callback to implement** `onNotification(NotificationEvent event)`

* **Event code** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **Meaning** The playback range has been updated.

* **Callback to implement** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Event code** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **Meaning** A new playback rate is visible on the screen.

* **Callback to implement** `onRatePlaying(PlaybackRateEvent event)`

* **Event code** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **Meaning** The MediaPlayer's rate attribute has been set.

* **Callback to implement** `onRateSelected(PlaybackRateEvent event)`

* **Event code** `RATE_SELECTED`

`PlayStartEventListener`

* **Meaning** The playback has started.

* **Callback to implement** `onPlayStart()`

* **Event code** `PLAY_START`

`ProfileChangeEventListener`

* **Meaning** The MediaPlayer's current profile has changed.

* **Callback to implement** `onProfileChanged(ProfileEvent event)`

* **Event code** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **Meaning** Playback reached a timeline reservation.

* **Callback to implement** `onReservationReached(ReservationEvent event)`

* **Event code** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **Meaning** Seek operation started.

* **Callback to implement** `onSeekBegin(SeekEvent event)`

* **Event code** `SEEK_BEGIN`

`SeekEndEventListener`

* **Meaning** The seek operation has finished.

* **Callback to implement** `onSeekEnd(SeekEvent event)`

* **Event code** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **Meaning** The seek position has been adjusted because of internal playback rules or external business rules.

* **Callback to implement** `onPositionAdjusted(SeekEvent event)`

* **Event code** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **Meaning** The size of the media is available.

* **Callback to implement** `onSizeAvailable(SizeAvailableEvent event)`

* **Event code** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **Meaning** The MediaPlayer state has changed.

* **Callback to implement** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Event code** `STATUS_CHANGED`

`TimeChangeEventListener`

* **Meaning** The playhead has changed.

* **Callback to implement** `onTimeChanged(TimeChangeEvent event)`

* **Event code** `TIME_CHANGED`

`TimedEventEventListener`

* **Meaning** The operation is complete with the time taken for the operation.

* **Callback to implement** `onTimedEvent(TimedEventEvent event)`

* **Event code** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **Meaning** A new timed metadata hsa been added to an item in background.

* **Callback to implement** `onTimedMetadata(TimedMetadataEvent event)`

* **Event code** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **Meaning** A new timed metadata was detected in the media stream.

* **Callback to implement** `onTimedMetadata(TimedMetadataEvent event)`

* **Event code** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **Meaning** The timeline has been modified. Ads might have been added to or removed from the timeline.

* **Callback to implement** `onTimelineUpdated(TimelineEvent event)`

* **Event code** `TIMELINE_UPDATED`
