---
description: If you select an HSM to store your server credentials, you must load the private keys and certificates onto the HSM and create a pkcs11.cfg configuration file.
title: HSM configuration
exl-id: 4c4423ea-b7af-4a30-99ac-f5b74a1e1168
---
# HSM configuration{#hsm-configuration}

If you select an HSM to store your server credentials, you must load the private keys and certificates onto the HSM and create a pkcs11.cfg configuration file.

You must locate the configuration file in the *LicenseServer.ConfigRoot* directory.

See the [!DNL Adobe Primetime DRM Server for Protected Streaming/configs] directory on the Adobe Primetime DRM DVD for an example PKCS11 configuration file.

See the Sun PKCS11 provider documentation regarding the format of [!DNL pkcs11.cfg] file.

You can use the following command from the directory where the [!DNL pkcs11.cfg] file is located ( [!DNL keytool] is installed with the Java JRE and JDK) to verify that the HSM and Sun PKCS11 configuration file has been correctly configured:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

If you can view your credentials in the list, then the HSM is correctly configured and the license server can now access the credentials.
