---
title: License preview
description: License preview
copied-description: yes
exl-id: 7e6b1062-7240-4dae-86bb-bd26e7be1f14
---
# License preview{#license-preview}

The client can send a license preview request, meaning that the application can carry out a preview operation before asking the user to buy the content in order to determine whether the user's machine actually meets all the criteria required for playback.

*`License preview`* refers to a client's ability to preview the license (to see what rights the license permits) as opposed to previewing the content (viewing a small portion of the content before deciding to buy). Some of the parameters that are unique to each machine are: outputs available and their protection status, the runtime/DRM version available, and the DRM client security level. The license preview mode allows the runtime/DRM client to test the license server business logic and provide information back to the user so he can make an informed decision. Thus the client can see what a valid license looks like but would not actually receive the key to decrypt the content. Support for license preview is optional, and only necessary if you implement a custom client that uses this functionality.

To determine whether the client sent a preview request or license acquisition request, call `LicenseRequestMessage.getRequestPhase()`and compare it to `LicenseRequestMessage.RequestPhase.Acquire`
