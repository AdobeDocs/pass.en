---
description: Occasionally, there will be times when content cannot be played back. Any number of situations may cause this, including errors in the browser network stack, transport layer, Operating System, Flash Player runtime, or Primetime DRM system.
title: Triaging errors overview
exl-id: fe94d0a4-4f3c-4b0e-b830-a7a83bac1e85
---
# Triaging errors {#triaging-errors}

Occasionally, there will be times when content cannot be played back. Any number of situations may cause this, including errors in the browser network stack, transport layer, Operating System, Flash Player runtime, or Primetime DRM system.

The first diagnostic step is to determine if the problem manifests itself without DRM encryption introduced into the equation. Attempt to package the content, but instruct the packager to not encrypt the content. If the problem still exists, it's likely an issue encoding or packaging the content, or somewhere in the network infrastructure. If the problem goes away when the content is packaged without encryption, the playback failure is likely due to a DRM issue, and you should engage in client/server triaging.

Primetime DRM (outside of Primetime Cloud DRM) has been in the market for several years. As such, there is a wealth of community-sourced information on troubleshooting and configuring Primetime DRM. Adobe has provided a forum for Primetime DRM (formerly called Adobe Access) users to aggregate and share problems and resolutions. To determine if your issue has previously been discussed, please check: [https://forums.adobe.com/community/adobe_access](https://forums.adobe.com/community/adobe_access)

## Client error triaging {#section_D0EBAEB0C27F4B01BD44124DEE62F6BA}

If content does not play, please examine the right-side panel of the Sample Video Players, which will log any `DRMErrorEvent` that occurs. If there is an error event, it will correlate with one of the Flash Player Runtime Errors :

* [DRM Client Error Message Reference](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages); or 
* [AS3 Flash Runtime Errors](https://help.adobe.com/en_US/FlashPlatform/reference/actionscript/3/runtimeErrors.html) (DRM issues start at 3300)
