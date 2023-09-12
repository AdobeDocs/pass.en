---
title: Building the license server
description: Building the license server
copied-description: yes
exl-id: 0535f1e4-9f63-47a0-b55c-45c32ba0d15e
---
# Building the license server {#building-the-license-server}

The reference implementation license server includes WAR files for deploying the license server. It also includes all the license server source code and an Ant build script (Reference Implementation\Server\refimpl\build-refimpl.xml) so you can easily make changes to the code.

>[!NOTE]
>
>This step is only needed if you want to modify the source code. For evaluation purposes, you can skip this step and use the WAR files as shipped.

Before running the Ant script, modify the script to specify the locations of the Adobe Access SDK, Tomcat, MySQL, and Log4J. Open build-refimpl.xml in a text editor and edit the values of the properties `sdkdir, tomcatdir, mysqldir, and log4jdir`. To compile the source code and create the WAR files for the reference implementation, run the script using `ant -f build-refimpl.xml all` in the directory containing the Ant script. When the script is complete, a [!DNL refimpl-build/wars] directory containing the server WAR files will be created.
