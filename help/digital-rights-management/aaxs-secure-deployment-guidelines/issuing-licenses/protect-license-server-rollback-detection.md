---
title: Rollback detection
description: Rollback detection
copied-description: yes
exl-id: 054d3634-5ce9-4a51-ac91-e6ae60a1fd6e
---
# Rollback detection {#rollback-detection}

If your implementation of Adobe Access uses business rules that require the client to maintain state (for example, the playback window interval), Adobe highly recommends that the server keep track of the rollback counter and use AIR or SWF allow listing.

The rollback counter is sent to the server in most requests from the client. If your implementation of Adobe Access does not require the rollback counter, it can be ignored. Otherwise, Adobe recommends that the server store the random machine ID—obtained using `MachineToken.getMachineId().getUniqueId()`—and the current counter value in a database. For more information on incrementing and tracking the rollback counter, see ClientState in *Adobe Access API Reference* and *Rollback detection* in *Using the Adobe Access SDK for Protecting Content*.
