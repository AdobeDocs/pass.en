---
description: You can turn on this feature and check for related events.
title: Use live master-manifest update
exl-id: 02cb3116-cc30-4139-841b-8d6297214b8b
---
# Use live master-manifest update{#use-live-master-manifest-update}

You can turn on this feature and check for related events.

1. To turn on live master-manifest updates, set the update frequency (in minutes) by setting the `NetworkConfiguration.masterUpdateInterval` property.
1. Optionally, track successful manifest updates by listening for the `MediaPlayerItemEvent.MASTER_UPDATED` event.
