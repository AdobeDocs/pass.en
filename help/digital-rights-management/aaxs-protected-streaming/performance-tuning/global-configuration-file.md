---
title: Global Configuration File
description: Global Configuration File
copied-description: yes
exl-id: 109e6e5b-4bb5-43dc-b11e-50799a346a28
---
# Global Configuration File{#global-configuration-file}

The largest impact to performance that you can make is by using settings in the global configuration file, flashaccess-global.xml. These settings include the `<Caching>` and `<Logging>` elements.

* `<Caching>` The `<Caching>` element controls caching of configuration files in memory. The `<Caching>` element has the following syntax: 

  ```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
  ```

    * `refreshDelaySeconds` controls how often the server checks for updates to the configuration files. A low value for `refreshDelaySeconds` negatively impacts performance, while a higher value can improve performance. For more information on `refreshDelaySeconds`, see "[Updating configuration files](../../aaxs-protected-streaming/updating-configuration-files/updating-configuration-files-overview.md)". 
    
    * `numTenants` specifies the number of tenants. A value that is lower than the number of tenants likely impacts performance because requests to the remaining tenants result in cache misses. A cache miss for configuration data negatively impacts performance. Therefore, Adobe recommends that you set this value higher than the number of tenants configured for the server, unless there are memory limitations to consider.

* `<Logging>` The `<Logging>` element specifies the logging level and how frequently log files are rolled. The `<Logging>` element has the following syntax: 

  ```
  <Logging level="..." rollingFrequency=""/>
  ```

    * `level` specifies the messages to log. A value of "DEBUG" yields a lot of log messages, and can negatively impact performance. Adobe recommends a setting of "WARN" for optimal performance. However, that value does risk losing essential runtime information, such as license audits. To preserve valuable log information with minimal performance impact, use a value of "INFO". 
    * `rollingFrequency` specifies how often log files are *rolled*. Rolling is the process where a new log file becomes the active log, while the previously active log file is no longer written to and is considered rolled. The rolling interval can be set to "MINUTELY", "HOURLY", "TWICE-DAILY", "DAILY", "WEEKLY", "MONTHLY", or "NEVER".

See *Using the Adobe Access SDK for Protecting Content* for additional tips on optimizing performance.
