---
title: Remote and local iOS key delivery
description: Remote and local iOS key delivery
copied-description: yes
exl-id: becc2d3f-39f3-40ee-b980-7dfbbe6f569d
---
# Remote and local iOS key delivery {#remote-and-local-ios-key-delivery}

Adobe Primetime supports the following options for key delivery to iOS clients:

* **Remote** - Performs as specified in the HTTP Live Streaming (HLS) specification; the M3U8 manifest specifies an HTTPS path that includes an AES key that should be used to decrypt the following encrypted segments in the stream. When you specify `Remote` in the Primetime DRM policy, the client device must connect to a remote HTTPS server to obtain an AES key. 

* **Local** - When you specify `Local` in the Primetime DRM instead of connecting to the internet/network for the AES key, a local HTTPS server is embedded into the iOS application, which then manages all AES key requests. The embedded HTTPS server is automatically set up and configured in the P application. No intervention is required by the application developer.

The remote key delivery is enabled through the Primetime DRM policy that is used to package content. If you want to change this setting, you must repackage the content. If you enable remote key delivery, you must deploy a Primetime DRM Key Server that can manage key requests from iOS clients. However, there is no change to the workflow for clients on other platforms.

>[!NOTE]
>
>The Key delivery selection only impacts iOS clients. All other devices that use HLS content , such as Android and Primetime on Desktop (Flash Player), always use `Local` key delivery, even if `Remote` has been specified.
