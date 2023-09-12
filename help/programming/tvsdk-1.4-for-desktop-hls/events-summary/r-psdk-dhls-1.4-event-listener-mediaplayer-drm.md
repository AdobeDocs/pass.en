---
description: TVSDK dispatches digital rights management (DRM) events in response to DRM-related operations such as when new DRM metadata becomes available.
title: DRM events
exl-id: 65a02744-8973-418d-9a9c-53a2a313f631
---
# DRM events{#drm-events}

TVSDK dispatches digital rights management (DRM) events in response to DRM-related operations such as when new DRM metadata becomes available.

 To be notified about all DRM-related events, listen for `DRMMetadataInfoEvent` for DRM events with the `MediaPlayer` object. 

|  Event  | Meaning  |
|---|---|
|DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE)  | New DRM metadata is available.  |
