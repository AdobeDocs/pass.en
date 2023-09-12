---
title: Deploying the license server and watched folder packager overview
description: Deploying the license server and watched folder packager overview
copied-description: yes
exl-id: b44aec8b-f1d7-4dce-bc51-0ce2b74ae0c1
---
# Deploying the license server and watched folder packager overview {#deploying-the-license-server-and-watched-folder-packager-overview}

Copy the license server WAR files to Tomcat's [!DNL webapps] directory. If you have previously deployed the WAR file, you may need to manually delete the unpacked WAR directories ( [!DNL flashaccess], [!DNL edcws], and [!DNL flashaccess-packager] in Tomcat's [!DNL webapps] directory). To prevent Tomcat from unpacking WAR files, edit the [!DNL server.xml] file in Tomcat's conf directory and set the `unpackWARs` attribute to `false`.

The properties file ( [!DNL flashaccess-refimpl.properties]) must be on the classpath for the server to load the properties. Copy this file to a directory and update the file with the appropriate values. Edit the [!DNL catalina.properties] file in Tomcat's [!DNL conf] directory and add the directory containing [!DNL flashaccess-refimpl.properties] to the `shared.loader` property. The [!DNL log4j.xml] file for configuring logging must also be on the classpath (see [!DNL resources\log4j.xml] for an example).

The reference implementation server uses several certificate files, policy files, and other resources. Those files are all located in one resource folder. By default, the resource folder is [!DNL C:\flashaccess-server-resources], but this location can be modified in [!DNL flashaccess-refimpl.properties]. Be sure to copy all the required resources to this location before starting the server.

To start Tomcat and the license server, run `catalina.bat start` from Tomcat's [!DNL bin] directory.
