---
title: Xbox Live XSTS token validation
description: Xbox Live XSTS token validation
copied-description: yes
---

# Xbox Live XSTS token validation{#xbox-live-xsts-token-validation}

For XSTS requests, the `customerSpecificAuthToken` field will contain the Base64 encoded XSTS token. The sample `XSTSValidator` code examines the Base64 decoded token for the existence of the `EncryptedAssertion` element; however, you can use other methods to distinguish between these requests and non-Xbox requests. For example, you could use a different URL.

The policy returned in the response message will override the original policy in the DRM metadata supplied with the Xbox key request. Only a subset of policy features are supported by the Xbox client, and these fields are the only ones that will override the original policy.

There are additional setup steps needed to support token decryption and validation. You must load the [!DNL xsts_partner_cert.pfx] and [!DNL x_secure_token_service.part.xboxlive.com.cer] credentials into a JKS format keystore, which you then provide to your back-end entitlement server as the system property `xsts-keystore`. By default, the partner [!DNL .pfx] has the alias `xsts`, and the token validation cert has the alias `xsts-verify-cert`. You can also override these using system properties. Finally, there is a system property `xsts-keystore-password` that has no default, and which contains the keystore password. The system properties read by the `XSTSValidator` code are summarized below:

|  System Property  | Default Value  | Comment  |
|---|---|---|
|  `xsts-keystore`  | `xsts.jks`  | JKS format keystore used by the validator.  |
|  `xsts-keystore-password`  | | Password for the keystore  |
|  `xsts-alias`  | `xsts`  | Alias used to retrieve the decryption key from the keystore  |
|  `xsts-verify-cert-alias`  | `xsts-verify-cert`  | Alias used to retrieve the validation cert from the keystore  |

