---
title: Packaging content
description: Packaging content
copied-description: yes
exl-id: d408889c-f96d-43d3-af50-62cb5ecc2e28
---
# Packaging content{#packaging-content}

When packaging content for remote key delivery, use a policy that specifies that remote key delivery is required. The Key Server URL must be included in the M3U8 (manifest file) for the HLS content. The Primetime DRM Key Server URL has the format: 

```
https://key-server-host:port/faxsks/tenant-name/key
```

For example, for Key Server host name [!DNL mykeyserver.com] listening on port 443, and a tenant named `tenant1`, the key server URL to specify in the M3U8 is: 

```
https://mykeyserver.com:443/faxsks/tenant1/key
```

The same URL may be used for both iOS and Xbox 360 clients. Or, if the server is configured with separate tenants for each client type, different URLs may be used.

The same content may be played on clients that do not require a key server, as long as the license server URL points to a correctly configured running license server.
