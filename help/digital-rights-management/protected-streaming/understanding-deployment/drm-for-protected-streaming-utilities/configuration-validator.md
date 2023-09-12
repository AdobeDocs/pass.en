---
description: Adobe recommends that if you make changes in the configuration file, you should run the Configuration Validator utility before you start the server. This utility can detect most configuration errors early, before they cause failures during request processing.
title: Configuration validator
exl-id: 41d0a926-4e12-442c-886e-5f12cf10eed8
---
# Configuration validator{#configuration-validator}

Adobe recommends that if you make changes in the configuration file, you should run the Configuration Validator utility before you start the server. This utility can detect most configuration errors early, before they cause failures during request processing.

To run the validator, type:

```
Validator.bat  
<i class="+ topic ph hi-d="" i "="">
  options  
</i class="+ topic>
```

or

```
java -jar libs/flashaccess-validator.jar  
<i class="+ topic ph hi-d="" i "="">
  options 
</i class="+ topic>
```

For each of the license server configuration files, the Validator can perform file-based validation, which ensures that the XML file is well-formed and conforms to the configuration file schema.

To perform file-based validation on the global configuration file, type:

```
Validator --<file path>/flashaccess-global.xml --global
```

To perform file-based validation on the tenant configuration file, type:

```
Validator --<file path>/flashaccess-tenant.xml --tenant
```

The Validator can also perform deployment-based validation. In addition to checking conformity with the schema, this level of validation also verifies that the values that you specified are valid. For example, it ensures that referenced files exist.

Deployment-based validation can be performed at the following levels:

* `Tenant` — Validates configuration file and credentials for a specific tenant. If you want to validate the configuration for `<tenant1>`, type: 

  ```
      Validator --<root-path-to-LicenseServer.ConfigRoot> -d flashaccessserver/tenant1 -t
  ```

* `Global` — Validates the global configuration file and tenant validation for all tenants. If you want to perform global deployment-based validation, type: 

  ```
      Validator --<root-path-to-LicenseServer.ConfigRoot> -g
  ```
