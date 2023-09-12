---
title: Prepare passwords for the Server properties files
description: Prepare passwords for the Server properties files
copied-description: yes
exl-id: b613d43d-17ec-44e9-bd14-81f9bb9a7f62
---
# Prepare passwords for the Server properties files{#prepare-passwords-for-the-server-properties-files}

The reference implementation provides `ScrambleUtil.class`, a class that ensures the security of your credential's password. 

  Use this tool to encrypt the password before you include it in the [!DNL flashaccess-refimpl.properties] file.

   To run the tool, you can use either an Ant script or Java.

The utility generates the encrypted password, which you must copy to the [!DNL flashaccess-refimpl.properties] file. 

>[!NOTE]
>
>Passwords that have been encoded with the `ScrambleUtil.class` that has been provided with the reference implementation do not work with the Primetime DRM Server for Protected Streaming.
