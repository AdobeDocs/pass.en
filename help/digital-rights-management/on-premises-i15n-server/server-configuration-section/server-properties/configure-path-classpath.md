---
title: Configure the Path and Classpath
description: Configure the Path and Classpath
copied-description: yes
exl-id: e6e9f837-4e3d-43e1-971d-3fa0ccaeff39
---
# Configure the Path and Classpath{#configure-the-path-and-classpath}

The [!DNL flashaccess.war] contains [!DNL jsafeWithNative.jar], which is the Crypto-J library. The latter requires an additional native library to perform crypto operations. 

1. Add the native [!DNL jsafe] library to your path.

    * **Linux / [!DNL libjsafe.so] -** The directory containing [!DNL libjsafe.so] must be on the Path (native Crypto-J libraries are also available for other platforms). For example, set [!DNL libjsafe.so] on `LD_LIBRARY_PATH`. 
    
    * **Windows / [!DNL jsafe.dll] -** The counterpart on Windows to [!DNL libjsafe.so] is the appropriate [!DNL jsafe.dll].

   These libraries are available to you in the [!DNL thirdparty] library folder.
1. Put one of the [!DNL adobe-flashaccess-certs] jar files on the classpath.

       This JAR file is not included in the WAR file; you must add it explicitly to the classpath.

    * Development servers - Should only use [!DNL adobe-flashaccess-certs-prerelease.jar]. 
    * Production servers - Should only use [!DNL adobe-flashaccess- certs.jar]

The distribution includes a [!DNL shared] folder that includes both the jar file as well as a pre-configured [!DNL AdobeInitial.properties] file. Adobe recommends that you add these items to the `common.loader` via the [!DNL catalina.properties] file. For example:

```
common.loader=<Any Pre-Existing Values>,${catalina.home}/shared/classes,${catalina.home}/shared/lib/*.jar
```
