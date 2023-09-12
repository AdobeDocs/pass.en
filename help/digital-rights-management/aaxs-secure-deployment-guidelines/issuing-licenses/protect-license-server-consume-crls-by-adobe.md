---
title: Consume CRLs published by Adobe
description: Consume CRLs published by Adobe
copied-description: yes
exl-id: b7f68a29-f834-4613-b64d-e610f660e6fc
---
# Consume CRLs published by Adobe{#consume-crls-published-by-adobe}

The SDK periodically downloads CRLs published by Adobe. Do not block access to these files or prevent enforcement of these CRLs.

The SDK has a configuration option to ignore errors when retrieving the Adobe CRLs. This option may only be used in development environments. In production environments, the license server must be able to retrieve the CRLs from Adobe. Failure to obtain a valid CRL is an error.
