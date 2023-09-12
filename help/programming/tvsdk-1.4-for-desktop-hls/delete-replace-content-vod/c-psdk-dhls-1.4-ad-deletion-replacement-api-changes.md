---
description: These changes in TVSDK support ad deletion and replacement.
title: Ad deletion and replacement API changes
exl-id: 3cf63353-741b-41f4-93fd-609b69f7c3af
---
# Ad deletion and replacement API changes {#ad-deletion-and-replacement-api-changes}

These changes in TVSDK support ad deletion and replacement.

* `AdSignalingMode` Added `CUSTOM_RANGES` signaling mode. 

* `OpportunityGenerator`  `extractAdSignalingMode()` - Set `AdSignalingMode.CUSTOM_RANGES` if replace ranges are in the metadata. 

* `PlacementType` Added `CUSTOM_RANGE` type. 

* `PlacementMode`

    * Added `DELETE` mode. 
    * Added `MARK` mode 
    * Added `FreeReplace` mode - This mode has a duration but is a pure insertion

* `TimeRange` No longer a `final` class 

* Added `ReplaceTimeRange()` method

  Extends `TimeRange` to have a `replacementDuration` property. For the MARK and DELETE cases, `replacementDuration` is 0. 

* `TimeRangeCollection`

    * Added `toReplaceMetadata()` utility function to extract `timeRanges`. 
    
    * Modified to work with `DELETE` and `REPLACE` 
    
    * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

    * Added `createCustomTimeRangesFrom()` - Creates metadata for MARK/DELETE/REPLACE use cases from the JSON file. 
    * Removed `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

    * Added `CUSTOM_DELETE_RANGES_METADATA_KEY` 
    * Added `CUSTOM_REPLACE_RANGES_METADATA_KEY` 
    * `CUSTOM_AD_MARKERS_METADATA_KEY` (did not change)

* `DefaultContentFactory`

    * `doRetrieveGenerators()`

        * Added `CustomRangesOpportunityGenerator` for when the metadata contains custom ranges

    * `doRetrieveResolvers()`

        * Add `CustomRangeResolver` for when DELETE and REPLACE custom ranges are present in the metadata 
        * Moved `CustomAdMarkerResolver` ahead of `AuditudeResolver`

* Added `CustomRangeOpportunityGenerator`

    * `doUpdate()` Leaves empty - no Update, VOD 
    * `doProcess()` Creates a new placement of a new type `Placement.Delete_Range` 
    
    * Added `CustomRangeOppotunityGenerator` to the top of the generators list in `DefaultContentFactory`, so delete ranges are processed before ad insertions. 
    
    * Added `createCustomRangeOpportunities` to create all the opportunities

      MARK - One opportunity for each valid mark range of `PlacementType.CUSTOM_RANGE` and `PlacementMode.MARK`

      DELETE - One opportunity for each valid delete range of `PlacementType.CUSTOM_RANGE` and `PlacementMode.DELETE`

      REPLACE - Two opportunities for each valid replace range:

        1. A delete range opportunity of `PlacementType.CUSTOM_RANGE` and `PlacementMode.DELETE`. 
        
        1. An Primetime ad decisioning ad opportunity of `PlacementType.MID_ROLL` or `PlacementType.PRE_ROLL` and `PlacementMode.FREEREPLACE`

* Added `CustomRangeResolver`:

    * `doCanResolve()` returns `true` for delete ranges. 
    
    * Added `createDeleteRangeOperation()` to create `DeleteRange` for the placement

* Added `CustomRangeHelper`:

    * Common utility class to extract Mark/Delete/Replace `timeRanges` and process them. 
    * Added `extractCustomRangesMetadata()` 
    * Added `extractCustomRanges()` 
    * Added `mergeRanges()` - Resolves conflicts and subsets/merges

* `MediaPlayerTimeline`:

    * ">In `executeOperation()`, if the operation is `DeleteRange`, added call to remove method in the operation 
    
    * In `executeOperation()`, if the operation is `NOPTimelineOperation` (empty `AdBreaks` coming back from server), added call to clear. 
    
    * Added `onDeleteRangeComplete()` 
    * Added `removeRange()` 
    * In `adjustPlacement()`, for `PlacementMode.FREEREPLACE` mode, zeroed out the duration. This duration is needed earlier when requesting `AdBreaks`, at this point it needs to be zero to be pure insertion.

* `VideoEngineTimeline` Added `removeC3Ad()` - call `removeByLocalTime()` for delete ranges 

* `AdSignalingModeGenerator`

    * `doConfigure()` - Do not resolve if no opportunity is generated 
    * `createInitialOpportunity()` - Do not generate initial opportunity for `AdSignalingMode.CUSTOM_RANGE`. The `CustomRangeOpportunityGenerator` covers this already.

* `DeleteRange`

    * Extends `TimelineOperation`. 
    * Created by `CustomRangeResolver` for delete and replacement (the deletion part of replacement)

* `AuditudeConstant`

    * `MAX_PLACEMENTS_PER_REQUEST 1->5` - allow packing 
    * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` The `accepts()` method was modified to allow packing of different placement type (pre-roll, mid-roll, post-roll) 

* `AuditudeRequestHelper` Bug fixes to allow server override of Ad parameters 

* `AuditudeResolver` The `canBePacked()` method was changed to allow packing 

* `CustomAdResolver` The `timeRange` extraction functions have been removed. We get one placement at a time, and turn that into a `AdBreakPlacement timelineOperation`.
