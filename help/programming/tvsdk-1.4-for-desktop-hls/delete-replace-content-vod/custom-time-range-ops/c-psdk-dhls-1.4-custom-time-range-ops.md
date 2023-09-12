---
description: TVSDK supports the programmatic deleting and replacing of ad content in VOD streams.
title: Custom time range operations
exl-id: 5480b22a-ecff-4fd8-9ec0-40e4a2e97641
---
# Overview {#custom-time-range-operations-overview}

TVSDK supports the programmatic deleting and replacing of ad content in VOD streams.

The delete and replace feature extends the custom ad markers feature. Custom ad markers mark sections of the main content as ad-related content periods. In addition to marking these time ranges, you can also delete and replace time ranges.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

Ad deletion and replacement are implemented with custom markers that identify different types of time ranges in a VOD stream: mark, delete, and replace. For each custom time range, you can perform associated operations, including deleting or replacing ad content.

For ad deletion and replacement, TVSDK includes the following *custom time range operation* modes:

* MARK - Dispatches `AdBreak` events for the marked regions. (This was called `customAdMarker` in previous versions of TVSDK.) Ad insertion is not allowed in this mode. 

* DELETE - For this mode, the app uses the `TimeRangeCollection` class to define time regions for C3 Ad Deletion. Ad insertion is allowed in this mode. 
* REPLACE - In this mode, the app replaces a `timeRange` with an Adobe Primetime ad decisioning `AdBreak`. The replace operation starts where the C3 Ad deletion occurs, and ends at the indicated time (shorter or longer than the original time range).

TVSDK provides a `CustomRangesOpportunityGenerator` class to generate placement opportunities for the MARK and DELETE ranges. For the REPLACE mode, TVSDK generates two placement opportunities for each time range:

* The `CustomRangeResolver` generates placement opportunities for DELETE 
* The `AuditudeAdResolver` generates placement opportunities for INSERT.
