---
description: This topic describes performance-related considerations. Any settings in the global configuration file called flashaccess-global.xml affect performance.
title: Global configuration file
exl-id: 52d41476-d352-4c02-8af6-25c0fe6bcaa7
---
# Performance tuning {#performance-tuning}

This topic describes performance-related considerations. Any settings in the global configuration file called flashaccess-global.xml affect performance.

## Global configuration file {#global-configuration-file}

The configuration file includes the following settings elements:

* `<Caching>` The `<Caching>` element controls caching of configuration files in memory. The `<Caching>` element supports the following syntax: 

```
  <Caching refreshDelaySeconds="..." numTenants="..."/>
```

* `refreshDelaySeconds` Controls how often the server checks for updates to the configuration files. A low value for `refreshDelaySeconds` negatively affects performance while a higher value can improve performance.

  See *Updating configuration files* for more information on `refreshDelaySeconds`.

* `numTenants` specifies the number of tenants. A value that is lower than the number of tenants affects performance because requests to the remaining tenants result in cache misses. A cache miss for any configuration data negatively affects performance. Therefore it is recommended that you set this value higher than the number of tenants that are configured for the server unless there are memory limitations that you need to consider.

* `<Logging>` The `<Logging>` element specifies the logging level and the frequency with which log files are rolled. The `<Logging>` element supports the following syntax: 

  ```
  <Logging level="..." rollingFrequency="..."/>
  ```

* `<level>`  `level` specifies messages to a log. A value of `DEBUG` yields many log messages, which can negatively affect performance. It is recommended that you apply a setting of `WARN` for optimal performance. However, this value may result in losing essential runtime information, such as license audits. If you want to save log information with minimal performance impact, you need to apply a value of `INFO`.

* `<rollingFrequency>`  `rollingFrequency` specifies how often log files are *rolled*. *`Rolling`* is a process that designates any new log file as an active log. Therefore the previously active log file is no longer can no longer be modified and is considered *`rolled`*. You can set the rolling interval to `MINUTELY`, `HOURLY`, `TWICE-DAILY`, `DAILY`, `WEEKLY`, `MONTHLY`, or `NEVER`.

See *Using the Adobe Primetime DRM SDK for Protecting Content* for tips on how to optimize performance.
