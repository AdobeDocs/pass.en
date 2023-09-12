---
description: With TVSDK you can control the basic playback experience for live and video on demand (VOD). TVSDK provides methods and properties on the player instance that you can use to configure the player user interface.
title: Wait for a valid state
exl-id: ab9da066-429f-44ca-b2e7-2bde9e5c0f90
---
# Wait for a valid state {#wait-for-a-valid-state}

With TVSDK you can control the basic playback experience for live and video on demand (VOD). TVSDK provides methods and properties on the player instance that you can use to configure the player user interface.

Before you can use most of the TVSDK player methods, the player must be in a valid state. 
The player moves through various states. Waiting for the player to be in the correct state ensures that the media resource has successfully loaded. If the player is not in at least the required state, many player methods throw `IllegalStateException`.

The required state is usually PREPARED.
