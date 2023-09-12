---
description: TVSDK supports the programmatic deleting and replacing of ad content in VOD streams.
title: Delete and replace ads in VOD streams
exl-id: 44d75250-23ee-4ce3-a0c1-59bd488a5aba
---
# Ad deletion and replacement API changes {#ad-deletion-and-replacement-api-changes}

TVSDK supports the programmatic deleting and replacing of ad content in VOD streams.

The delete and replace feature extends the custom ad markers feature. Custom ad markers mark sections of the main content as ad-related content periods. In addition to marking these time ranges, you can also delete and replace time ranges.

The following changes in TVSDK support ad deletion and replacement.

**New APIs**

* `PTTimeRangeCollection` is a public class that defines a predefined set of ranges and a type:

    * `property PTTimeRangeCollectionType type` indicates the type of time range. 
    * `property NSArray* ranges` is used to set the time ranges.

      The expected type of objects in the array are `PTReplacementTimeRange` or `CMTimeRange`.

      >[!TIP]
      >
      >All the objects of the array must be the same type.

    * `PTTimeRangeCollectionType` is an enum that defines the behavior for the ranges that are defined in the `PTTimeRangeCollection`:

        * `PTTimeRangeCollectionTypeMarkRanges`: The type of the ranges is *Mark*. The ranges are used for marking the ranges in the content as Ads. 
        
        * `PTTimeRangeCollectionTypeDeleteRanges`: The type of the ranges is Delete. The defined ranges are removed from the main content before ad insertion. 
        * `PTTimeRangeCollectionTypeReplaceRanges`: The type of the ranges is Replace. The defined ranges are replaced from the main with Ads (Ad signaling mode is set to `PTAdSignalingModeCustomTimeRanges`).

* `PTReplacementTimeRange` - New public class that defines a single range of the `PTTimeRangeCollection`:

    * `property CMTimeRange range` - Defines the start and duration of the range. 
    * `property long replacementDuration` - If the type of the `TimeRangeCollection` is `PTTimeRangeCollectionTypeReplaceRanges`, the `replacementDuration` is used to create a placement opportunity (ad insertion) with a duration of `replacementDuration`. If the `replacementDuration` is not set, the ad server will determine the duration and number of ads for that placement opportunity.

* `PTAdSignalingMode`:

    * `PTAdSignalingModeCustomTimeRanges` - Added a new type of `PTAdSignalingMode`. This mode is used in conjunction with the `PTTimeRangeCollection` with type `PTTimeRangeCollectionReplace` for ad insertion based on the replacement ranges.

* `PTAdMetadata`:

    * `property PTTimeRangeCollection* timeRangeCollection` - For setting the time ranges used in the mark/delete/replace ranges in the playback content.

* Warning logs:

    * `UNDEFINED_TIME_RANGES`

        * Type - Warning 
        * Description - The ad signaling mode is defined as custom ranges but the custom ranges are not defined.

    * `INVALID_TIME_RANGES`

        * Type - Warning 
        * Description - One or more time ranges are invalid and will be ignored or modified.

**Deprecated APIs**

* `PTAdMetadata`:

    * `property NSArray* externalAdRanges` - This property was previously used to define C3 ranges for marking. It is now deprecated, as these ranges are set via `PTTimeRangeCollection`.
