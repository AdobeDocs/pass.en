---
description: Adobe provides a Cloud DRM service to Adobe Primetime DRM customers who do not wish to develop and maintain their own Primetime DRM License Server. By utilizing this service, customers can reduce the operational and development complexity around DRM license issuance. Primetime Cloud DRM can issue DRM licenses to all devices capable of running a Primetime Browser TVSDK-enabled video application, such as iOS, Android, Desktops, and Xbox360. This DRM service is hosted and maintained by Adobe, with 24/7 uptime.
title: Background
exl-id: bb5ad080-5b1d-43a6-8d0e-9b5735c82d96
---
# Background {#background}

Adobe provides a Cloud DRM service to Adobe Primetime DRM customers who do not wish to develop and maintain their own Primetime DRM License Server. By utilizing this service, customers can reduce the operational and development complexity around DRM license issuance. Primetime Cloud DRM can issue DRM licenses to all devices capable of running a Primetime Browser TVSDK-enabled video application, such as iOS, Android, Desktops, and Xbox360. This DRM service is hosted and maintained by Adobe, with 24/7 uptime.

>[!NOTE]
>
>Adobe Primetime DRM was formerly called Adobe Access, and prior to that, Flash Access.

## What is included with Primetime Cloud DRM {#section_788D0DD5F6DB41678FD87CFBD21B25FD}

* Custom Authentication/Entitlement module and instructions on how to engage custom authentication for your content. For more documentation, please refer to the [!DNL Custom Authentication Entitlement] directory. 
* Cloud DRM-specific License Server certificate ( [!DNL .pem/.cer/.der]) 

* Cloud DRM-specific License Server Transport certificate ( [!DNL .pem/.cer/.der]) 

* Primetime Java Offline Packager 
* Sample DRM Policies for Packaging

    * **policy_24hr** - Licenses cache on disk for 24 hours. After 24 hours, a new license must be acquired to view the content. All other policies in this kit also have 24 hour license caching. 
    * **policy_ios_remotekeyserver** - On iOS devices, the DRM license will be acquired from  Cloud DRM. In addition, the client will acquire all AES decryption keys from Cloud DRM. Playback is disallowed on jailbroken iOS devices. 
    
    * **policy_ios_localkeyserver** - On iOS devices, the DRM license will be acquired from  Cloud DRM. In addition, the client will acquire all HLS AES decryption keys from a local HTTP server, instead of  Cloud DRM. Playback is disallowed on jailbroken iOS devices. 
    
    * **policy_adobePass** - The client must first authenticate with  (formerly called Adobe Pass) or a license will be denied.

* Adobe Policy Manager tool to create additional DRM policies 
* Sample video content to use for packaging
