---
description: Before you can use most of the TVSDK player methods, the player must be in a valid status.
title: Wait for a valid state
exl-id: 150b37b8-c36d-4143-bead-ddc601bba6fe
---
# Wait for a valid state{#wait-for-a-valid-state}

Before you can use most of the TVSDK player methods, the player must be in a valid status.

 The player moves through various statuses. Waiting for the player to be in the correct status ensures that the media resource has successfully loaded. If the player is not in at least the required status, many player methods throw `IllegalStateException`.

The required status is usually `PTMediaPlayerStatusReady`.
