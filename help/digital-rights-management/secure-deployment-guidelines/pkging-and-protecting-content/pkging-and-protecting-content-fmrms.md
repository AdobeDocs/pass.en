---
description: Flash Media Rights Management Server 1.x and Adobe Primetime DRM use different metadata to package content and request licenses. For Primetime DRM to use FMRMS version 1.x content, the metadata must be converted.
title: Ensuring compatibility with Flash Media Rights Management Server 1.x
exl-id: 737c853f-4e27-47e6-9248-857c7800795a
---
# Ensuring compatibility with Flash Media Rights Management Server 1.x {#ensuring-compatibility-with-flash-media-rights-management-server-x}

Flash Media Rights Management Server 1.x and Adobe Primetime DRM use different metadata to package content and request licenses. For Primetime DRM to use FMRMS version 1.x content, the metadata must be converted.

The Primetime DRM SDK supports the following options for conversion of metadata:

* Offline (recommended)

  Generate the Primetime DRM metadata in an offline process and store the metadata until it is requested by a client. If metadata is generated offline, the license server does not need access to the 1.x CEKs or the packager credential. Converting offline offers better performance because the License Server does not need to generate the metadata in real time. 
* On-demand

  The Primetime DRM metadata is generated when the metadata is requested by a client. When a Primetime DRM client downloads version 1.x content, the client sends the DRM metadata to the Primetime DRM SDK. The SDK converts the DRM metadata to the current format, encrypts and embeds the content encryption key (CEK) in the metadata, and sends the content back to the Primetime DRM client.

  >[!NOTE]
  >
  >The Primetime DRM 1.x metadata does not include the CEK.

  To convert the metadata, Primetime DRM requires access to the Primetime DRM 1.x content encryption keys. When you migrate from Flash Media Rights Management Server 1.x, you can continue to store the content encryption keys in the LiveCycle ES database or implement a custom solution to securely store the content encryption keys in another location. If you decide to store the content encryption keys in the LiveCycle ES database, follow the recommendations that are outlined in *Protecting access to sensitive content in the database* in **Hardening and Security for LiveCycle® ES2**.

For more information on ensuring compatibility with content packaged by using Flash Media Rights Management Server 1.x, see the Adobe Primetime DRM APIs on [Adobe Primetime API References](https://help.adobe.com/en_US/primetime/api/index.html#api-Adobe_Primetime_API_References).
