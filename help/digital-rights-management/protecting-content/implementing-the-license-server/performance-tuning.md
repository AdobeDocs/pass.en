---
title: Performance tuning
description: Performance tuning
copied-description: yes
exl-id: 1b54b7c2-da32-47db-b57f-b2afbaf386c4
---
# Performance tuning{#performance-tuning}

Use the following tips to help to increase performance:

* Using a network HSM can be significantly slower than using a directly-connected HSM. 
* For improved performance, you can optionally enable native support for cryptographic operations by deploying the platform-specific libraries located in the [!DNL thirdparty/cryptoj] folder of the SDK. To enable native support, add the library for your platform (jsafe.dll for Windows or libjsafe.so for Linux) to the path. 

  >[!NOTE]
  >
  >If you run multiple web applications in the same Tomcat instance and have `jsafe.dll` on the path, only the first web application that loads is able to load the `jsafe.dll` library. Therefore, only the first web application gets the benefit of the native support. In such cases, to improve the performance of all web applications, place `cryptoj.jar`outside of the WAR file. For example, in the `<tomcat_installation_folder>/lib` directory.

* A 64-bit operating system, such as the 64-bit version of Red Hat® or Windows, provides much better performance over a 32-bit operating system.

## Generating random numbers (Linux) {#section_3E2E936A538F40B7BF8892C65E117907}

Under certain conditions Linux environments may pause when conducting Primetime DRM-related operations that require random number generation, including:

* Startup of the Adobe Primetime DRM License Server 
* Policy generation using the [!DNL AdobePolicyManager] utility 
* Packaging DRM-protected content with Adobe Media Server or the Primetime OfflinePackager

Delays during these operations are often the result of a low entropy pool on your Linux server.

On Linux, random numbers are generated from the server environment's entropy pool. The entropy pool is normally maintained by receiving hardware interrupts by the Linux kernel. If a server is isolated and does not receive regular input from HW resources (such as a mouse or keyboard), the waits to refill the entropy pool may be extended. In this scenario, operations waiting for data from [!DNL /dev/random] may pause.

You can use hardware random number generators on Linux servers to ensure that sufficient entropy is generated. However, if hardware random number generators are not available in a given deployment scenario, you can use software based solutions to augment the entropy pool refresh rate. One such software solution on Linux is [!DNL haveged] (HArdware Volatile Entropy Gathering and Expansion daemon).

## Determining Available Entropy {#section_686B311FE6144566B6939E9F20915ADC}

To verify the number of bits available in a given server's entropy pool during an unexpected delay, execute the following command: 

```
cat /proc/sys/kernel/random/entropy_avail 
```

A healthy Linux system with a lot of entropy available will return close to the full 4,096 bits of entropy. If the value returned is less than 200, the system is running very low on entropy.
