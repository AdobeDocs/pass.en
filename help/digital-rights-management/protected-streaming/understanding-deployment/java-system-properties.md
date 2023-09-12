---
description: There are several Java System properties that you can configure on the license server to control the location of configuration and log files.
title: Java system properties
exl-id: 08fe6910-9d58-41c3-91d3-514406bedf05
---
# Java system properties{#java-system-properties}

There are several Java System properties that you can configure on the license server to control the location of configuration and log files.

You can optionally configure the following Java System properties:

* *`LicenseServer.ConfigRoot`* — Name of directory that includes the configuration files for the license server.

  See *License server configuration files* for details about the contents of these files. If not configured, the default value is `CATALINA_BASE/licenseserver`. 

* *LicenseServer.LogRoot* — Name of the [!DNL logs] directory in which license server application logs are located. If you have not modified the name of this directory, then the name of this directory is configured as *LicenseServer.ConfigRoot* by default.

If you use the [!DNL catalina.bat] or [!DNL catalina.sh] file to start Tomcat, you can configure the System properties with the `JAVA_OPTS` environment variable. Any Java options that you configure are automatically applied when Tomcat starts.

For example, you can configure the `JAVA_OPTS` environment variable as follows:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" 
  -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
