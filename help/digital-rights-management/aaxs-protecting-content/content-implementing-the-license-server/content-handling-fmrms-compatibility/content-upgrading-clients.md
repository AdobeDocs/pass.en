---
title: Upgrading clients
description: Upgrading clients
copied-description: yes
exl-id: 0476c9ef-3622-4bc5-bb24-f8543470b7d3
---
# Upgrading clients{#upgrading-clients}

If an FMRMS 1.x client contacts a Adobe Access server, the server needs to prompt the client to upgrade.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.compatibility.FMRMSv1RequestHandler`. 
* The request URL is "*Base URL from 1.x content*" + "/edcws/services/urn:EDCLicenseService"

  Unlike other Adobe Access request handlers, this handler does not provide access to any request information or require any response data to be set. Create an instance of the `FMRMSv1RequestHandler`, and then call `close()`
