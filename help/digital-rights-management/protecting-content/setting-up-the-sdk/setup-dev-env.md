---
description: If you want to set up Primetime DRM, copy the files from the DVD. These files include JAR files that include code, certificates, and third-party classes. In addition, you need to request a certificate from Adobe Systems, Incorporated. Adobe then issues you multiple credentials that you use to protect the integrity of your packaged content, licenses, and communication between client and server.
title: Set up your development environment
exl-id: c10f85b6-84bc-444f-9001-f49dc88cf99c
---
# Set up your development environment {#set-up-your-development-environment}

If you want to set up Primetime DRM, copy the files from the DVD. These files include JAR files that include code, certificates, and third-party classes. In addition, you need to request a certificate from Adobe Systems, Incorporated. Adobe then issues you multiple credentials that you use to protect the integrity of your packaged content, licenses, and communication between client and server.

Adobe provides the Primetime DRM SDK on DVD: 

1. Copy the following files from [!DNL [DRM DVD]/SDK/] to your development system (on your Java classpath):

    * [!DNL adobe-flashaccess-certs.jar] - Includes Adobe root certificates 
    * [!DNL adobe-flashaccess-sdk.jar] - Includes Primetime DRM Core SDK classes 
    * [!DNL adobe-flashaccess-sdk-pro.jar] - Includes Primetime DRM Professional SDK classes, required only for Professional features

1. Copy the following files from [!DNL [DRM DVD]/SDK/thirdparty] to your development system:

    * [!DNL bcmail-jdk15-141.jar] 
    * [!DNL bcprov-jdk15-141.jar] 
    * [!DNL commons-discovery-0.4.jar] 
    * [!DNL commons-logging-1.1.1.jar] 
    * [!DNL cryptoj.jar] 
    * [!DNL jaxb-api.jar] 
    * [!DNL jaxb-impl.jar] 
    * [!DNL jaxb-libs.jar] 
    * [!DNL relaxngDatatype.jar] 
    * [!DNL rm-pdrl.jar] 
    * [!DNL xsdlib.jar] 
    * [!DNL jackson-annotations-2.4.0-rc4-20140522.175222-3.jar] 
    * [!DNL jackson-core--2.4.0-rc4-20140529.184520-13.jar] 
    * [!DNL jackson-databind-2.4.0-rc4-20140603.005043-38.jar]

1. (Optional) For improved performance, you can enable native support for cryptographic operations by copying the appropriate platform-specific library from [!DNL [DRM DVD]/SDK/thirdparty/cryptoj/] to your development system (remember to place the location on your path):

    * [!DNL jsafe.dll] - Windows 
    * [!DNL libjsafe.so] - Linux

       >[!NOTE]
       >
       >32-bit and 64-bit versions of these libaries are available. You should only use the 64-bit version if you have a 64-bit OS and you run the 64-bit version of Java.

1. (Optional) For functionality related to Adobe Flash Media Rights Management Server (FMRMS) 1.x compatibility, copy `[DRM DVD]/SDK/adobe-flashaccess-lcrm.jar]` to your development system:

   Deploy this only if you previously deployed FMRMS 1.x and do not want to re-package your FMRMS-protected content. In this case, you must add this support to your license server so it can manage old content and clients.
