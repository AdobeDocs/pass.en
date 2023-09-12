---
title: Secure Ad loading over HTTPS
description: Secure Ad loading over HTTPS
copied-description: yes
exl-id: e12cb9d4-05d4-485e-b629-1af680b83e04
---
# Secure Ad loading over HTTPS{#secure-ad-loading-over-https}

Adobe Primetime provides an option to request first call to the Primetime ad server and CRS related calls over HTTPS.

The feature is not enabled by default. Use the following to enable secure ad loading.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
