---
title: Set the XSTS token in your player
description: Set the XSTS token in your player
copied-description: yes
exl-id: 1b83baac-e6a6-4e84-8ea5-07bd7e4afd9d
---
# Streaming to Xbox360 (Optional) {#streaming-to-xboc360} 

Primetime DRM is available on the Xbox360 platform. However, only the Protected Streaming use case is supported, not the full suite of DRM policy rights. Non-streaming DRM policy rights, such as Device Domain Groups, are not supported. The Xbox360 ignores unsupported rights when attempting to play content.

The supported Primetime DRM Policy rights for the Xbox are:
* Digital Output Protection
* License Offline Caching End Date
* License Start Date
* License End Date
* Playback Window Duration (seconds)

Content may not have to be repackaged to stream to Xbox360, if it was already packaged for another Primetime platform, such as iOS, Android, or Desktop.

One caveat with Xbox360 is that it must always reach out to a key server every time an EXT-X-KEY tag is encountered in the M3U8. Unlike iOS, where a DRM Policy setting (policy.requireKeyServer) will cause the iOS Primetime video player to retrieve the AES decryption key from localhost, Xbox will always attempt to retrieve the decryption key from a remote keyserver . There is no DRM policy right to instruct the Xbox app to retrieve the AES decryption
key from localhost. Because of this requirement, EXT-X-KEY entries must be in the M3U8 pointing to the Primetime Cloud DRM endpoint. This URL is set via <key_url> in the OfflinePackager.jar configuration file config_hls.xml.

If you wish to package content once and have it stream to all  Primetime targets, as well as configure iOS devices to not retrieve a key from a remote keyserver, you can package the content using a DRM policy that has the property policy.requireKeyServer=false (such as in policy_ios_localkeyserver.pol). iOS devices will retrieve the AES key locally, while Xbox devices will ignore this property and reach out to the Primetime Cloud DRM key server
for a decryption key.

>!Note
>
>All Xbox360 requests must utilize Custom Authentication/>Entitlement.This is because on the Xbox360 platform, Xbox Live >utilizes an Xbox Secure Token Server (XSTS) token for >athentication purposes.
>The Primetime Cloud DRM license server uses the XSTS token to >validate the integrity of both the Xbox device and the user making >the license request. However, validating the XSTS token requires a >customer’s private Xbox Live vendor key, which Primetime Cloud DRM >does not store. Because of this, when Primetime Cloud DRM receives >a license request from an Xbox 360 client, Primetime Cloud DRM >will forward the XSTS token to the Primetime customer’s Back-End >Authentication/Entitlement server. The Primetime customer's server
>will then parse and validate the XSTS token to ensure it was >signed using the customer's application publisher key.
>To pass an XSTS token from the Xbox360 client, set the token >synchronously in response to the MediaPlayer.RequestKeyAttribute >event – described in further detail here: **Set the XSTS token in your player.** A sample Back-End Authentication/Entitlement server >is included with the software release in the Custom Authentication >and Entitlement directory.Validation of XSTS tokens is discussed >in further detail here: **Xbox Live XSTS token validation.**


## Set the XSTS token in your player {#set-the-xsts-token-in-your-player}

In Xbox360, you set the token asynchronously in response to the `MediaPlayer.RequestKeyAttribute` event. 

Set the XSTS token.

   The sample app bundled with your software shows how to set the XSTS token in your player. Here is the relevant code snippet from the sample player: 

   ```
      MediaPlayer mMediaPlayer;  
    
   mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
    
   private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
       string token = "";  
       // XBOX XSTS Token...  
       KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
       mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
   } 
   
   ```

## Xbox Live XSTS token validation {#xbox-live-xsts-token-validation}

For XSTS requests, the `customerSpecificAuthToken` field will contain the Base64 encoded XSTS token. The sample `XSTSValidator` code examines the Base64 decoded token for the existence of the `EncryptedAssertion` element; however, you can use other methods to distinguish between these requests and non-Xbox requests. For example, you could use a different URL.

The policy returned in the response message will override the original policy in the DRM metadata supplied with the Xbox key request. Only a subset of policy features are supported by the Xbox client, and these fields are the only ones that will override the original policy.

There are additional setup steps needed to support token decryption and validation. You must load the [!DNL xsts_partner_cert.pfx] and [!DNL x_secure_token_service.part.xboxlive.com.cer] credentials into a JKS format keystore, which you then provide to your back-end entitlement server as the system property `xsts-keystore`. By default, the partner [!DNL .pfx] has the alias `xsts`, and the token validation cert has the alias `xsts-verify-cert`. You can also override these using system properties. Finally, there is a system property `xsts-keystore-password` that has no default, and which contains the keystore password. The system properties read by the `XSTSValidator` code are summarized below:

|  System Property  | Default Value  | Comment  |
|---|---|---|
|  xsts-keystore  | xsts.jks  | JKS format keystore used by the validator.  |
|  xsts-keystore-password  | | Password for the keystore  |
|  xsts-alias  | xsts  | Alias used to retrieve the decryption key from the keystore  |
|  xsts-verify-cert-alias  | xsts-verify-cert  | Alias used to retrieve the validation cert from the keystore  |

## Create JKS for an XSTS validator{#create-jks-for-an-xsts-validator}

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
