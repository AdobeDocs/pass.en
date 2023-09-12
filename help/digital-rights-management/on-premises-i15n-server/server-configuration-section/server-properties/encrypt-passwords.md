---
title: Encrypt Passwords
description: Encrypt Passwords
copied-description: yes
exl-id: 97b78e00-e5e3-4a9d-8eab-fcf96d3b1219
---
# Encrypt Passwords{#encrypt-passwords}

The properties files include several password values that you should not enter as plain text. Encrypt these values using the following command: 

`java -jar adobe-flashaccess-i15n-setup.jar password`

This command will output an encrypted password, which you then use in the properties files.

>[!NOTE]
>This is not the utility used for encrypting License Server passwords.
