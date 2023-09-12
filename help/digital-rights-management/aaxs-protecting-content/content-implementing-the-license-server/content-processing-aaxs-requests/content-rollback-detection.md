---
title: Rollback detection
description: Rollback detection
copied-description: yes
exl-id: 525ae64e-1ade-4661-8403-ee4e42181358
---
# Rollback detection{#rollback-detection}

For rollback detection, some usage rules require the client to maintain state information for enforcement of the rights. For example, to enforce the playback window usage rule, the client stores the date and time when the user first began viewing the content. This event triggers the start of the playback window. To securely enforce the playback window, the server needs to ensure that the user is not backing up and restoring the client state in order to remove the playback window start time stored on the client. The server does this by tracking the value of the client's rollback counter. For each request, the server gets the value of the counter by calling `RequestMessageBase.getClientState()` to obtain the `ClientState` object, then calling `ClientState.getCounter()` to obtain the current value of the client state counter. The server should store this value for each client (use `MachineId.getUniqueId()` to identify the client associated with the rollback counter value), and then call `ClientState.incrementCounter()` to increase the counter value by one. If the server detects that the counter value is less than the last value seen by the server, the client state may have been rolled back. For more information on client state tamper detection, see the `ClientState` API reference documentation.
