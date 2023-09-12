---
title: Packaging content
description: Packaging content
copied-description: yes
exl-id: 85950028-d58d-45b3-9337-9fcabe7cc4c0
---
# Packaging content{#packaging-content}

When packaging content, the license server URL must be specified. The Adobe Access Server URL has the format:

```
http(s):// license-server-host:port/flashaccessserver/tenant-name
```

For example, for license server hostname "mylicenseserver.com" listening on port 8080 and a tenant named "tenant1", the license server URL to specify at packaging time is:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

If each tenant uses a different License Server and Transport Credential, be sure to specify the correct tenant's certificate in the packager.

To ensure the server issues licenses only to content packaged by known packagers, include the packager's certificate in the packager allow list of the tenant configuration file.
