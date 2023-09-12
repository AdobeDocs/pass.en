---
description: The Adobe Primetime DRM Server for Protected Streaming is a license server implementation that is based on the Primetime DRM SDK. This server issues licenses for protected content to Primetime DRM clients.
title: About Adobe Primetime DRM Server for Protected Streaming
exl-id: 911acd61-8b27-4ac7-a420-2faeb46e8087
---
# About Adobe Primetime DRM Server for Protected Streaming{#about-adobe-primetime-drm-server-for-protected-streaming}

The Adobe Primetime DRM Server for Protected Streaming is a license server implementation that is based on the Primetime DRM SDK. This server issues licenses for protected content to Primetime DRM clients.

The Primetime DRM Server for Protected Streaming supports multiple tenants. You can host a single server on behalf of multiple content publishers, each with its own configuration settings. In addition, the server supports custom authorization components, so you can execute custom logic before a license is issued.

This server is intended for use with HTTP Streaming. As a result, this server implementation does not support all capabilities that are available in Primetime DRM. For example, it does not support user authentication requests, multiple policies, domain-bound licenses, license chaining, or synchronization messages.

>[!NOTE]
>
>Adobe Primetime DRM was formerly called Adobe Access, and prior to that, Flash Access.
