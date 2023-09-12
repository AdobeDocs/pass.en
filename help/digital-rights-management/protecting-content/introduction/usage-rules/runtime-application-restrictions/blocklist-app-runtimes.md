---
title: Block list of application runtimes
description: Block list of application runtimes
copied-description: yes
exl-id: f8d1d385-41d4-4361-82c1-417b2ff421c5
---
# Block list of application runtimes {#blocklist-of-application-runtimes}

Block list of application runtimes specifies the version of the Primetime client or Flash Runtime that cannot access content. Specify the restricted runtime (Flash Player, AIR, or iOS), platform, and version.

Example use case: Similar to the Primetime DRM Client block list, the latest version of the Flash Player, AIR, or iOS runtimes can be specified as the minimum version required for license acquisition and content playback.

You can identify the application runtime by any of the attributes supported for Primetime DRM client versions, in addition to the following attributes:  

| **Attribute** |**Supported Values** |**Match Criteria** |**Description** |
|---|---|---|---|
|  Application  | `“FlashPlayer”, “AIR”, "DRM_Library", "AVE"`  | Exact Match  | Identifies the name of the application runtime.  |
