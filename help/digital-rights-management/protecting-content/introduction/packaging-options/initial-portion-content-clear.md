---
title: Initial portion of content in the clear
description: Initial portion of content in the clear
copied-description: yes
exl-id: f291e0f5-ce26-41c4-b468-36b111cb7a1c
---
# Initial portion of content in the clear{#initial-portion-of-content-in-the-clear}

This optional parameter specifies an amount of time (in seconds) from the beginning of the content that will remain unencrypted.

Example use case: This allows for a faster playback startup time while the Primetime DRM client downloads the license in the background. The unencrypted portion of the video begins playback immediately while the initialization and license acquisition occur in the background. When this feature is turned off, users may notice a delay in the playback experience, because the client machine performs all of the licensing steps before any video playback can occur.
