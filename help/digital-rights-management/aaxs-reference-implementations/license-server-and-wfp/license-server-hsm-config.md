---
title: HSM configuration
description: HSM configuration
copied-description: yes
exl-id: 0418bcc1-0a85-4074-9616-915f77507bdd
---
# HSM configuration {#hsm-configuration}

Use of an HSM is not required, but it is recommended. The reference implementation can be configured to use the Sun PKCS11 provider for HSM support. In order to use a credential on an HSM, you must create a configuration file for the Sun PKCS11 provider. See the Sun documentation for details. To verify that your HSM and Sun PKCS11 configuration file are configured properly, you can use the following command (keytool is installed with the Java JDK):

```
    keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
        -providerArg pkcs11.cfg -list
```

If you see your credentials in the list, the HSM is configured properly.

>[!NOTE]
>
>As of Java 1.7, 64-bit Sun Java for Windows does not support the PKCS11 interfaces that Adobe Access DRM requires in order to communicate with HSM devices. If you plan to use an HSM, please use a 32-bit version of Java, or use a JDK that supports the full PKCS11 interfaces.
