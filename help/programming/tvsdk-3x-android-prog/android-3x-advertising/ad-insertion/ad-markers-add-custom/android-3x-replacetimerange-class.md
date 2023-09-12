---
description: The ReplaceTimeRange utility class is an extension of the TimeRange class to be used with CustomRangeMetadata.
title: ReplaceTimeRange class
exl-id: 8d4e9263-bcc0-4300-86ac-6aa7afe5914b
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
