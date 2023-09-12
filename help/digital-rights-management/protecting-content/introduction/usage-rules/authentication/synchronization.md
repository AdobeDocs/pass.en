---
title: Requirements for synchronization
description: Requirements for synchronization
copied-description: yes
exl-id: 0368e363-893f-4b51-a317-00791d0ab54f
---
# Requirements for Synchronization {#requirements-for-synchronization}

Requirements for synchronization specifies the frequency with which the client synchronize its state with the server. If the client has been issued an out-of-band license (without a license server being contacted), usage rules may specify that the client must send synchronization messages to the server in order to synchronize the client's secure time, and report client state to the server.

The synchronization behavior is defined using the following parameters:

* **Start Interval** - Specifies how long to wait after the last successful synchronization to start another synchronization request. 
* **Hard Stop Interval** - (Optional). Disallow playback if a successful synchronization has not occurred in the specified amount of time. 
* **Force Sync Probability** - (Optional). Probability with which the client should send a synchronize message before the next start interval.

>[!NOTE]
>
>This usage rule is supported by Primetime DRM clients version 3.0 or later. The behavior on older clients depends on the minimum client version supported by the license server.
