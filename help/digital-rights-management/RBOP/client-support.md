---
description: This section describes the features available with different versions of Flash Player and TVSDK.
title: RBOP Client Support
exl-id: 1120587e-45cf-45cc-8b41-1886ab2ed2a4
---
# RBOP Client Support {#rbop-client-support}

This section describes the features available with different versions of Flash Player and TVSDK.

**Error Dispatch** - The TVSDK platforms listed below dispatch a DRM Runtime Error when the resolution of the content that is being played exceeds the resolution that is allowed for the device configuration that is defined in the DRM policy:

* Flash Player Versions 18 through 20
* Android - Versions
* iOS - Versions

>[!NOTE]
>
>* All Flash and mobile platforms support Error Dispatch, however only the TVSDK clients listed above process RBOP-related errors.
>* RBOP-related [DRM Client Errors](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages):
>    * **3371** - Malformed resolution based on output protection constraints in the license. 
>    * **3372** - The content's resolution is larger than the maximum resolution that is specified in the output-protection constraint. (This can occur if somebody tried to inject content meant for another device.) 
>    * **3373** - The content's resolution is larger than the resolution that is specified by the currently active output-protection constraint. (This means we will have to downgrade.)
>

**Automatic Downscaling** - The technique used to downscale varies by platform and Flash Player version:

* Flash Player Version 21: Supports RBOP with Automatic Downscaling (intelligent bitrate switching)
* Firefox Version 38 and later on Windows (with Access CDM): Adobe automatically downgrades a higher bitrate stream to a lower one (as opposed to downloading a lower-grade stream).

>[!NOTE]
>
>These platforms automatically down-scale video and display the content at a resolution that is lower than or equal to what is specified by the DRM policy. With this feature, content will always be played back to the client, as long as there is an available stream that meets the DRM policy restrictions.

**Legacy Output Protection** - Clients using Flash Players prior to Version 18 can only handle legacy OP restrictions. Clients with Flash Player Version 18 and later can handle either legacy or RBOP restrictions. If you are setting RBOP restrictions, you should also set legacy OP restrictions for older clients. For clients that support RBOP, RBOP restrictions trump legacy OP restrictions.
