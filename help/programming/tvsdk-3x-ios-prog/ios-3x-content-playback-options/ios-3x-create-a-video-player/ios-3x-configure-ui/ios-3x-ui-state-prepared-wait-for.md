---
description: Before you can use most of the TVSDK player methods, the player must be in a valid status.
title: Wait for a valid state
exl-id: 2ea7e287-7393-4909-8f55-53cebf4dc289
---
# Wait for a valid state {#wait-for-a-valid-state}

Before you can use most of the TVSDK player methods, the player must be in a valid status.

 The player moves through various statuses. Waiting for the player to be in the correct status ensures that the media resource has successfully loaded. If the player is not in at least the required status, many player methods throw `IllegalStateException`.

The required status is usually `PTMediaPlayerStatusReady`.
