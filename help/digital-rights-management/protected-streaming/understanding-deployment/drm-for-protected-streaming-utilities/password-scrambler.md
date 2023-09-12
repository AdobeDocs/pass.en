---
description: The Password Scrambler utility encrypts a password for the Adobe Primetime DRM Server for Protected Streaming configuration files.
title: Password scrambler
exl-id: 9cedd3e5-01db-4ea9-bf23-8767987fc26c
---
# Password scrambler {#password-scrambler}

The Password Scrambler utility encrypts a password for the Adobe Primetime DRM Server for Protected Streaming configuration files.

To run the scrambler, type:

```
Scrambler.bat  
<i class="+ topic ph hi-d="" i "="">
  password 
</i class="+ topic>
```

or

```
java -jar libs/flashaccess-scrambler.jar  
<i class="+ topic ph hi-d="" i "="">
  password  
</i class="+ topic>
```

The utility displays the following message:

```
Encrypted password:  
<i class="+ topic ph hi-d="" i "="">
  scrambled-password 
</i class="+ topic>
```

All passwords that you have specified in the [!DNL flashaccess-global.xml] and [!DNL flashaccess-tenant.xml] files must be encrypted.

>[!NOTE]
>
>The Password Scrambler utility in the Primetime DRM Server for Protected Streaming is not interchangeable with the scrambler that is provided with the Reference Implementation License Server.
