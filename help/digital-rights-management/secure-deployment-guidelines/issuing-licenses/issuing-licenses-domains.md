---
description: To prevent users from backing up and restoring files to bypass domain de-registration, you must implement some domain management approaches.
title: Managing Domains
exl-id: cbf745d2-ba6e-4144-9608-23870bdfe16d
---
# Managing Domains {#managing-domains}

To prevent users from backing up and restoring files to bypass domain de-registration, you must implement some domain management approaches.

Here are some domain management approaches:

* Limit the amount of time the domain credentials are valid.

  Clients need to contact the domain server to reacquire domain credentials when the credentials expire. At that time, the Domain Server can verify that the machine is still authorized to be a member of the domain. 
* Roll over the domain keys each time a user deregisters.

  The License Server should only issue licenses to clients that have the latest domain key. This approach assumes that the License Server can coordinate with the Domain Server to know which key is the latest. Rolling over the domain keys involves generating a new key pair for the domain. When you roll over the keys for a domain, increment the key version in `generateDomainCredential`. 
* If the domain server is the same as the license server, the server can use the rollback counter to detect a backup and restore.

  For more information, see [Processing Adobe Primetime DRM requests](../../protecting-content/implementing-the-license-server/processing-drm-requests.md).
