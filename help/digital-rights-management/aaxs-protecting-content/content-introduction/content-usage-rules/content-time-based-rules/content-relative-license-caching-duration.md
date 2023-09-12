---
title: License caching duration
description: License caching duration
copied-description: yes
---

# License caching duration{#license-caching-duration}

Specifies the duration a license can be cached on disk in the client's local License Store without requiring reacquisition from the license server. You can alternatively specify an absolute date/time after which a license can no longer be cached.

Once the cache expiration date has passed, the license is no longer valid, and the client must request a new license from the license server.

Example use case: Use the license caching duration to specify a fixed amount of time valid for a particular license, such as in a rental use case. A 30-day rental can be specified (with license caching) to indicate the total license duration within which to consume the content. 
