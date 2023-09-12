---
description: As soon as the license server reads one of the license server configuration files (global or tenant configuration), the configuration information is cached in memory. Therefore the files do not have to be read from disk for every license request. However, the server also allows most values in the configuration files to be modified without requiring a server restart for the changes to take effect.
title: Updating configuration files
---

# Updating configuration files{#updating-configuration-files}

As soon as the license server reads one of the license server configuration files (global or tenant configuration), the configuration information is cached in memory. Therefore the files do not have to be read from disk for every license request. However, the server also allows most values in the configuration files to be modified without requiring a server restart for the changes to take effect.

Whenever you modify the configuration file, the license server stores the time that the file was last modified. At a configurable interval, the server checks if the file modification time has changed. If it has changed, the server automatically reloads the contents of the configuration file.

If you want to control how often the server checks for updates, you need to to set the `refreshDelaySeconds` attribute in the `Caching` element of the global configuration file. For example, if `refreshDelaySeconds` is set to 3600 seconds, the server will update the configuration within at most one hour from the modification time of the configuration file. If `refreshDelaySeconds` is set to 0, the server checks for configuration updates at every request. It is not recommended that you set `refreshDelaySeconds` to a low value in any production environments because doing this can affect performance.

The `Caching` element also controls how many tenants' configurations are cached at once. You can set this value to a number that is smaller than the total number of tenants to limit the amount of memory being used to cache the configuration information. If a request is received for a tenant that is not in the cache, the configuration is loaded before the request can be processed. If the cache is full, the least recently used tenant is removed from the cache.

The cached version of the configuration continues to be used in the following situations (up until the next time the server checks for updates):

* If a change is saved to a configuration file or to any of the certificate files referenced in the [!DNL flashaccess-tenant.xml] file while the server attempts to read the file 
* If the file's timestamp is found to be less than one second before the current time 
* If the file's timestamp is in the future

If there is no cached version, loading of the configuration fails, and an error is returned to the client. The server then attempts to load the file again the next time it receives a request for that tenant.

## Updating the global configuration file {#section_AA546C72442646CFB8906AEEBDF50587}

You can modify the HSM password in [!DNL flashaccess-global.xml] at any time. The changes take effect the next time that the server reloads the configuration file. However, changes to the Logging and Caching elements are not reloaded. You need to restart the server before any changes for these elements become effective.

## Updating the tenant configuration file {#section_71624DB8DF28480F84F34F0FF7FD4365}

You can modify all values that are specified in the [!DNL flashaccess-tenant.xml] file at any time. The changes take effect the next time that the server reloads the configuration file. Also, the server checks for any modifications in all credential ( [!DNL .pfx]) files and packager allow list certificate files that are referenced in the tenant configuration file. 
