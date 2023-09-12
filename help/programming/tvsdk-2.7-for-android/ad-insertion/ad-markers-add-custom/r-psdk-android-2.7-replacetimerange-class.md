---
description: The ReplaceTimeRange utility class is an extension of the TimeRange class to be used with CustomRangeMetadata.
title: ReplaceTimeRange class
exl-id: 61885c52-d40a-4c72-97a0-51e56da9d449
---
# ReplaceTimeRange class {#replacetimerange-class}

The ReplaceTimeRange utility class is an extension of the TimeRange class to be used with CustomRangeMetadata.

```java
public class ReplaceTimeRange extends TimeRange {
    // Default constructor method
    public ReplaceTimeRange() { 
        ... 
    }

    // Details of begining, duration and replaceDuration 
    // provided at construction time 
    public ReplaceTimeRange(long begin, long duration, long replaceDuration) { 
        ... 
    }

    // Replace duration
    public long getReplaceDuration() { 
        ... 
    }
}

```
