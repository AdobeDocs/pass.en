---
title: Defining time-based rules
description: Defining time-based rules
copied-description: yes
exl-id: ef72ee76-7d83-486d-86fe-df90c2aaca3a
---
# Defining time-based rules {#defining-time-based-rules}

Adobe Access uses “soft enforcement” of time-based license restrictions. If a time right expires during playback of a video, the default behaviour of Adobe Access is to not restrict playback until the next time the video stream is recreated (by calling `Netstream.stop()` and `Netstream.play()`).

While soft enforcement is the default behavior, you can also enable hard enforcement by performing one of the following tasks:

* Have your Video Player periodically poll the license to make sure none of the time restrictions have expired. This can be accomplished by calling `DRMManager.loadVoucher(LOCAL_ONLY).`An error code indicates that the locally-stored license is no longer valid. 
* Whenever the user clicks the Pause button, you can record the current video timestamp and then call `Netstream.stop().`When the user clicks the Play button, you can seek to the recorded location and then call `Netstream.play()`.

## Start date {#start-date}

Specifies the date after which a license is valid.

Example use case: Use an absolute date to issue content licenses ahead of the availability date of an asset, or to enforce an "embargo" period.

## End date {#end-date}

Specifies the date after which a licenses expires.

Example use case: Use an absolute expiration date to reflect the end of distribution rights. 

## Relative end date {#relative-end-date}

Specifies the license expiration date, expressed relative to the date of packaging.

Example use case: In an automated packaging process, use a single policy with this option for a series of videos to set the expiration date to 30 days relative to the date of packaging.

## License caching duration {#license-caching-duration}

Specifies the duration a license can be cached on disk in the client's local License Store without requiring reacquisition from the license server. You can alternatively specify an absolute date/time after which a license can no longer be cached.

Once the cache expiration date has passed, the license is no longer valid, and the client must request a new license from the license server.

Example use case: Use the license caching duration to specify a fixed amount of time valid for a particular license, such as in a rental use case. A 30-day rental can be specified (with license caching) to indicate the total license duration within which to consume the content.

## Playback window {#playback-window}

Specifies the duration a license is valid after the first time it is used to play protected content.

Example use case: Some business models allow a rental period of 30 days but, once playback begins, it must be completed in 48 hours. This 48-hour longevity of the license is defined as the playback window.

## Requirements for Synchronization {#requirements-for-synchronization}

Specifies the frequency in which the client will synchronize its state with the server. If the client has been issued an out-of-band license (without a license server being contacted), usage rules may specify that the client must send synchronization messages to the server in order to synchronize the client's secure time and report client state to the server.

The synchronization behavior is defined using the following parameters:

* Start Interval — Specifies how long to wait after the last successful synchronization to start another synchronization request. 
* Hard Stop Interval — (Optional). Disallow playback if a successful synchronization has not occurred in the specified amount of time. 
* Force Sync Probability — (Optional). Probability with which the client should send a synchronize message before the next start interval.

>[!NOTE]
>
>This usage rule is supported by Adobe Access clients version 3.0 and higher. The behavior on older clients depends on the minimum client version supported by the license server. See, [Minimum Client Version](../../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).
