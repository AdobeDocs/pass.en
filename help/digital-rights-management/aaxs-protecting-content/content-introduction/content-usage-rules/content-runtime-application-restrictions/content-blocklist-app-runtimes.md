---
title: Block list of application runtimes restricted from accessing protected content
description: Block list of application runtimes restricted from accessing protected content
copied-description: yes
exl-id: 7c9d9e31-1a8d-4c76-9f2c-fcda58de1a42
---
# Block list of application runtimes restricted from accessing protected content {#blocklist-of-application-runtimes-restricted-from-accessing-protected-content}

Specifies the version of the Primetime or Flash Runtime that cannot access content. Specify the restricted runtime (Flash Player, AIR, or iOS), platform, and version.

Example use case: Similar to the DRM Client block list, the latest version of the Flash Player, AIR, or iOS runtimes can be specified as the minimum version required for license acquisition and content playback.

The application runtime may be identified by any of the attributes supported for DRM client versions, in addition to the following attributes:  

| **Attribute** |**Supported Values** |**Match Criteria** |**Description** |
|---|---|---|---|
|  Application  | “FlashPlayer”, “AIR”, "DRM_Library", "AVE"  | Exact Match  | Identifies the name of the application runtime. |
