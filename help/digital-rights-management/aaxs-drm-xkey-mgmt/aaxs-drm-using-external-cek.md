---
description: Use the External CEK feature to vend and package licenses using your existing CKMS.
title: Using External CEK to Vend and Package Licenses
exl-id: 3944624a-099e-4fc0-b829-6ab154a53758
---
# Using External CEK to Vend and Package Licenses{#using-external-cek-to-vend-and-package-licenses}

Use the External CEK feature to vend and package licenses using your existing CKMS.

## EncryptContentWithExternalKey.java

This is a command line tool that will AAXS-encrypt a video and create metadata that will *not* contain the CEK (protected with an AAXS license server's public cert). Instead, the tool embeds a CEK ID into the video's metadata.

During license acquisition, the AAXS license server observes a flag in the metadata identifying that this content was protected using an External CEK. The license server will extract the CEK ID from the metadata and then query a secure repository/CKMS to retrieve the appropriate CEK.

## Packaging Workflow

1. Ensure you are using Java 1.6.0_24 or later.
1. To see the tool usage: `java -jar AdobePackager_ExternalCEK.jar`
1. To package content: 

   ```
   java -jar AdobePackager_ExternalCEK.jar sample.flv encrypted.flv abc abcdef0123456789 
       policy.pol https://path-to-your-server:8090 <license-server-public-cert.pem> 
       <license-server-private-key.pfx> <private-key-password>
   ```

>[!NOTE]
>
>* The Java source code can be built using the included ANT `build-samples.xml`
>* The Flash Access SDK ( `adobe-flashaccess-sdk.jar`) must be on the classpath
>

## Server Workflow

1. Set up the Reference Implementation.
1. If any exist, clean up previous Reference Implementation deployments:

    1. `delete <tomcat>\work\Catalina\*.*`
    1. `delete <tomcat>\conf\Catalina\*.*`
    1. `delete <tomcat>\logs\*.*`

1. Verify that there is a [!DNL CEKDepot.properties] file alongside your [!DNL flashaccess-refimpl.properties] 

1. Initiate a license request from an Adobe Primetime Player 
1. Observe Ref Impl logs for something similar to: 

   ```
   DEBUG [com.adobe.flashaccess.refimpl.web.RefImplLicenseReqHandler.REQUESTS] 
     Used CEK ID:{abc} to retrieve CEK: {abcdef0123456789} from depot
   ```

    1. You may have to change your [!DNL log4j.xml] settings to log at a `DEBUG` level ( `INFO` is set by default)

## Known Issues

None
