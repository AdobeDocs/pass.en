---
description: The TimeRangeCollection utility class abstracts the notion of an ordered collection of TimeRange specifications and provides services to translate itself into a Metadata instance.
title: TimeRangeCollection class
exl-id: 2e5160b0-2254-4a40-8c32-fe3e05b9fc30
---
# TimeRangeCollection class{#timerangecollection-class}

The TimeRangeCollection utility class abstracts the notion of an ordered collection of TimeRange specifications and provides services to translate itself into a Metadata instance.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

The defined value for the type of collection are `MARK_RANGES`, `DELETE_RANGES`, and `REPLACE_RANGES`. You can create `TimeRangeCollection`s using these three types.
