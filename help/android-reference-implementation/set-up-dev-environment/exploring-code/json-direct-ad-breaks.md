---
title: JSON object for direct ad breaks
description: Details the JSON object when the type value is direct ad breaks
exl-id: d5e3ddd5-b963-4e7d-b04b-087d4fe96faf
---
# JSON object for direct ad breaks{#json-object-for-direct-ad-breaks}

The following code block defines the details JSON object when the type value is direct ad breaks.

The `MetadataNode` returned by `IFeedItemAdapter:getStreamMetadata()` contains an entry with key of type `com.adobe.mediacore.metadata.DefaultMetadataKeys.JSON_METADATA_KEY` and value of a string representation of the details JSON object value below.

```
“metadata”: { 
    “ad” :  { 
        “type”: “direct ad breaks”, 
        “details”: { 
            "ad-breaks": [ 
                { 
                    "tag": "break-001", 
                    "time": 0, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        }, 
                        { 
                        } 
                    ] 
                }, 
                { 
                    "tag": "break-002", 
                    "time": 300000, 
                    "replace": 0, 
                    "ad-list": [ 
                        { 
                        } 
                    ] 
                } 
            ] 
        } 
    } 
} 

```

|  Property  | Description  |
|---|---|
|  `tag`  | A string that maps to the tag field in `com.adobe.mediacore.timeline.advertising.AdBreak`.  |
|  `time`  | Indicates the start time for the ad break, maps to the time field in `com.adobe.mediacore.timeline.advertising.AdBreak`. A value of 0 indicates a pre-roll ad.  |
|  `replace`  | Indicates the ad break replace duration, maps to the `replaceDuration` field in `com.adobe.mediacore.timeline.advertising.AdBreak`.  |
|  `ad-list`  | A list of ads to be played during the given ad break, maps to the `List<Ad>` field in `com.adobe.mediacore.timeline.advertising.AdBreak`.  |

The following code block defines the JSON object for the ads-list array.

```
"ad-list": [ 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 15000, 
        "tag": "1st break - 1st ad" 
    }, 
    { 
        "url": "https://cdn.auditude.com/player/downloads/data/espn/ads/csx/prog_index.m3u8", 
        "duration": 30000, 
        "tag": "1st break - 2nd ad" 
    } 
], 

```

|  Property  | Description  |
|---|---|
|  `url`  | The URL to the ad content, maps to the url field in `com.adobe.mediacore.timeline.advertising.Ad`.  |
|  `duration`  | The duration of the ad, maps to the duration field in `com.adobe.mediacore.timeline.advertising.Ad`.  |
|  `tag`  | A description string.  |
