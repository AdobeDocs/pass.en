---
title: HSM configuration
description: HSM configuration
copied-description: yes
exl-id: a3e5759e-1419-4519-bcd7-de83364a48f8
---
# HSM configuration {#hsm-configuration}

If you choose to use an HSM to store your server credentials, you must load the private keys and certificates onto the HSM and create a [!DNL pkcs11.cfg] configuration file. This file must be located in the *LicenseServer.ConfigRoot* directory. See the [!DNL Adobe Access Server for Protected Streaming/configs] directory on the Adobe Access DVD for an example PKCS11 configuration file. For information on the format of [!DNL pkcs11.cfg], see the Sun PKCS11 provider documentation.

To verify that your HSM and Sun PKCS11 configuration file is configured properly, you can use the following command from the directory where the [!DNL pkcs11.cfg] file is located ( [!DNL keytool] is installed with the Java JRE and JDK):

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

If you see your credentials in the list, the HSM is configured properly and the license server will be able to access the credentials. 

>[!NOTE]
>
>Adobe Access Serverfor protected Streaming does not currently support HSMs on 64-bit Windows OSes.
