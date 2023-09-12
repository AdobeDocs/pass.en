---
description: The methods in the MediaPlayerItem class allow you to obtain information about the content stream represented by a loaded MediaResource.
title: MediaPlayerItem methods for accessing MediaResource information
exl-id: d6a547f3-0267-4a49-93a4-628b4879aef4
---
# MediaPlayerItem methods for accessing MediaResource information {#mediaplayeritem-methods-for-accessing-mediaresource-information}

The methods in the MediaPlayerItem class allow you to obtain information about the content stream represented by a loaded MediaResource.

| Method | Description |
|--- |--- |
|**Ad tags**||
|List`<String>` getAdTags()|Provides the list of ad tags that are used for the ad placement process.|
|**Live stream**||
|boolean isLive();|True if the stream is live; false if it is VOD.|
|**DRM protected**||
|boolean isProtected();|True if the stream is DRM protected.|
|List`<DRMMetadataInfo>` getDRMMetadataInfos();|Lists all the DRM metadata objects discovered in the manifest.|
|**Closed captions**||
|boolean hasClosedCaptions();|True if closed-caption tracks are available.|
|List`<ClosedCaptionsTrack>` getClosedCationsTracks();|Provides a list of available closed-caption tracks.|
|ClosedCaptionsTrack get SelectedClosedCaptionsTrack();|Retrieves the current closed caption track selected with  SelectClosedCaptionsTrack .|
|selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack)|Sets a closed-caption track to be the current closed-caption track.|
|**Alternate audio tracks**||
|boolean hasAlternateAudio();|True if the stream has alternate audio tracks. Note:  The main (default) audio track is also part of the alternate audio track list.  TVSDK for Android considers the main audio track to be one of the items in the alternate audio track list. Because of this, the only case where  MediaPlayerItem.hasAlternateAudio  returns false is when the stream has no audio at all. If the content has only one audio track, this method returns true, and  `MediaPlayerItem.getAudioTracks`  returns a list with a single element (the default audio track).|
|List`<AudioTrack>` getAudioTracks();|Provides a list of available alternate audio tracks.|
|AudioTrack getSelectedAudioTrack();|Retrieves the audio track selected with  selectAudioTrack .|
|selectAudioTrack ( AudioTrack audioTrack )|Selects an audio track to be the current audio track.|
|**Timed metadata**||
|boolean hasTimedMetadata();|True if the stream has associated timed metadata.|
|List`<TimedMetadata>` getTimedMetadata();|Provides a list of the timed metadata objects associated with the stream.|
|**Multiple profiles (bit rates)**|
|boolean isDynamic();|True if the stream is a multiple bit rate (MBR) stream.|
|List`<Profile>` getProfiles();|Provides a list of the associated bit rate profiles. For each profile, you can retrieve its bit rate and the height and width of the profile.|
|Profile getSelectedProfile()|Retrieves the currently selected profile.|
|**Trick play**||
|boolean isTrickPlaySupported();|True if the player supports fast forward, rewind, and resume.|
|List`< Float>` getAvailablePlaybackRates()|Provides the list of available playback rates in the context of the trick-play feature.|
|Float getSelectedPlaybackRate()|Retrieves the currently selected playback rate.|
|MediaPlayerItemConfig getConfig()|Returns the  MediaPlayerItemConfig  instance associated with this item.|
|**Media resource**||
|MediaResource getResource();|Returns the media resource associated with this item.|
|int getResourceId()|Returns the media identifier associated with this item. This ID is set when the item is loaded using  MediaPlayerItemLoader.load .|
