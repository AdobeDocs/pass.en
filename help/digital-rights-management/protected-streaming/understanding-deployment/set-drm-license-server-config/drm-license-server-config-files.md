---
title: License server configuration files
description: License server configuration files
copied-description: yes
exl-id: d48e88a4-caae-4f4e-b870-38da4f3a715e
---
# License server configuration files{#license-server-configuration-files}

The Adobe Primetime DRM Server for Protected Streaming requires the following types of configuration files:

* Global configuration file ( [!DNL flashaccess-global.xml]) 
* Tenant configuration file for each tenant ( [!DNL flashaccess-tenant.xml])

After you complete editing the configuration files, Adobe recommends that you use the utilities provided with the Primetime DRM Server for Protected Streaming to verify that the files are well-formed.

See *Configuration Validator*.

If you want to avoid making passwords available in clear text in the configuration files, then you must encrypt all passwords that you have specified in the global and tenant configuration files by using the Scrambler tool that Adobe has provided.

See *Password Scrambler* for more information on how to encrypt passwords.
