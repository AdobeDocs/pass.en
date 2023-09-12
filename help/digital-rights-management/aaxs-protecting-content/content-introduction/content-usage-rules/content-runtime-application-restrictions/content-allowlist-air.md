---
title: Allow list for Adobe® Primetime applications allowed to play protected content
description: Allow list for Adobe® Primetime applications allowed to play protected content
copied-description: yes
exl-id: 56004a0f-118c-42f3-869b-2cc1c91ee544
---
# Allow list for Adobe® Primetime applications allowed to play protected content {#allowlist-for-adobe-primetime-applications-allowed-to-play-protected-content}

Specifies the AIR/iOS applications that can play content. Specify the AIR/iOS application ID, minimum version, maximum version, and publisher ID.

Example use case: Use this rule to limit playback to a particular AIR/iOS application, or to control which version can access the content. 

>[!NOTE]
>
>If you are using Adobe Flash Builder to build protected applications, make sure that you do not deploy the application in ‘Debug' mode. When deploying an application in ‘Debug' mode, the Flash Builder will append “.debug” to the AIR application ID. This will cause the allow list functionality in Adobe Access to behave unexpectedly.
