---
description: To set up the Adobe® Access™ for use, copy files from the DVD. These files include JAR files containing code, certificates, and third-party classes. In addition, request a certificate from Adobe Systems Incorporated. You will be issued multiple credentials used to protect the integrity of packaged content, licenses, and communication between the client and server.
title: Setting up the development environment
exl-id: 66310fc8-7513-4aab-81d6-1370ce216cbf
---
# Setting up the SDK {#setting-up-the-sdk}

To set up the Adobe® Access™ for use, copy files from the DVD. These files include JAR files containing code, certificates, and third-party classes. In addition, request a certificate from Adobe Systems Incorporated. You will be issued multiple credentials used to protect the integrity of packaged content, licenses, and communication between the client and server.

The Adobe Access SDK is available in two types:
* Adobe Access Core SDK
* Adobe Access Professional SDK

The following table shows a basic comparison of Adobe Access SDKs:

| Feature |Adobe Access Core SDK |Adobe Access Professional SDK|
|---|---|---|
| Flash Access 2.0 features |Available |Available |
| Key rotation |- |Available |
| Domain Support |Available |Available |
| Enhanced License Chaining |Available |Available |
| Synchronization Messages  |Available |Available |
| License Pre-Generation  |Available |Available |
| Embedded Licenses |Available |Available |

## Setting up the development environment {#setting-up-the-development-environment}

From the DVD, copy the following SDK files for use in your development environment and your Java classpath:

* adobe-flashaccess-certs.jar (contains Adobe root certificates) 
* adobe-flashaccess-sdk.jar (contains Adobe Access Core SDK classes) 
* adobe-flashaccess-sdk-pro.jar (contains Adobe Access Professional SDK classes, required only for Professional features)

You need the following third party JAR files also located on the DVD in the SDK's "thirdparty" folder:

* bcmail-jdk15-141.jar 
* bcprov-jdk15-141.jar 
* commons-discovery-0.4.jar 
* commons-logging-1.1.1.jar 
* cryptoj.jar 
* jaxb-api.jar 
* jaxb-impl.jar 
* jaxb-libs.jar 
* relaxngDatatype.jar 
* rm-pdrl.jar 
* xsdlib.jar

For improved performance, you can optionally enable native support for cryptographic operations by deploying the platform-specific libraries located in the "thirdparty/cryptoj" folder of the SDK. To enable native support, add the library for your platform (jsafe.dll for Windows or libjsafe.so for Linux) to the path. The 32-bit and 64-bit versions of these libaries are provided. (Note that the 64-bit version should only be used if you have a 64-bit OS and you are running the 64-bit version of Java).

Additionally, an optional part of the SDK is adobe-flashaccess-lcrm.jar. This file is only needed for functionality related to Adobe Flash Media Rights Management Server (FMRMS) 1.x compatibility. If you previously deployed FMRMS 1.x and do not want to re-package your FMRMS-protected content, you must add support to your license server so it will be able to handle old content and clients.
