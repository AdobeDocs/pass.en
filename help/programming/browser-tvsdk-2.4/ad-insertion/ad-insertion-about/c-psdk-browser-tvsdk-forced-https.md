---
title: Secure Ad Loading over HTTPS
description: Secure Ad Loading over HTTPS
copied-description: yes
exl-id: d43418e9-631b-4344-a5b3-0a6154a325d4
---
# Secure Ad Loading over HTTPS{#secure-ad-loading-over-https}

Adobe Primetime can request third-party ad servers over https even if the player is hosted on http. Only those ad-servers calls are upgraded to https that the client seeks during the Auditude Ad resolver phase.

>[!NOTE]
>
>This feature is not supported for Flash.

Use the following to enable secure ad loading. It is not enabled by default. 

```
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.forceHttpsConfiguration.adServerCalls = true;
```
