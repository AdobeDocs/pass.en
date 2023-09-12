---
title: Implement identity-based domain registration
description: Implement identity-based domain registration
copied-description: yes
exl-id: e2f826a8-eea5-4d5f-ac4d-401d7a6c5373
---
# Implement identity-based domain registration{#implement-identity-based-domain-registration}

1. Create a DRM policy with mandatory domain registration.
1. Specify the server's host and port for the domain server URL.

   In your [!DNL .properties] file, set: 

   ```
   policy.domain.url=https://[server:port] 
   ```

1. Make authentication with a username and password mandatory.

   In your [!DNL .properties] file, set: 

   ```
   policy.domain.anonymous=false 
   ```
