---
title: Deploying the Adobe Primetime DRM Server for Protected Streaming
description: Deploying the Adobe Primetime DRM Server for Protected Streaming
copied-description: yes
exl-id: 814c08e6-5d09-495b-b529-cedc9b9c02a7
---
# Deploying the Adobe Primetime DRM Server for Protected Streaming{#deploying-the-adobe-primetime-drm-server-for-protected-streaming}

Before you can deploy the Adobe Primetime DRM Server for Protected Streaming, you must have installed the versions of Java and Tomcat as listed in the Requirements topic.

The Primetime DRM Server for Protected Streaming package includes [!DNL flashaccesserver.war]. If you:

* Want to deploy this WAR file, you need to copy it to Tomcat's [!DNL webapps] directory. 
* Have previously deployed the WAR file, you may need to delete the unpacked WAR directory ( [!DNL flashaccessserver] in Tomcat's [!DNL webapps] directory). 

* Want to prevent Tomcat from unpacking WAR files, edit the [!DNL server.xml] file in Tomcat's [!DNL conf] directory and configure the `unpackWARs` attribute iby setting it to `false`.

>[!NOTE]
>
>If you have configured Tomcat to include [!DNL commons-logging.jar] on the System classpath (not required for the Primetime DRM Server for Protected Streaming) then you must configure commons-logging to use Log4J.

The server optionally uses a platform-specific library ( [!DNL jsafe.dll] on Microsoft Windows or [!DNL libjsafe.so] on Linux for optimal performance. You can copy the appropriate library for your platform from [!DNL thirdparty/cryptoj/]*platform* to a location that is specified by the `PATH` environment variable or `LD_LIBRARY_PATH` on Linux.

>[!NOTE]
>
>You should only use the 64-bit version if both the operating system and the JDK support 64 bit. Otherwise you need to use the 32-bit version.
