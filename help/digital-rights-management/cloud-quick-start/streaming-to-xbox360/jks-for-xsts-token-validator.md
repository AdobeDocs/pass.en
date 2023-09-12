---
title: Create JKS for an XSTS validator
description: Create JKS for an XSTS validator
copied-description: yes
---

# Create JKS for an XSTS validator{#create-jks-for-an-xsts-validator}

1. Find out the private cert's alias name, located in the partner [!DNL .pfx] file.

   ```
   keytool -list -storetype pkcs12 -keystore xsts_partner_cert.pfx -v 
   ```

1. Convert [!DNL .pfx] to [!DNL .jks].

   ```
   keytool -importkeystore -srckeystore xsts_partner_cert.pfx -srcstoretype PKCS12 \  
           -keystore xsts.jks -srcalias  
   <alias> -destalias xsts
   ```

   (where `<alias>` is the private cert's alias name that you discovered in Step 1.)
1. Import [!DNL x_secure_token_service.part.xboxlive.com.cer].

   ```
   keytool -importcert -alias xsts-verify-cert -keystore xsts.jks \  
           -file x_secure_token_service.part.xboxlive.com.cer 
   ```

1. Put [!DNL xsts.jks] in your Tomcat home directory, and define `-Dxsts-keystore-password=****` for Tomcat.

If [!DNL xsts_partner_cert.pfx] and [!DNL xsts.jks] are using different passwords, update the `xsts` password in `jks` to make them the same. 

```
keytool -keypasswd -keystore xsts.jks -alias xsts 
```
