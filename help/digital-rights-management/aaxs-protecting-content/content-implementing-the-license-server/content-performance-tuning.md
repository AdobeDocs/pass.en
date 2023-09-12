---
title: Performance tuning
description: Performance tuning
copied-description: yes
exl-id: f6b2338e-a209-4881-a599-ded5f1498daf
---
# Performance tuning{#performance-tuning}

Use the following tips to help to increase performance:

* Using a network HSM can be significantly slower than using a directly-connected HSM. 
* For improved performance, you can optionally enable native support for cryptographic operations by deploying the platform-specific libraries located in the "thirdparty/cryptoj" folder of the SDK. To enable native support, add the library for your platform (jsafe.dll for Windows or libjsafe.so for Linux) to the path.

  >[!NOTE]
  >
  >If you run multiple web applications in the same Tomcat instance and have `jsafe.dll` on the path, only the first web application that loads is able to load the `jsafe.dll` library. Therefore, only the first web application gets the benefit of the native support. In such cases, to improve the performance of all web applications, place `cryptoj.jar`outside of the WAR file. For example, in the `<tomcat_installation_folder>/lib` directory.

* A 64-bit operating system, such as the 64-bit version of Red Hat® or Windows, provides much better performance over a 32-bit operating system.
