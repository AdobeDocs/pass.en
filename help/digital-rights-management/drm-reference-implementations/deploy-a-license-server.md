---
title: Deploy the license server
description: Deploy the license server
copied-description: yes
exl-id: 1439a5b2-eccb-41b7-a4d3-0673e727fb13
---
# Deploy the license server{#deploy-the-license-server}

1. Copy your reference implementation war files to the `webapps` directory on your Tomcat server.

   To use the reference implementation license server as is, you can simply copy the license server WAR file ( `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\\flashaccess.war`) to the `webapps` directory on your Tomcat server.

   If you are customizing the reference implementation license server, copy the server war files you built from `DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\refimpl-build\wars` to the `webapps` directory.     

   >[!NOTE]
   >
   >If you previously deployed license server WAR files, you might need to delete the unpacked WAR directories in the [!DNL webapps] directory on the Tomcat server:
   >
   >* [!DNL webapps/flashaccess] 
   >* [!DNL webapps/edcws] 

   >[!NOTE]
   >
   >Do not deploy [!DNL edsws.war] unless you require backwards compatibility with Flash Media Rights Management (FMRMS) v1.5 content. (This is a very rare requirement.) 
   >
   >If you prefer to prevent Tomcat from unpacking WAR files, edit `server.xml` in the `conf` directory and set `unpackWARs` to `false`. 

1. Copy the entire contents of the `[DRM SDK DVD]\Reference Implementation\Server\Reference Implementation Server\resources\` directory into your [!DNL tomcat] directory.

   The [!DNL resources] directory includes:

   * [!DNL flashaccesstools.properties] - The license server properties file. 
   * [!DNL log4j.xml] - License server logging configuration 
   * [!DNL *.pol] - Sample DRM policy files.

   In addition, you may also choose to copy the Adobe certification files to this location. 
    
1. Modify license server settings in [!DNL flashaccesstools.properties] to reflect your server setup.

   At a minimum, set values for the following properties:

   * `config.resourcesDirectory` 
   * `HandlerConfiguration.ServerTransportCredential` 
   * `HandlerConfiguration.ServerTransportCredential.password` 
   * `LicenseHandler.ServerCredential` 
   * `LicenseHandler.ServerCredential.password` 
   * `MetaDataConverter.SignatureParameters.ServerCredential` 
   * `MetaDataConverter.SignatureParameters.ServerCredential.password` 
   * `V2KeyParameters.LicenseServerUrl` 
   * `V2KeyParameters.KeyOptions.AsymmetricKeyOptions.Certificate` 
   * V2KeyParameters.LicenseServerTransportCertificate

1. Edit the `catalina.properties` file in your Tomcat `conf` directory; add the location of your [!DNL resources] directory (or the alternate location where you have stored your properties file and other resource files) to the `shared.loader` property.

   For example, if you have `flashaccess-refimpl.properties` located in [!DNL [Tomcat home]\resources\]: 

   ```
   shared.loader=..\resources
   ```

   This places `flashaccess-refimpl.properties` on the classpath.
1. Ensure that your other resource files ( [!DNL log4j.xml], policy files, certifications) are either in the [!DNL resources] directory or are otherwise on the classpath and their location specified in [!DNL flashaccess-refimpl.properties].

   You will likely want to initially run `log4j` in debug mode. In [!DNL log4j.xml], set `debug` to true: 

   ```
   <log4j:configuration xmlns:log4j="https://jakarta.apache.org/log4j/"<b>debug="true"</b>>
   ...
   ```

1. From the Tomcat [!DNL bin] directory, start your server.

   On Linux: 

   ```
   catalina.sh start
   ```

   On Windows: 

   ```
   catalina.bat start
   ```
