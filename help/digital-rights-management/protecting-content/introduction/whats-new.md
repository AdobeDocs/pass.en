---
description: Adobe Primetime DRM is an advanced Digital Rights Management (DRM) and content protection solution for high-value audiovisual content. In applications that support the creation of Java APIs, you can use the Primetime DRM SDK to specify DRM policies, apply those policies to content, and encrypt that content.
title: What is new in Adobe Primetime DRM
exl-id: 998dae80-b3d3-419e-8fd3-d925a83d8b53
---
# What is new in Adobe Primetime DRM{#what-is-new-in-adobe-primetime-drm}

Adobe Primetime DRM is an advanced Digital Rights Management (DRM) and content protection solution for high-value audiovisual content. In applications that support the creation of Java APIs, you can use the Primetime DRM SDK to specify DRM policies, apply those policies to content, and encrypt that content.

>[!NOTE]
>
>Primetime DRM was formerly called Adobe Access, and prior to that, Flash Access.

Here is a high level walk-through of the content protection process:

1. Use the DRM Java APIs to set DRM policy properties and encryption parameters. 
1. Create a DRM policy that describes the usage roles for any content.

   You can create any number of DRM policies. Most users create a small number of policies, and then apply them to many files. 
1. Package a media file.

   *`Packaging a file`* means that you encrypt the file and then apply a DRM policy to the file. 
1. Implement the license server to issue a license to the user.

With the completion of these steps, your encrypted content is ready for deployment. After deployment, a client can request a license from the license server, and upon receipt can play the content.

The Primetime DRM SDK provides a Java API to complete these tasks. The SDK includes reference implementations of the license server and command-line tools, both of which are based on the DRM SDK Java APIs.

The features described below are new in this release.

## New Features {#section_F6BA874CEAE24610920BC3A4C6D20EBA}

* **Hard Stop -** You can specify whether playback stops or continues at the end of a playback window. 
* **Resolution dependent output controls -** You can specify output constraints based on pixel resolutions. 
* **Anonymization of License Server Responses -** To enhance the privacy with Primetime DRM License Server protocols, the transport certificate serial number will be zeroed for license server responses to supporting clients.
