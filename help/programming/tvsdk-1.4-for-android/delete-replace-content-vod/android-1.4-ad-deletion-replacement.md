---
description: These changes in the Android TVSDK API support ad deletion and replacement.
title: Ad deletion and replacement API changes
exl-id: bde8bd6e-0afe-42d0-b716-f33f75de757e
---
# Ad deletion and replacement API changes{#ad-deletion-and-replacement-api-changes}

These changes in the Android TVSDK API support ad deletion and replacement.

* `AdSignalingMode` New Custom Time Range Ad Signaling Mode 

* `AdvertisingMetadata` New `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: Sets the time ranges to mark, delete, or replace when processing metadata 

* `ContentResolver`

    * New `public final boolean canResolve(PlacementOpportunity placementOpportunity)` 
    * New `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* New `ContentRemoval` class

  `TimelineOperation` class that defines the time range to be removed from the timeline 

* `AuditudeResolver`

    * New `private LinkedList<AuditudeRequest> _requestQueue` 
    * New `void startConsumer()`: Starts processing the Primetime ad decisioning request queue and ensures that each request is issued at `MIN_INIT_REQUEST_INTERVAL` intervals 
    
    * New `processReplacementRange()`: Extracts time-ranges from the ad metadata and generates `PlacementInformations`, and creates a Primetime ad decisioning request containing the `PlacementInformations`.
    
    * New `canDoResolver()`: Checks if placement opportunity has Primetime ad decisioning metadata

* New `CustomRangeHelper` Helper class that extracts time range metadata from ad metadata, and removes subsets/overlaps/invalid time ranges. 

* New `DeleteContentResolver` Content resolver that resolves Placement opportunities of `PlacementInformation.Mode.DELETE` 

* New `NopTimelineOperation` New timeline operation for when no ad break placement or replacement needs to be done. This class is used to distinguish between this and when an error occurs during the resolving process. 

* `TimelineOperationQueue` Checks if the Timeline Operation is a `NopTimelineOperation` before processing. 

* `CustomAdMarkersContentResolver` New `canDoResolve()`: Checks if a placement opportunity is of type `Mode.MARK` 

* `MetadataResolver` New `canDoResolve()`: Checks if a placement opportunity is of type `Mode.INSERT` 

* `DefaultMetadataKeys` New `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")` 

* `PlacementInformation`

    * New Mode `enum (INSERT, DELETE, REPLACE, MARK)`
    * New Type `CUSTOM_TIME_RANGES`

* `TimeRange` New `compareTo(TimeRange timeRange)`: So can sort TimeRanges based on begin time 

* New `ReplacementTimeRange` Extends the `TimeRange` class that represents a replacement timerange, with a `begin`, `end`, and `replacement-duration` parameter. 

* `TimeRangeCollection`

    * New `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES` 
    * Renamed `CUSTOM_AD_MARKERS` to `MARK_RANGES` 
    
    * Modified `toMetadata(Metadata options)` to put delete/mark/replace ranges into ad metadata.

* `MediaPlayerNotification`

    * New `UNDEFINED_TIME_RANGES`: When the ad signaling mode is Server Map or Manifest Cues, and replace ranges are also in the ad metadata, replace ranges are ignored. 
    * New `REPLACE_RANGES_NOT_AVAILABLE`: When ad signaling mode is Custom Time Ranges and replace ranges are not available, a warning will be dispatched.

* `AdvertisingFactory` New `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)` 

* `DefaultAdvertisingFactory` New `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)` 

* `DefaultContentResolverFactory` New `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)` 

* `DefaultMediaPlayer`

    * In `prepareToPlay()`: Makes an initial seek to 0, because if range `[0,n]` is deleted, the media player will not automatically play. 
    
    * In `prepareToPlay()`: Loops through the list of initial placement informations for `mediaplayerclient` to resolve. 
    
    * In `extractAdSignalingMode()`: Accommodate for the new Custom Time Range mode. 
    * New `private static List<PlacementInformation> createInitalPlacementInformations()`: Generates the initial placement informations for the ad signaling mode and content resolvers (derived from ad metadata). 
    * In `ContentPlacementCompletedListener`: Checks to see if `mediaPlayerClient` is `doneInitialResolving` before calling `endAdResolving`.

* `MediaPlayerClient`

    * New `List<ContentResolver> _contentResolvers` 
    * New `int _reservations` 
    * New `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Looks up which resolver can resolve the `PlacementOpportunity`. 
    
    * Modified code to create multiple content resolvers. 
    * New `public boolean doneInitialResolving()`: Checks if there are any opportunities left to be resolved.

* `VideoEngineTimeline`

    * New `removeContent(TimelineOperation timelineOperation)`: Removes a given range of content from timeline. 
    * New `removeContentByLocalTime(long begin, long end)`: Removes content by local time given `begin` and `end`.

* `DefaultOpportunityDetectorFactory` Modified `createOpportunityDetector`: For VOD streams, only return a new `SpliceOutOpportunityDetector` if there are no MARK or REPLACE ranges (as those ranges have priority over the signaling mode).
