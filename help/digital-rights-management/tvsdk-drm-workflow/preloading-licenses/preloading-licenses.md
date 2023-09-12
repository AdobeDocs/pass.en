---
title: Pre-loading licenses for offline playback overview
description: Pre-loading licenses for offline playback overview
copied-description: yes
exl-id: 0d49c0e4-821b-4354-b92d-bbe2c07e467b
---
# Pre-loading licenses for offline playback {#pre-loading-licenses-for-offline-playback}

You can preload the licenses required to play content protected by Primetime DRM. Pre-loaded licenses allow users to view the content whether or not they have an active Internet connection.

The preload process itself *does* require an Internet connection. You can use `DRMManager.loadVoucher()` ahead of time to preload licenses. Later, when the client wishes to play the desired content, the DRM system has been pre-primed and can play the protected content immediately.
