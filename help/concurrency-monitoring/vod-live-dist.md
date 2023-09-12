---
title: How to distinguish between VOD and Live Content in Concurrency Monitoring
description: How to distinguish between VOD and Live Content in Concurrency Monitoring
---

# How to: Distinguish between VOD and Live Content in Concurrency Monitoring {#dist-vod-live}

**Q:** Can the Concurrency Monitoring service distinguish between the type of content that is being played (Live content vs. Video on demand)?

 

**A:** Concurrency Monitoring cannot directly distinguish between live content and Video on demand (VOD). The video player must know the type of content it is playing and send this information during the [session initialization call](/help/concurrency-monitoring/cm-api-overview.md#session-initial) (required for Concurrency Monitoring). The regular workflow looks like this:

1. The Concurrency Monitoring customers define a set of metadata that they would like to have rules implemented on (e.g. content-type=live|vod, device-type=mobile|console|desktop). 
1. The Concurrency Monitoring team implements the desired policy. Example:
    1. if content-type=live, max streams=3, latest wins
    1. if content-type=vod, max streams=1, latest wins

1. When the end-user plays the content, the video player must send values for those metadata fields that were established as being part of a policy. 

1. The Concurrency Monitoring service, based on the defined policy and received values, will issue a decision (play/stop). 

1. The decision must be obeyed by the video player in order for the system to work.

 

## Related Information {#related-info-vod-live-dist}

* [Concurrency Monitoring Standard Metadata Attributes](/help/concurrency-monitoring/standard-metadata-attributes.md)
* [Concurrency Monitoring API Overview](/help/concurrency-monitoring/cm-api-overview.md)
