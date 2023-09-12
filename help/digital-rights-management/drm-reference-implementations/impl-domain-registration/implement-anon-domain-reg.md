---
title: Implement anonymous domain registration
description: Implement anonymous domain registration
copied-description: yes
exl-id: 304cfe6f-0917-42ef-a49a-e6c4bc9c10d0
---
# Implement anonymous domain registration{#implement-anonymous-domain-registration}

1. Create a DRM policy that specifies that domain registration is required.
1. Specify the domain server URL as:

   ```
   https://[host:port]/flashaccess/domainserver/domainname/
   ```

1. Make anonymous authentication mandatory.

   In your [!DNL .properties] file, set: 

   ```
   policy.domain.anonymous=true 
   ```
