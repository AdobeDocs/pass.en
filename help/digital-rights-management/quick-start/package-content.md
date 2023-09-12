---
title: Package encrypted content
description: Package encrypted content
copied-description: yes
exl-id: e5792917-8172-48b0-8792-7a7e942596c5
---
# Package encrypted content{#package-encrypted-content}

1. Copy the `<Primetime DRM DVD>\Reference Implementation\Command Line Tools\` directory to your local filesystem.
1. In your local `Command Line Tools\` folder, update the `flashaccesstools.properties` file to work with your server.

   You must modify at least the following properties:

    * `encrypt.keys.asymmetric.certfile=[license-server-certificate.cer]`: The path to your License Server Certificate (it usually ends with [!DNL .cer], [!DNL .der] or [!DNL .pem]). 
    
    * `encrypt.license.serverurl=[license-server-url]`: Your license server URL, e.g.:    `https://<License Server Hostname>:8080/flashaccessserver/sampletenant`. 
    
    * `encrypt.license.servercert=[transport-certificate.cer]`: The path to your Transport certificate (it usually ends with [!DNL .cer], [!DNL .der], or [!DNL .pem]). 
    
    * `encrypt.sign.certfile=[packager-credentials.pfx]`: The path to your Packager certificate (this ends with [!DNL .pfx]). 
    
    * `encrypt.sign.certpass=[password]`: The password for your Packager certificate.     
    
    >[!NOTE]
    >
    >Ensure that you do not scramble the password.

1. Create a policy.

   In your local `Command Line Tools\` folder, run the following command: 

   ```
   java -jar libs/AdobePolicyManager.jar new examplepolicy.pol -n examplepolicy -x
   ```

   This command creates a policy file named [!DNL examplepolicy.pol] that uses anonymous license server authentication (the `-x` option).
1. Copy the MP4, FLV, or F4V video file that you want to encrypt into your local `Command Line Tools\` folder.
1. Package your content.

   Let's say that your source video file is [!DNL sample.mp4]. In your local `Command Line Tools\` folder, run the following command: 

   ```
   java -jar libs/AdobePackager.jar sample.mp4 sample_encrypted.mp4 -p examplepolicy.pol
   ```

   >[!NOTE]
   >
   >If you want to package HLS, HDS or DASH contents, you must use a different packager tool, such as [Adobe Primetime Offline Packager](https://helpx.adobe.com/content/dam/help/en/primetime/guides/offline_packager_getting_started.pdf).

1. Copy the encrypted file artifacts (in this case [!DNL sample_encrypted.mp4] and [!DNL sample_encrypted.mp4.metadata]) to `<Your Content Server - Tomcat Install Dir>\webapps\ROOT`.

At this point you have completed the packaging phase of the process.

>[!NOTE]
>
>For more detailed information on command-line tools for packaging content, creating policies, and more, see [Adobe Primetime DRM Command-line tools](../drm-reference-implementations/command-line-tools/command-line-tools-overview.md).
