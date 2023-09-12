---
description: The Adobe Access Server for Protected Streaming requires two types of configuration files  a global configuration file (flashaccess-global.xml) and a tenant configuration file for each tenant (flashaccess-tenant.xml).
title: Configuration Directory Structure
exl-id: 6561c001-798c-4503-8afb-93580d957372
---
# License server configuration files & Configuration Directory Structure {#configuration-directory-structure}

The Adobe Access Server for Protected Streaming requires two types of configuration files: a global configuration file (flashaccess-global.xml) and a tenant configuration file for each tenant (flashaccess-tenant.xml).

After editing the configuration files, Adobe recommends using the utilities provided with the Adobe Access Server for Protected Streaming to verify that the files are well-formed. For more information, see "[Configuration Validator](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/configuration-validator.md)".

To avoid making passwords available in clear text in the configuration files, all passwords specified in the global and tenant configuration files must be encrypted. For more information on encrypting passwords, see "[Password Scrambler](../../aaxs-protected-streaming/aaxs-protected-streaming-utilities/password-scrambler.md)".

The configuration directories have the following structure:

```
<i class="+ topic ph hi-d="" i "="">
  LicenseServer.ConfigRoot/  
  flashaccess-global.xml  
  pkcs11.cfg (optional)  
  flashaccessserver/  
   libs/ (optional)  
   tenants/  
     
 <i class="+ topic ph hi-d="" i "="">
   tenantname/  
      flashaccess-tenant.xml  
       
  <i class="+ topic ph hi-d="" i "="">
    credential.pfx (optional)  
        
   <i class="+ topic ph hi-d="" i "="">
     packagercert.cer (optional) 
   </i class="+ topic> 
  </i class="+ topic> 
 </i class="+ topic> 
</i class="+ topic>
```
