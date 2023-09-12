---
description: TVSDK supports the programmatic deleting and replacing of ad content in VOD streams.
title: Custom time range operations
exl-id: 10aa3609-d5d0-49e2-959f-d72d8dbd6ef4
---
# Custom time range operations {#custom-time-range-operations}

TVSDK supports the programmatic deleting and replacing of ad content in VOD streams.

The delete and replace feature extends the custom ad markers feature. Custom ad markers mark sections of the main content as ad-related content periods. In addition to marking these time ranges, you can also delete and replace time ranges.

Ad deletion and replacement is implemented with `TimeRange` elements that identify different types of time ranges in a VOD stream: mark, delete, and replace. For each of these custom time range types, you can perform corresponding operations, including deleting and replacing ad content.

For ad deletion and replacement, TVSDK uses the following *custom time range operation* modes:

* **MARK**
  (These were referred to as custom ad markers in previous versions of TVSDK). They mark the beginning and ending times for ads that are already placed into the VOD stream. When there are time range markers of type MARK in the stream, an initial placement of `Mode.MARK` is generated and resolved by the `CustomAdMarkersContentResolver`. No ads are inserted.

* **DELETE**
  For DELETE time ranges, an initial `placementInformation` of type `Mode.DELETE` is created and resolved by the corresponding `DeleteContentResolver`. `ContentRemoval` is a new `timelineOperation` that defines the ranges to be removed from the timeline. TVSDK uses `removeByLocalTime` from the Adobe Video Engine (AVE) API to facilitate that operation. If there are DELETE ranges and Adobe Primetime ad decisioning (previously known as Auditude) metadata, the ranges are deleted first, then the `AuditudeResolver` resolves ads using the normal Adobe Primetime ad decisioning workflow.

* **REPLACE**
  For REPLACE time ranges, two initial `placementInformations` are created, one `Mode.DELETE` and one `Mode.REPLACE`. The `DeleteContentResolver` deletes the time ranges first and then the `AuditudeResolver` inserts ads of the specified `replaceDuration` into the timeline. If no `replaceDuration` is specified, the server determines what to insert.

To support these custom time range operations, TVSDK provides the following:

* Multiple content resolvers

  A stream can have multiple content resolvers based on the ad signaling mode and ad metadata. The behavior changes with different combinations of ad signaling modes and ad metadata. 
* Multiple initial `PlacementInformations` The `DefaultMediaPlayer` creates a list of initial `PlacementInformations` based on the ad signaling mode and ad metadata to be resolved by the `MediaPlayerClient`. 

* New ad signaling mode: Custom time ranges

  Ads are placed based on Time Range data from an external source (such as a JSON file).
