---
title: Implementation models

description: Implementation models

---

# Implementation models {#imp-models}

## Server-side policies {#ss-policies}

This model will make use of CM as a Policy Decision Point, thus delegating the access decision to the service.

Since the client should make no assumption regarding the applied policies, the implementation needs to check the decision on session initialization as well as on a regular basis, during playback from the heartbeat response.
