---
description: The methods in the MediaPlayerItem class allow you to obtain information about the content stream represented by a loaded MediaResource.
title: MediaPlayer methods for accessing MediaResource information
exl-id: 74e453d6-233e-4146-9f63-ab6919a4ba39
---
# MediaPlayer methods for accessing MediaResource information{#mediaplayer-methods-for-accessing-mediaresource-information}

The methods in the MediaPlayerItem class allow you to obtain information about the content stream represented by a loaded MediaResource.

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Method </th> 
   <th colname="3" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Live stream </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isLive():Boolean; </span> </td> 
   <td colname="3"> <p>True if the stream is live; false if it is VOD. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM protected</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isProtected():Boolean; </span> </td> 
   <td colname="3"> <p>True if the stream is DRM protected. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get drmMetadataInfos(): Vector.&lt;DRMMetadataInfo&gt;; </span> </td> 
   <td colname="3"> <p>Lists all the DRM metadata objects discovered in the manifest. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Closed captions</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasClosedCaptions():Boolean; </span> </td> 
   <td colname="3"> <p>True if closed-caption tracks are available. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get closedCaptionsTracks():Vector.&lt;ClosedCaptionsTrack&gt;; </span> </td> 
   <td colname="3"> <p>Provides a list of available closed-caption tracks. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get selectedClosedCaptionsTrack():ClosedCaptionsTrack </span> </td> 
   <td colname="3"> <p>Retrieves the current closed caption track selected with <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack (closedCaptionsTrack: com.adobe.mediacore.info:ClosedCaptionsTrack ) </span> </td> 
   <td colname="3"> <p>Sets a closed-caption track to be the current closed-caption track. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Alternate audio tracks </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasAlternateAudio():Boolean; </span> </td> 
   <td colname="3"> <p>True if the stream has alternate audio tracks. </p> <p>Tip:  The main (default) audio track is also part of the alternate audio track list. </p> <p>TVSDK for Desktop&nbsp;HLS considers the main audio track to be one of the items in the alternate audio track list. Because of this, the only case where <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> returns false is when the stream has no audio at all. If the content has only one audio track, this method returns true, and <span class="codeph"> get AudioTracks </span> returns a list with a single element (the default audio track). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get audioTracks():Vector.&lt;AudioTrack&gt;; </span> </td> 
   <td colname="3"> Provides a list of available alternate audio tracks. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get audioTracks():Vector.&lt;AudioTrack&gt;; </span> </td> 
   <td colname="3"> <p>Provides a list of available alternate audio tracks. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get selectedAudioTrack():AudioTrack; </span> </td> 
   <td colname="3"> <p>Retrieves the audio track selected with <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack: AudioTrack ) </span> </td> 
   <td colname="3"> <p>Selects an audio track to be the current audio track. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Timed metadata</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get hasTimedMetadata():Boolean; </span> </td> 
   <td colname="3"> <p>True if the stream has associated timed metadata. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get timedMetadata():Vector.&lt;TimedMetadata&gt;; </span> </td> 
   <td colname="3"> <p>Provides a list of the timed metadata objects associated with the stream. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isDynamic():Boolean; </span> </td> 
   <td colname="3"> <p>True if the stream is a multiple bit rate (MBR) stream. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get profiles():Vector.&lt;Profile&gt;; </span> </td> 
   <td colname="3"> <p>Provides a list of the associated bit rate profiles. For each profile, you can retrieve its bit rate and the height and width of the profile. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Trick play </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get isTrickPlaySupported():Boolean; </span> </td> 
   <td colname="3"> <p>True if the player supports fast forward, rewind, and resume. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get availablePlaybackRates():Vector.&lt;Number&gt; </span> </td> 
   <td colname="3"> <p>Provides the list of available playback rates in the context of the trick-play feature. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Media player </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get player():MediaPlayer </span> </td> 
   <td colname="3"> <p>Returns the media player currently associated with this player. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Media resource</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> function get resource():MediaResource; </span> </td> 
   <td colname="3"> <p>Returns the media resource associated with this item. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> function get resourceId():int </span> </td> 
   <td colname="3"> <p>Returns the media identifier associated with this item. </p> </td> 
  </tr> 
 </tbody> 
</table>
