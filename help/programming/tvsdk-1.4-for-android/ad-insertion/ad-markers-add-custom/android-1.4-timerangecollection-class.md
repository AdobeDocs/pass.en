---
description: The TimeRangeCollection utility class abstracts the notion of an ordered collection of TimeRange specifications and provides services to translate itself into a Metadata instance.
title: TimeRangeCollection class
exl-id: 1af41267-c222-43ac-84ca-0bf37b6a59de
---
# TimeRangeCollection class{#timerangecollection-class}

The TimeRangeCollection utility class abstracts the notion of an ordered collection of TimeRange specifications and provides services to translate itself into a Metadata instance.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```java
public final class TimeRangeCollection {
    // default constructor method
    public TimeRangeCollection(Type type) {...}

    // the list of timerange specifications provided at construction time 
    public TimeRangeCollection(Type type, List<TimeRange> timeRanges) {...}

    // timerange specs can also be added later
    public void addTimeRange(TimeRange timeRange) {...}

    // translate the set of timerange specs into a Metadata instance 
    public Metadata toMetadata(Metadata options) {...}
}

```

The `type` parameter, which is the first positional parameter in the signature of the constructor methods, is an instance of the `TimeRangeCollection#Type` enumeration. This is part of the `TimeRangeCollection` class. The values that are currently defined by this enumeration are `MARK_RANGES`, `DELETE_RANGES`, and `REPLACE_RANGES`. You can create `TimeRangeCollection` objects using these three types.
