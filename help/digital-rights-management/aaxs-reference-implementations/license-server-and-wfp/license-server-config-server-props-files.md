---
title: Server properties files
description: Server properties files
copied-description: yes
exl-id: c42fde8f-e438-4497-bd15-ebd0f6e2eed7
---
# Server properties files {#server-properties-files}

The server requires two configuration files, one for the license server and one for the packager. Both files must be placed on the classpath. The properties files contain the location of the credentials issued by Adobe. These credentials can be specified as a .pfx file and password or by providing an alias and password for a credential stored on an HSM.

Please refer to the property files for details about the specific values and usage of the each parameter. Sample properties files can be found in the "resources" directory of the reference implementation (Reference Implementation\Server\resources).

To ensure the security of your credential's password, a tool is provided (ScrambleUtil.class) to encrypt the password before it is entered into the flashaccess-refimpl.properties or flashaccess-refimpl-packager.properties file.

To properly prepare your credential's password:

1. Go to [!DNL Reference Implementation\Server\refimpl\scrambler]. 
1. From the command prompt, enter the command: 

   ```
   java -classpath  
   <i class="+ topic ph hi-d="" i "="">
   path_to_adobe-flashaccess-sdk.jar.; 
        com.adobe.flashaccess.refimpl.util.ScrambleUtil " 
   <i class="+ topic ph hi-d="" i "="">
   your_pfx_password" 
   </i class="+ topic> 
   </i class="+ topic>
   ```

>[!NOTE]
>
>The previous example uses a semicolon (;) as the delimiter. For platforms other than Microsoft Windows, use a colon (:) as the delimiter.

The utility outputs the encrypted password, which you must copy to the [!DNL .properties] file.
