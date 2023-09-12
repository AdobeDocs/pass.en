---
title: Java system properties
description: Java system properties
copied-description: yes
exl-id: 3fac8fac-7c71-4638-a671-eecc203dc871
---
# Java system properties {#java-system-properties}

The following two Java System properties may optionally be set to modify the location of configuration and log files for the license server:

* *LicenseServer.ConfigRoot* — Directory containing all the configuration files for the license server. For details on the contents of these files, see "[License server configuration files](../../aaxs-protected-streaming/aaxs-license-server-config-files/aaxs-configuration-directory-structure.md)". If not set, the default is *CATALINA_BASE/licenseserver*. 
* *LicenseServer.LogRoot* — Directory of the "logs" folder, where license server application logs are written. If not set, the default is *LicenseServer.ConfigRoot*.

If you are using [!DNL catalina.bat] or [!DNL catalina.sh] to start Tomcat, these System properties can easily be set using the `JAVA_OPTS` environment variable. Any Java options set here will be used when Tomcat is started. For example, set:

```
JAVA_OPTS=-DLicenseServer.ConfigRoot="absolute-path-to-config-folder" -DLicenseServer.LogRoot="absolute-path-to-log-folder"
```
