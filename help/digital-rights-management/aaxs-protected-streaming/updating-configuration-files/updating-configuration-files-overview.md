---
title: Updating configuration files overview
description: Updating configuration files overview
copied-description: yes
exl-id: 51c8a0af-9445-4c9e-93bc-af0af0096705
---
# Updating configuration files overview {#updating-configuration-files-overview}

Once the license server reads one of the license server configuration files (global or tenant configuration), the configuration information is cached in memory. Therefore, the files do not have to be read from disk for every license request. However, the server also allows most values in the configuration files to be modified without requiring a server restart for the changes to take effect. (See below for details on which configuration values are checked for updates.)

In order to reload the configuration when changes are made, the license server stores the time the file was last modified. At a configurable interval, the server checks if the file modification time has changed, and if so, reloads the contents of the file.

To control how often the server checks for updates, set the `refreshDelaySeconds` attribute in the Caching element of the global configuration file. For example, if `refreshDelaySeconds` is set to 3600 seconds, it takes at most one hour from the time the file is updated for any configuration updates to be detected by the server. If `refreshDelaySeconds` is set to 0, the server checks for configuration updates on every request. Setting `refreshDelaySeconds` to a low value is not recommended for production environments, as it could impact performance.

The Caching element also controls how many tenants' configurations are cached at once. You can set this value to a number smaller than the total number of tenants to limit the amount of memory used to cache the configuration information. If a request is received for a tenant not in the cache, the configuration is loaded before the request can be processed. If the cache is full, the least recently used tenant is removed from the cache.

If a change is saved to a configuration file or to any of the certificate files referenced within [!DNL flashaccess-tenant.xml] while the server is attempting to read the file, or if the file's timestamp is found to be less than one second before the current time or is in the future, the cached version of the configuration is used until the next time the server checks for updates. If there is no cached version, the loading of the configuration fails, and an error is returned to the client. The server attempts to load the file again the next time it receives a request for that tenant.
