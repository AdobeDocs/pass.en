---
description: If your implementation of Adobe Primetime DRM uses business rules that require the client to maintain state (for example, the playback window interval), Adobe recommends that the server keeps track of the rollback counter and use AIR or SWF allow listing.
title: Rollback detection
---

# Rollback detection {#rollback-detection}

If your implementation of Adobe Primetime DRM uses business rules that require the client to maintain state (for example, the playback window interval), Adobe recommends that the server keeps track of the rollback counter and use AIR or SWF allow listing.

The rollback counter is sent to the server in most requests from the client. If your implementation of Primetime DRM does not require the rollback counter, it can be ignored. Otherwise, Adobe recommends that the server store the random machine ID, which is obtained using [MachineToken.getUniqueId()](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/cert/MachineId.html#getUniqueId()), and the current counter value in a database.

For more information on how to increment and track the rollback counter, see [ClientState](https://help.adobe.com/en_US/primetime/api/drm-apis/server/javadocs-flashaccess-pro/com/adobe/flashaccess/sdk/protocol/ClientState.html) and Rollback detection.