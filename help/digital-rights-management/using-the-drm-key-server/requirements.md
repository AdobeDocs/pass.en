---
title: Requirements for using Primetime DRM Key Server
description: Requirements for using Primetime DRM Key Server
copied-description: yes
exl-id: a5c0db05-15a1-45b0-abb9-11f857f5e34c
---
# Introduction {#introduction}

Primetime DRM Key Server is a multi-tenant Key Server for Remote iOS and / or Xbox 360 key delivery. If Remote Key Delivery is enabled in a policy for iOS, a Primetime DRM Key Server must be deployed in order to enable content playback on iOS clients. Primetime DRM Key Server is always required for Xbox 360. 

## Requirements for using Primetime DRM Key Server {#requirements-for-using-primetime-drm-key-server}

The minimum requirements for using Primetime DRM Key Server are:

* [Java JRE 1.6](https://www.oracle.com/technetwork/java/javase/downloads/index.html) or later. (In order to use HSM on Windows 64 bit, JRE 8 is required) 

  >[!NOTE]
  >
  >64-bit PKCS11 is now supported in OpenJDK 8: [https://openjdk.java.net/jeps/131](https://openjdk.java.net/jeps/131), and Oracle
* [Apache Tomcat 7](https://tomcat.apache.org) 
* Credentials issued by Adobe 
* Credentials issued by Microsoft (for Xbox 360 clients)
