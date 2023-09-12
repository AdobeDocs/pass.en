---
title: Time-based rules
description: Time-based rules
copied-description: yes
exl-id: 02a5c10d-13f5-4482-b525-bf6a1ec9dcf0
---
# Time-based rules {#time-based-rules}

Primetime DRM uses "soft enforcement" of time-based license restrictions. If a time right expires during playback of a video, the default behaviour of Primetime DRM is to not restrict playback until the next time the video stream is recreated (by calling `Netstream.stop()` and `Netstream.play()`).

While soft enforcement is the default behavior, you can also enable hard enforcement by performing one of the following tasks:

* Have your Video Player periodically poll the license to make sure none of the time restrictions have expired. This can be accomplished by calling `DRMManager.loadVoucher(LOCAL_ONLY).` An error code indicates that the locally-stored license is no longer valid. 
* Whenever the user clicks **[!UICONTROL Pause]**, you can record the current video timestamp and then call `Netstream.stop()`. When the user clicks the Play button, you can seek to the recorded location and then call `Netstream.play()`.

## Start date {#start-date}

The start date specifies the date after which a license is valid.

Example use case: Use an absolute date to issue content licenses ahead of the availability date of an asset, or to enforce an "embargo" period.

## End date {#end-date}

The end date specifies the date after which a license expires.

Example use case: Use an absolute expiration date to reflect the end of distribution rights.

## Relative end date {#relative-end-date}

The relative end date specifies the license expiration date, which is expressed relative to the date of packaging, not relative to the date when the license was issued.

Example use case: In an automated packaging process, use a single Primetime DRM policy with this option for a series of videos, to set the expiration date to 30 days relative to the date of packaging.

## License caching duration{#license-caching-duration}

The license caching duration specifies how long a license can be cached on disk in the client's local License Store without requiring reacquisition from the license server. Alternatively, you can specify an absolute date and time after which a license can no longer be cached.

Once the cache expiration date has passed, the license is no longer valid, and the client must request a new license from the license server.

Example use case: Use the license caching duration to specify a fixed amount of time valid for a particular license, such as in a rental use case. You can specify a 30-day rental (with license caching) to indicate the total license duration within which to consume the content.

## Playback window {#playback-window}

The playback window specifies the duration a license is valid after the first time it is used to play protected content.

Example use case: Some business models allow a rental period of 30 days but, once playback begins, playback must be completed in 48 hours. In this case, the 48-hour duration of the license is the playback window.

**From version 5.3 forward** - The playback window also supports the option of enabling or disabling Hard Stop, which indicates whether the decryption context for playback should stop at the expiration of the playback window (enabled) or continue despite expiration (disabled).

>[!NOTE]
>
>The hard stop option does not work properly with Playback Window if used in conjunction with it (Playback Window will not be honored). Playing content with Playback window without secure stop does respect the playback window restriction.
