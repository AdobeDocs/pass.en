---
title: License acquisition process overview
description: License acquisition process overview
copied-description: yes
exl-id: 0e1c43a5-9a7d-4534-acd6-7feff94f4670
---
# License acquisition process overview{#license-acquisition-process-overview}

Enabling your application to play content under the protection of Primetime DRM is described in the following sections, using ActionScript 3 (AS3) code samples. The nuanced departures from this workflow for native apps on mobile platforms are presented where appropriate. The Primetime DRM workflows are very similar across all platforms, however, so your understanding of the AS3 code will make extrapolation to other plaforms fairly straightforward.

**License Acquisition Process:**

1. Get the protected content's DRM metadata. 
1. Check if a license is available locally:

    * If the license is available locally, load the license and go to Step 6. 
    * If the license is not available locally, proceed to Step 3.

1. Check if authentication is required:

    * If authentication is required, get the authentication credentials from the user and pass them to the license server. 
    * If authentication is not required, go to Step 6.

1. If device domain registration is required, join the device domain. 
1. If authentication was needed and is now complete, download the license from the license server. 
1. Play the content.

If no errors occured and the user was successfully authorized to view the content, Primetime dispatches a `DRMStatusEvent` object and the application begins playback. The `DRMStatusEvent` object holds the related license information, which identifies the user's policy and permissions. For example, `DRMStatusEvent` may hold information regarding whether the content can be made available offline, when the license expires, and so on.

The application can use the license information to inform the user of the status of their policy. For example, the application can display the number of remaining days the user has for viewing the content in a status bar. If the user is allowed offline access, the license is cached, and the encrypted content is downloaded to the user's machine. The content is made accessible for the duration defined in the license caching duration. The detail property in the event contains `DRM.voucherObtained`. The application decides where to store the content locally in order for it to be available offline. You can also preload licenses using the `DRMManager` class.
