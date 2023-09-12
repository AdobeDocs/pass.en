---
description: When you package content, you must specify the license server URL.
title: Packaging content
exl-id: f82385d5-cdb3-4c24-822e-3fc3c3a0793f
---
# Packaging content{#packaging-content}

When you package content, you must specify the license server URL.

The Adobe Primetime DRM Server URL uses the following format:

```
http(s)://<license-server-host:port>/flashaccessserver/<tenant-name>
```

For example, for license server hostname `mylicenseserver.com` that listens on port 8080, and a tenant called *`tenant1`*, you would use the following syntax for the license server URL that you specify at the time that you package content:

```
https://mylicenseserver.com:8080/flashaccessserver/tenant1
```

If each tenant uses a different License Server and Transport Credential, make sure that you specify the correct tenant's certificate in the packager.

If you want to make sure that the server issues licenses only to content from known packagers, you need to include the packager's certificate in the packager allow list of the tenant configuration file.
