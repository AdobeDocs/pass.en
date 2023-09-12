---
description: The reference implementation server can help you create a fully functional license server that uses all of the features of the Adobe Primetime DRM Java SDK.
title: License server
exl-id: a928b7ac-9191-4b8c-b038-eb92a09286fa
---
# License server {#license-server}

The reference implementation server can help you create a fully functional license server that uses all of the features of the Adobe Primetime DRM Java SDK.

In this implementation, users are authenticated based on user entries in a database. The server includes demonstration business logic for issuing licenses and provides compatibility support for Flash Media Rights Management Server 1.0 and 1.5.

## License server requirements {#license-server-requirements}

License server requirements:

* Install Tomcat 6.0 or later 
* Install a database, e.g., MySQL (available on the DVD, in [!DNL Third Party\MySQL])
* Ensure you have Java 1.6 or later installed
* To run the sample build scripts, ensure that you have Ant 1.8 or later

After you install Tomcat and MySQL, contact Adobe for your set of required DRM credentials.

## Build the license server {#build-the-license-server}

>[!NOTE]
>
>Building the license server is only necessary if you intend to modify the source code. For evaluation purposes, you can simply use the WAR files as shipped.

The reference implementation license server includes all of the license server source code ( `([DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\src/`), along with an Ant build script ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl/build-refimpl.xml`) with which you can customize the license server to suit your business needs. 

1. Modify the Ant build script to specify the locations of your Primetime DRM SDK, Tomcat, MySQL, and Log4J.

   Open the [!DNL build-refimpl.xml] file in a text editor and set these property values:

   * `sdkdir` 
   * `tomcatdir` 
   * `mysqldir` 
   * `log4jdir`

1. Run the Ant build script with the `all` property, in the directory where the Ant build script is located.

   ```
   ant -f build-refimpl.xml all
   ```

   The Ant build script creates a [!DNL refimpl-build/wars] directory that includes the server WAR files.
