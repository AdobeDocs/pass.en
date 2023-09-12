---
description: The flashaccess-global.xml configuration file includes settings that apply to all tenants of the license server.
title: Global configuration file
exl-id: 3e74bce6-1634-469f-9d02-1121e9d50687
---
# Global configuration file{#global-configuration-file}

The flashaccess-global.xml configuration file includes settings that apply to all tenants of the license server.

You must place the configuration file in the [!DNL LicenseServer.ConfigRoot] directory.

See the [!DNL configs] directory for an example of a global configuration file.

The global configuration file includes:

* Caching — Controls caching of config files in memory.

  See *Updating configuration files* for information about the caching settings. 
* Logging — Specifies the logging level and how frequently log files are rolled. 
* HSM password — Required only if an HSM is used to store server credentials.

See comments in the example global configuration file that is located in Primetime DRM `<DVD>`\Adobe Primetime DRM Server for Protected Streaming\configs for more details.
