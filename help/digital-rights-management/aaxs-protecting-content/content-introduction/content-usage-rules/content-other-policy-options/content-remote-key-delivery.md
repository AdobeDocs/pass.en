---
title: Remote and Local iOS Key Delivery
description: Remote and Local iOS Key Delivery
copied-description: yes
exl-id: de9c7070-46a9-453c-9d98-a9f161282cfa
---
# Remote and Local iOS Key Delivery{#remote-and-local-ios-key-delivery}

Adobe Primetime supports two options for key delivery to iOS clients:

* Remote - Exactly as specified in the HLS specification, the M3U8 manifest specifies an HTTPS path that contains an AES key that should be used to decrypt the following encrypted segments in the stream. When "Remote" is specified, the client device will reach out to a remote HTTPS server to fetch the AES key. 
* Local - When "Local" is specified, instead of reaching out over the internet/network for the AES key, a local HTTPS server is embedded into the iOS application which will handle all AES key requests. The embedded HTTPS server is automatically set up and configured in the Primetime application. No intervention is required by the application developer.

The remote key delivery is enabled through the policy used to package content (changing this setting requires repackaging of content), When remote key delivery is enabled, an Adobe Access Key Server must be deployed to handle key requests from iOS clients, but there is no change to the workflow for clients on other platforms.

>[!NOTE]
>
>The Key delivery selection only impacts iOS clients. All other devices that consume HLS content will always use "Local" key delivery, even if "Remote" has been specified.

For information, see *Using the Adobe Access Key Server*.
