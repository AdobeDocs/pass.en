---
title: Allow list for Adobe® Flash® Player SWFs allowed to play protected content
description: Allow list for Adobe® Flash® Player SWFs allowed to play protected content
copied-description: yes
exl-id: e6adf548-c5d5-45d0-bcd3-ef5185092291
---
# Allow list for Adobe® Flash® Player SWFs allowed to play protected content {#allowlist-for-adobe-flash-player-swfs-allowed-to-play-protected-content}

Specifies the SWF files that can play content. Specify the SWF file by a SWF URL or a SHA-256 digest computed using the contents of the SWF. If you use the SHA-256 digest, this usage rule also specifies the maximum amount of time to allow for the client to download and verify the SWF.

Example use case: Conceptually equivalent to SWF Verification in the case of Flash Media Server, but enforced on the client side to limit which video players can play the content. Note that Adobe Access behavior is different in regards to enforcement of the child SWF compared to the parent SWF.
