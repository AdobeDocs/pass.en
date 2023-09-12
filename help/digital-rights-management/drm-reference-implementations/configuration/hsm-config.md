---
description: You can configure the reference implementation with the Sun PKCS#11 provider that supports HSM. Although the use of an HSM is not required, it is recommended.
title: HSM configuration
exl-id: 87a7d242-8202-4749-91a6-e6697be6a61d
---
# HSM configuration{#hsm-configuration}

You can configure the reference implementation with the Sun PKCS#11 provider that supports HSM. Although the use of an HSM is not required, it is recommended.

To use a credential on an HSM, you must create a configuration file for the Sun PKCS#11 provider. For more information, see the [Java PCKS#11 Reference Guide](https://docs.oracle.com/javase/1.5.0/docs/guide/security/p11guide.html).

To verify that your HSM and Sun PKCS#11 configuration file are configured, type the following command by using the keytool that was installed with the Java JDK:

```
keytool -keystore NONE -storetype PKCS11 -providerClass sun.security.pkcs11.SunPKCS11 
  -providerArg pkcs11.cfg -list
```

You have configured the HSM correctly if you can view your credentials in the list.

>[!NOTE]
>
>As of Java 1.7, 64-bit Sun Java for Windows no longer supports the PKCS#11 interfaces that Adobe Primetime DRM requires to communicate with HSM devices. If you plan to use an HSM, ensure that you use a 32-bit version of Java or use a JDK that supports the full PKCS#11 interfaces.
