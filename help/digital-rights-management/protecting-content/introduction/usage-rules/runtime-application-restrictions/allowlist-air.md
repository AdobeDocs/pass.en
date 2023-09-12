---
title: Allow list for Primetime DRM applications allowed to play protected content
description: Allow list for Primetime DRM applications allowed to play protected content
copied-description: yes
exl-id: c5aced0f-2c38-4ae7-9a33-44877e57a993
---
# Allow list for Primetime DRM applications allowed to play protected content {#allowlist-for-primetime-drm-applications-allowed-to-play-protected-content}

A allow list specifies the AIR, iOS, and Android applications that are allowed to play content. It also specifies AIR and iOS application IDs, minimum version, maximum version, and publisher ID.

Example use case: Use this rule to limit playback to a particular application, or to control the version of the application that can access content. 

>[!NOTE]
>
>If you use Adobe Flash Builder to build protected applications, you must make sure that you do not deploy the application in Debug mode. When you deploy an application in Debug mode, the Flash Builder appends `.debug` to the AIR application ID, which then causes the allow list functionality in Primetime DRM to behave unexpectedly.
