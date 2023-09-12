---
description: The ConfigProvider class gets the configuration for the media player. You must implement the configuration interface so the feature managers can read the configuration information.
title: ConfigProvider
exl-id: 75613bfb-3c2b-4b53-b365-adc98f7e1164
---
# ConfigProvider {#configprovider}

The ConfigProvider class gets the configuration for the media player. You must implement the configuration interface so the feature managers can read the configuration information.

You use the [ConfigProvider](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/ConfigProvider.html) class to implement the `ICCConfig`, `IAAConfig`, `IPlaybackConfig`, `IAdConfig`, and `IQosConfig` configuration interfaces so that the feature managers can read the configurations. For example, the `ICCConfig` is the interface for the `CCManager` configuration. The configuration files receive the configuration parameters from the JSON configuration file.

The `ConfigProvider.java` file is an example of Adobe's implementation of the configuration interfaces. It reads the settings from `SharedPreferences`, where the configuration is stored. You can store your configuration in any way that works for your organization. The config implementation provides a wrapper for your configuration source.
