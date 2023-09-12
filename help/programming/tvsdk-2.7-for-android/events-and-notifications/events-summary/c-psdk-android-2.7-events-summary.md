---
description: Your application can monitor the activity in your player and the changing status of the player by listening for the events that are dispatched by TVSDK.
title: Primetime player events summary
exl-id: 42489abe-ccaf-4b40-bb4b-de8547b5585a
---
# Primetime player events summary {#primetime-player-events-summary-overview}

Your application can monitor the activity in your player and the changing status of the player by listening for the events that are dispatched by TVSDK.

## Events {#events}

TVSDK notifies you when events, to which your application must respond, occur. Each event corresponds to a listener class, with a callback method that you must implement.

>[!TIP]
>
>The event codes are the constants of the `MediaPlayerEvent` enum.

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* ** Meaning ** The playback of the ad break is complete.

* ** Callback to implement ** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* ** Event code ** `AD_BREAK_COMPLETE`

## AdBreakSkippedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* ** Meaning ** An ad break was skipped during playback.

* ** Callback to implement ** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* ** Event code ** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* ** Meaning ** The playback of ad break has started.

* ** Callback to implement ** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* ** Event code ** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* ** Meaning ** An ad was clicked during playback.

* ** Callback to implement ** `onAdClicked(AdClickEvent event)`

* ** Event code ** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* ** Meaning ** The playback of the ad is complete.

* ** Callback to implement ** `onAdCompleted(AdPlaybackEvent event)`

* ** Event code ** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* ** Meaning ** Reporting progress during playback.

* ** Callback to implement ** `onAdProgress(AdPlaybackEvent event)`

* ** Event code ** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* ** Meaning ** Primetime ad decisioningad resolution is complete. This event is only applicable to VOD content.

* ** Callback to implement ** `onAdResolutionComplete()`

* ** Event code ** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* ** Meaning ** The playback of the ad has started.

* ** Callback to implement ** `onAdStarted(AdPlaybackEvent event)`

* ** Event code ** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* ** Meaning ** A new audio track has been detected.

* ** Callback to implement ** `onAudioUpdated(MediaPlayerItemEvent event)`

* ** Event code ** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* ** Meaning ** The player has started buffering.

* ** Callback to implement ** `onBufferingBegin(BufferEvent event)`

* ** Event code ** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* ** Meaning ** The player has stopped buffering.

* ** Callback to implement ** `onBufferingEnd(BufferEvent event)`

* ** Event code ** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* ** Meaning ** The buffer is prepared.

* ** Callback to implement ** `onBufferPrepared()`

* ** Event code ** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* ** Meaning ** A new caption track has been detected.

* ** Callback to implement ** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* ** Event code ** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* ** Meaning ** A new DRM metadata has been detected in the media stream.

* ** Callback to implement ** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* ** Event code ** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* ** Meaning ** A new media player item has been created.

* ** Callback to implement ** `onItemCreated(MediaPlayerItemEvent event)`

* ** Event code ** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* ** Meaning ** New load information has been created for the current item.

* ** Callback to implement ** `onLoadComplete(MediaPlayerItemEvent event)`

* ** Event code ** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* ** Meaning ** A new segment has been loaded.

* ** Callback to implement ** `onLoadInformation(LoadInformationEvent event)`

* ** Event code ** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* ** Meaning ** The main manifest or playlist has been updated.

* ** Callback to implement ** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* ** Event code ** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* ** Meaning ** The operation has failed.

* ** Callback to implement ** `onNotification(NotificationEvent event)`

* ** Event code ** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* ** Meaning ** The playback range has been updated.

* ** Callback to implement ** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* ** Event code ** `PLAYBACK_RANGE_UPDATED`

## PlaybackRatePlayingEventListener {#section_548A489ABED44F89BDF29DB9EDD348C5}

* ** Meaning ** A new playback rate is visible on the screen.

* ** Callback to implement ** `onRatePlaying(PlaybackRateEvent event)`

* ** Event code ** `RATE_PLAYING`

## PlaybackRateSelectedEventListener {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* ** Meaning ** The MediaPlayer's rate attribute has been set.

* ** Callback to implement ** `onRateSelected(PlaybackRateEvent event)`

* ** Event code ** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* ** Meaning ** The playback has started.

* ** Callback to implement ** `onPlayStart()`

* ** Event code ** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* ** Meaning ** The MediaPlayer's current profile has changed.

* ** Callback to implement ** `onProfileChanged(ProfileEvent event)`

* ** Event code ** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* ** Meaning ** Playback reached a timeline reservation.

* ** Callback to implement ** `onReservationReached(ReservationEvent event)`

* ** Event code ** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* ** Meaning ** Seek operation started.

* ** Callback to implement ** `onSeekBegin(SeekEvent event)`

* ** Event code ** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* ** Meaning ** The seek operation has finished.

* ** Callback to implement ** `onSeekEnd(SeekEvent event)`

* ** Event code ** `SEEK_END`

## SeekPositionAdjustedEventListener {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* ** Meaning ** The seek position has been adjusted because of internal playback rules or external business rules.

* ** Callback to implement ** `onPositionAdjusted(SeekEvent event)`

* ** Event code ** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* ** Meaning ** The size of the media is available.

* ** Callback to implement ** `onSizeAvailable(SizeAvailableEvent event)`

* ** Event code ** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* ** Meaning ** The MediaPlayer state has changed.

* ** Callback to implement ** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* ** Event code ** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* ** Meaning ** The playhead has changed.

* ** Callback to implement ** `onTimeChanged(TimeChangeEvent event)`

* ** Event code ** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* ** Meaning ** The operation is complete with the time taken for the operation.

* ** Callback to implement ** `onTimedEvent(TimedEventEvent event)`

* ** Event code ** `TIMED_EVENT`

## TimelineMetadataAddedInBackgroundEventListener {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* ** Meaning ** A new timed metadata hsa been added to an item in background.

* ** Callback to implement ** `onTimedMetadata(TimedMetadataEvent event)`

* ** Event code ** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* ** Meaning ** A new timed metadata was detected in the media stream.

* ** Callback to implement ** `onTimedMetadata(TimedMetadataEvent event)`

* ** Event code ** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* ** Meaning ** The timeline has been modified. Ads might have been added to or removed from the timeline.

* ** Callback to implement ** `onTimelineUpdated(TimelineEvent event)`

* ** Event code ** `TIMELINE_UPDATED`
