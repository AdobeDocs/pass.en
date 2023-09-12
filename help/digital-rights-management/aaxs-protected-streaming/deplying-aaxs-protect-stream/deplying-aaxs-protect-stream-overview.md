---
title: Deploying the Adobe Access Server for Protected Streaming overview
description: Deploying the Adobe Access Server for Protected Streaming overview
copied-description: yes
exl-id: fdefa13a-14ec-4301-ab39-2ceea830463d
---
# Deploying the Adobe Access Server for Protected Streaming overview {#deploying-the-adobe-access-server-for-protected-streaming-overview}

Before deploying the Adobe Access Server for Protected Streaming, make sure you have installed the versions of Java and Tomcat listed in the Requirements section.

The Adobe Access Server for Protected Streaming package includes [!DNL flashaccesserver.war]. To deploy this WAR file, copy it to Tomcat's [!DNL webapps] directory. If you have previously deployed the WAR file, you may need to manually delete the unpacked WAR directory ( [!DNL flashaccessserver] in Tomcat's [!DNL webapps] directory). To prevent Tomcat from unpacking WAR files, edit the [!DNL server.xml] file in Tomcat's [!DNL conf] directory and set the `unpackWARs` attribute to `false`.

>[!NOTE]
>
>If you have configured Tomcat to include [!DNL commons-logging.jar] on the System classpath (not required for the Adobe Access Server for Protected Streaming), commons-logging must be configured to use Log4J.

The server optionally uses a platform-specific library ( [!DNL jsafe.dll] on Microsoft Windows or [!DNL libjsafe.so] on Linux) for optimal performance. Copy the appropriate library for your platform from [!DNL thirdparty/cryptoj/]*platform* to a location specified by the `PATH` environment variable (or `LD_LIBRARY_PATH` on Linux).

>[!NOTE]
>
>The 64-bit version should only be used if both the operating system and JDK support 64-bit, otherwise use the 32-bit version.
