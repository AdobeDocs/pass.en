---
title: How to use the Primetime reference implementation
description: How to use the Primetime reference implementation
copied-description: yes
exl-id: 45145f0d-c0e4-4d36-94fd-72f07619dc91
---
# How to use the Primetime reference implementation {#how-to-use-the-primetime-reference-implementation}

The Primetime reference implementation is a modular player that has been broken down into individual features that you can easily modify through specialized feature managers. These feature managers are used as a bridge to connect the application and the TVSDK library.

You can use the reference implementation in the following ways:

* Use it as-is without changing any code (all features are turned on with default values). 
* Use it as a reference to understand how to use the TVSDK library. 
* Pick and choose the features that apply to your application by turning off the features that you don't use. 
* Customize the UI components without making any changes to the features.

We provide the Primetime reference implementation to help you understand the TVSDK and easily modify the feature managers to customize your player. However, please refer to the [TVSDK 1.4 for Android Programmer's Guide](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android.pdf) for detailed information about the TVSDK library.

For easy access to the reference implementation API documentation in Javadoc format, click [here](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/index.html).
