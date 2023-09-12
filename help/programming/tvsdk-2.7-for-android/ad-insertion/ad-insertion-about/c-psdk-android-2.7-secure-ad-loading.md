---
title: Secure Ad loading over HTTPS
description: Secure Ad loading over HTTPS
copied-description: yes
exl-id: f9de1a2b-4eea-4028-83db-1b4021d1fbb7
---
# Secure Ad loading over HTTPS {#secure-ad-loading-over-https}

Adobe Primetime provides an option to request first call to the Primetime ad server and CRS related calls over HTTPS.

The feature is not enabled by default. Use the following to enable secure ad loading.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
