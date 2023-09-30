---
title: Implementation models
description: Implementation models
exl-id: 3bcb63ba-9b4a-4df4-8d24-e520b8830a10
---
# Implementation models {#imp-models}

## Server-side policies {#ss-policies}

This model will make use of CM as a Policy Decision Point, thus delegating the access decision to the service.

Since the client should make no assumption regarding the applied policies, the implementation needs to check the decision on session initialization as well as on a regular basis, during playback from the heartbeat response.
