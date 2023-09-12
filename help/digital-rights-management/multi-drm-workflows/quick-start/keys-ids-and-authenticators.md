---
description: To implement DRM you need particular certs and keys, including a content encryption key or CEK to encrypt your content, a customer authenticator for protecting communications with ExpressPlay servers, and CEKSIDs for identifying your content encryption keys as stored in a key management system.
title: Keys, IDs, and Authenticators
exl-id: b769192d-92ad-4b93-84dd-80b182fc6c43
---
# Keys, IDs, and Authenticators{#keys-ids-and-authenticators}

To implement DRM you need particular certs and keys, including a content encryption key or CEK to encrypt your content, a customer authenticator for protecting communications with ExpressPlay servers, and CEKSIDs for identifying your content encryption keys as stored in a key management system.

You need these items to package, license, and play your protected content:

## Content Encryption Key {#section_8D16D36BAE3B4D1F92A0C43567D782D0}

The Content Encryption Key (CEK) is a 16-byte string used for encrypting content.

**What is the CEK?** - The CEK is the key that your packager uses to encrypt your content. It's a 16 byte hex encoded string.

**Where does the CEK come from?** - You (the content provider) create this key yourself, using a tool such as OpenSSL, or Notepad++. For example: 

```
openssl rand 16 -hex > cek_hex_file
```

or (for the Adobe Offline Packager):

1. Generate the 16 byte hex encoded string, as above or using some other tool. It will look something like this: 

   ```
   7debe705d938c76bfd886f077b8fa5f7
   ```

1. Open Notepad++ and paste in the 16 byte hex string. 
1. Convert this value from hex ASCII by Base64-encoding the value to create your [!DNL keyfile.bin]. (This is covered in [](../../multi-drm-workflows/quick-start/package-your-content.md).)

**Same key, different name?** - Yes, you may see the CEK referred to by other names in other places, such as:

* ** [!DNL [somefile].bin]** - The Adobe Offline Packager refers to the CEK as [!DNL [somefile].bin]; e.g., * [!DNL Keyfile.bin]* - This is your CEK as used by the Adobe Offline Packager, in the form of a file on the machine you use for packaging content.

  You "Base64" your random CEK hex string, and save it as a file (e.g., [!DNL keyfile.bin]), usually located in the [!DNL creds] directory beneath [!DNL offlinepkgr/]. In your Packager config file (e.g., you might call it [!DNL widevine.xml] if you're packaging for the Widevine DRM), you refer to your CEK in your config file like this:

  ```
  <config>  
    <in_path>sample.mp4</in_path>  
    <out_type>dash</out_type>
    <b><key_file_path>keyfile.bin</key_file_path></b> // This is your CEK  
    […] 
  </config> 
  ```

* **Content Key** - You also may see the CEK referred to as a Content Key in calls ( `&contentKey=`), in error messages, in support tickets, and in other documentation.

**When / where do I use it?**

1. First, you need to have the CEK available on the machine on which you are doing your packaging. Your packaging tool uses your CEK to encrypt your content. 
1. Second, you need to store the CEK in some form of Key Management System (KMS), with each CEK associated with its own [Content Encryption Key](../../multi-drm-workflows/glossary/glossary-cek.md). You can create your own KMS, or use [ExpressPlay's Key Storage](https://www.expressplay.com/developer/key-storage/). This lets your storefront (your entitlement server, that handles customer entitlement and License Token provision) pull a license token for the customer from the KMS using a Key ID instead of the actual CEK (this is much more secure).

## Content Encryption Key Storage ID {#section_0C94F54970E04BDB82DE3C8A33A62CD4}

The Content Encryption Key Storage ID (CEKSID) uniquely identifies the stored key that decrypts an encrypted piece of video content.

**What is the CEKSID?** - The CEKSID is the unique identifier for a Content Encryption Key (CEK). The CEK is necessary to unlock the protected content; the CEKSID is necessary to access the CEK from where it is stored. When you are testing your setup, you can provide a random CEKSID and CEK at Packaging time, as long as you use the same information for the licensing and playback checks.

**Where does it come from?** - You (the content provider) can create this ID yourself, or you can use a service such as [ExpressPlay's Key Storage](https://www.expressplay.com/developer/key-storage/) to generate CEKSIDs for each of your CEKs (and store both of them). Further, you can use randomly generated CEKSIDs, or employ a scheme that suits your business model. For example, you could use CEKSIDs that are meaningful strings rather than random Hex strings (the ID name could consist of subjects, dates, times, etc.)

**What else is the CEKSID called?** - It is sometimes referred to as a *Content ID*.

## Customer authenticator {#section_F9DDBAA54C544D82A42320CBEEB6CD74}

The customer authenticator is a key you obtain from ExpressPlay when you set up an admin account there. The authenticator is used in communications with ExpressPlay servers.

**What are the customer authenticators?** - The two customer authenticators make up the pair of IDs — one for testing, one for production — that ExpressPlay registers for you hen you sign up with their service. They are always available to you on your ExpressPlay admin page: 
<!--<a id="fig_c5h_xdl_wv"></a>-->

![](assets/expressplay_admin_dashboard-web.png)

**When do I use this?** - You include this in all calls to ExpressPlay servers — for example, license servers, [ExpressPlay Key Storage](https://www.expressplay.com/developer/key-storage/), and other calls.
