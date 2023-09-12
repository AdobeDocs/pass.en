---
title: Upgrading the Adobe Primetime DRM Server for Protected Streaming
description: Upgrading the Adobe Primetime DRM Server for Protected Streaming
copied-description: yes
exl-id: 6edfba1b-46a2-4cbd-bc14-feeef1a36ed6
---
# Upgrading the Adobe Primetime DRM Server for Protected Streaming{#upgrading-the-adobe-primetime-drm-server-for-protected-streaming}

If you want to upgrade a server that runs the Primetime DRM Server for Protected Streaming, you need to replace the `flashaccessserver.war` file that has been deployed on your application server with the file that has been included with the latest Primetime DRM.

If you want to use the new configuration options, you need to update your server's `flashaccess-tenant.xml`. You also need to update [!DNL jsafe.dll] or [!DNL libjsafe.so] with the version that has been included with the latest Primetime DRM.
