---
title: Allow list for Adobe® Flash® Player SWFs
description: Allow list for Adobe® Flash® Player SWFs
copied-description: yes
exl-id: 1bae06b6-dbac-4839-b1d3-b7f6379b521a
---
# Allow list for Adobe® Flash® Player SWFs{#allowlist-for-adobe-flash-player-swfs}

This allow list specifies the SWF files that are allowed to play content.

Specify the SWF file with a SWF URL or a SHA-256 digest computed using the contents of the SWF. If you use the SHA-256 digest, this usage rule also specifies the maximum amount of time to allow for the client to download and verify the SWF.

Example use case: Conceptually equivalent to SWF Verification in the case of Flash Media Server, but enforced on the client side to limit which video players can play the content. Note that Primetime DRM behavior differs regarding the enforcement of the child SWF compared to the parent SWF.
