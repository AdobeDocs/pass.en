---
title: Secure Ad loading over HTTPS
description: Secure Ad loading over HTTPS
copied-description: yes
exl-id: 752d9a35-2faa-4953-8357-e2aff445d3c7
---
# Secure Ad loading over HTTPS {#secure-ad-loading-over-https}

Adobe Primetime provides an option to request first call to the Primetime ad server and CRS related calls over HTTPS.

The feature is not enabled by default. Use the following to enable secure ad loading.

```
AuditudeSettings auditudeSettings = new AuditudeSettings(); 
auditudeSettings. getForceHttpsConfiguration().setAdServerCalls(true);
```
