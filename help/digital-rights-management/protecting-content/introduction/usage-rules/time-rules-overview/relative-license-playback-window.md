---
title: Playback window
description: Playback window
copied-description: yes
---

# Playback window{#playback-window}

The playback window specifies the duration a license is valid after the first time it is used to play protected content.

Example use case: Some business models allow a rental period of 30 days but, once playback begins, playback must be completed in 48 hours. In this case, the 48-hour duration of the license is the playback window.

**From version 5.3 forward** - The playback window also supports the option of enabling or disabling Hard Stop, which indicates whether the decryption context for playback should stop at the expiration of the playback window (enabled) or continue despite expiration (disabled).

>[!NOTE]
>
>The hard stop option does not work properly with Playback Window if used in conjunction with it (Playback Window will not be honored). Playing content with Playback window without secure stop does respect the playback window restriction.

