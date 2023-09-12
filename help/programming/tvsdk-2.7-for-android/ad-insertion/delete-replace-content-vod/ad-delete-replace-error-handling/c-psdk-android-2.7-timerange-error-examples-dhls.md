---
description: TVSDK responds to erroneous time range specifications by merging or replacing the time ranges as appropriate.
title: Time range error examples
exl-id: 70bbd98b-4084-4a26-8420-fdbe9029194d
---
# Time range error examples{#time-range-error-examples}

TVSDK responds to erroneous time range specifications by merging or replacing the time ranges as appropriate.

**DELETE time range**

In the following example, four intersecting DELETE time ranges are defined. TVSDK merges the four time ranges into one, so that the actual delete range is from 0-50s. 

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000
        },
        {
            "begin": 20000,
            "end": 50000
        },
        {
            "begin": 0,
            "end": 30000
        },
        {
            "begin": 30000,
            "end": 40000
        }
    ]
}

```

**REPLACE time range**

In the following example, four REPLACE time ranges are defined with conflicting time ranges. In this case, TVSDK replaces 0-50s with 25s of ads. It goes with the first replacement duration in the sort order, because there are conflicts in subsequent ranges. 

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000,
            "replace-duration": 15000
        },
        {
            "begin": 20000,
            "end": 50000,
            "replace-duration": 20000
        },
        {
            "begin": 0,
            "end": 30000,
            "replace-duration": 25000
        },
        {
            "begin": 30000,
            "end": 40000,
            "replace-duration": 30000
        }
    ]
}

```
