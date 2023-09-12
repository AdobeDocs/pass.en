---
title: JSON object for custom ad markers
description: JSON object for custom ad markers
copied-description: yes
exl-id: 85bcf306-703c-4a0d-b125-df9316fadf69
---
# JSON object for custom ad markers {#json-object-for-custom-ad-markers}

The code block below defines the "details" JSON object when the type is custom ad markers.

The MetadataNode returned by IFeedItemAdapter:getStreamMetadata() contains 2 entries:
1. an entry with key of type `com.adobe.mediacore.metadata.DefaultMetadataKeys.CUSTOM_AD_MARKERS_METADATA_KEY` and value of of an instance of the MetadataNode returned by `TimeRangeCollection.toMetadata()`.
1. The second entry has a key of type `com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED` with the value of the *adjust-seek-position* attribute below.

```
“metadata”: {
    “ad” :  {
        “type”: “custom ad markers”,
        “details”: {
            "adjust-seek-position": true,
            "time-ranges": [
                {
                    "begin": 5000,
                    "end":15000
                },
                {
                    "begin": 120000,
                    "end":135000
                }
            ]
        }
    }
}

```

|  Property  | Description  |
|---|---|
|  adjust-seek-position  | true or false, used to set the value of the key com.adobe.mediacore.metadata.DefaultMetadataKeys.METADATA_KEY_ADJUST_SEEK_ENABLED in the MetadataNode.  |
|  time-ranges  | An array of JSON Objects indicating the time range for each ad marker. Each JSON Object entry maps to an instance of com.adobe.mediacore.utils.TimeRange.  |
|  time-ranges.begin  | Value in ms indicating the start time of the ad marker.  |
|  time-ranges.end  | Value in ms indicating the end time of the ad marker.  |

Refer to the TVSDK documentation for further information on how custom ad markers work.
