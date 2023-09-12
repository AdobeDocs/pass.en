---
description: TVSDK dispatches timed metadata events and generates timed metadata whenever default or custom tags are encountered or when a playlist changes in a manifest. Events are dispatched in the order in which they appear in the manifest.
title: Timed metadata events
exl-id: 4c58b06e-5f70-452c-a743-55c4b6206711
---
# Timed metadata events{#timed-metadata-events}

TVSDK dispatches timed metadata events and generates timed metadata whenever default or custom tags are encountered or when a playlist changes in a manifest. Events are dispatched in the order in which they appear in the manifest.

Your player implements actions based on the following events:

* `TimedMetadataEvent.TIMED_METADATA_ID3_ADDED`: Dispatched when an ID3 timed metadata was processed. 
* `TimedMetadataEvent.TIMED_METADATA_SKIPPED`: Dispatched when timed metadata was processed and no opportunity was detected.
