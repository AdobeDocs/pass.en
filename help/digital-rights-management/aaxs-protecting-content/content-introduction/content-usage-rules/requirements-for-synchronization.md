---
title: Requirements for Synchronization
description: Requirements for Synchronization
copied-description: yes
---

# Requirements for Synchronization{#requirements-for-synchronization}

Specifies the frequency in which the client will synchronize its state with the server. If the client has been issued an out-of-band license (without a license server being contacted), usage rules may specify that the client must send synchronization messages to the server in order to synchronize the client's secure time and report client state to the server.

The synchronization behavior is defined using the following parameters:

* Start Interval — Specifies how long to wait after the last successful synchronization to start another synchronization request. 
* Hard Stop Interval — (Optional). Disallow playback if a successful synchronization has not occurred in the specified amount of time. 
* Force Sync Probability — (Optional). Probability with which the client should send a synchronize message before the next start interval.

>[!NOTE]
>
>This usage rule is supported by Adobe Access clients version 3.0 and higher. The behavior on older clients depends on the minimum client version supported by the license server. See, [Minimum Client Version](../../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-minimum-client-version.md).

