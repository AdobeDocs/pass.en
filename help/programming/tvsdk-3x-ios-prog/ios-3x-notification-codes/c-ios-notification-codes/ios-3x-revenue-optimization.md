---
description: This table provides detailed information about Revenue Optimization notifications. 
title: REVENUE Optimization code
exl-id: 3657ba70-ec35-495b-ae7b-4198429bdf6a
---
# REVENUE Optimization code {#revenue-optimization-code}

This table provides detailed information about REVENUE OPTIMIZATION notifications.

## Enable Revenue Optimization Reporting {#enable-revenue-optimization-reporting}

To enable this reporting, use PTMediaPlayer api: `[mediaPlayersetRevenueOptimizationReportingLevel:PTNotificationTypeInfo]`.

>[!NOTE]
>
>Most informational notifications contain relevant metadata, for example, the URL of the resource that failed to download. Some notifications contain metadata to specify whether the problem occurred in the main video content, in the alternate audio content, or in an ad.

|Code |Name |Inner Notification |Metadata Keys |Comments |
|---|---|---|---|---|
|401001 | REVENUE_OPTIMIZATION_REPORTING | None | Refer below table for metadata keys based on different events. | None |

| Event Details |ContextMetadata |
|---|---|
| **CONTENT_RESOURCE_START** Dispatched in TVSDK when MediaPlayer::replaceCurrentResource is called. |clientTimestamp, fallbackOnInvalidCreative, showStaticBanners, hasPreroll, event, adSignalingMode, resourceUrl, creativeRepackagingFormat, delayAdLoadingTolerance, zoneID, hasLivePreroll, adRequestTimeout, delayAdLoading, resourceType, creativeRepackagingEnabled, mediaId, clientId |
| **CONTENT_PLAYBACK_START** Dispatched in TVSDK when content has entered the prepared state and is ready for playback. This event will not dispatch on every manifest upload - will only dispatch on the initial load.|clientTimestamp, contentURL, contentType, event, isLive, clientID|
| **AD_OPPORTUNITY_GENERATED** Dispatched in TVSDK when an opportunity is generated.|clientTimestamp, event, opportunityId, placementDuration, clientId|
| **AD_OPPORTUNITY_RESOLVE_START** Dispatched in TVSDK when an opportunity begins resolving. | clientTimestamp, event, opportunityId, placementDuration, clientId |
| **AD_OPPORTUNITY_RESOLVE_FAILED** Dispatched in TVSDK when an ad resolver calls MediaPlayerClient::notifyFailed(). Need to fill in data | opportunityId, notificationAD |
| **AD_RESOURCE_LOAD** Dispatched when any ad resource is fetched by URL. responseStartTime:Unix timestamp for when the request first started. responseTotalTime:Total amount of time (in seconds) that it took for a response to load. responseStatus:The status code encountered while fetching the resource. status:"error" or "success" referrerAdId:The referring ad id that requested fetching of this resource (if present). referrerUrl:The referring url that requested fetching of this resource. errorMessage:If the status is "error", the reason for the error will be located here. | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, referrerURL, referrerAdId |
| **AD_RESOURCE_LOAD_CRS** Dispatched in TVSDK when a CRS is applied to an asset, as well as the response for the m3u8. resourceType:always "crs". responseStartTime:Unix timestamp for when the request first started. responseTotalTime:Total amount of time (in seconds) that it took for a response to load. responseStatus:The status code encountered while fetching the resource. status:"error" or "success". errorMessage:If the status is "error", the reason for the error will be located here. mediaFileUrl:The original media file url that was selected. mediaFileBitrate:The bitrate of the media file that was selected. mediaFileMimeType: The mime type of the media file that was selected. url:The final asset url. | opportunityId, resourceType, responseTotalTime, responseStatus, responseStartTime, status, errorMessage, url, mediaFileURL, mediaFileBitrate, mediaFileMimeType, url |
| **AD_TIMELINE_PLACE** Dispatched in TVSDK after an adBreak was placed on the timeline. This event will occur once for each ad break. proposedTime:The time in which the ad break was requested to be placed. actualTime:The time in which the ad break was actually placed. proposedDuration:The duration of the ad break that was requested for insertion. For live content this would be the cue duration. For VOD content this would normally be -1. actualDuration:The actual duration of the ad break inserted. Calculated as the sum duration of all ads, defined by their respective segment durations, added or replaced in the original stream timeline. proposedAds:The number of ads in the proposed ad break. totalAds:The number of ads that were successfully placed. ads...n:The successfully insert ads will be inserted here. Entire ad manifest information can be retrieved from AD_OPPORTUNITY_RESOLVE_PROCESS | opportunityId, status, errorMessage, proposedTime, proposedDuration, actualTime, actualDuration, proposedAds, totalAds, ads_id, ads_type, ads_duration, ads_url |
|**AD_PLAYBACK_START** Dispatched in TVSDK after an ad begins playback. | clientTimestamp, event, id, url, duration, type, opportunityId, clientId |
| **AD_PLAYBACK_COMPLETE** Dispatched in TVSDK after an ad completes playback. | clientTimestamp, event, id, url, duration, type, opportunityId, clientId |
| **ADBREAK_PLAYBACK_START** Dispatched in TVSDK when an adbreak starts playback. | clientTimestamp, event, opportunityId, duration, time, clientId |
| **ADBREAK_PLAYBACK_COMPLETE** Dispatched in TVSDK when an adbreak completes playback. | clientTimestamp, event, opportunityId, clientId |
| **CONTENT_PLAYBACK_COMPLETE** Dispatched in TVSDK when any content is completed.This could occur if the stream is replaced, the player enters an error state, the player is reset, or the content actually completes. This event will be necessary to track a sessionId. | clientTimestamp, event, clientId, url, status, errorMessage |
| **AD_PLAYBACK_ERROR** Dispatched in TVSDK when an ad has an error playing back (variant stream errors). | event, error, Timestamp, manifestUrl, time, opportunityId, url |
