---
title: BEES Overview
description: BEES Overview
copied-description: yes
exl-id: 481af72b-40a3-4f33-9e91-990dc5308596
---
# BEES Overview{#bees-overview}

You can implement a Back-end Entitlement Service (BEES) to provide custom entitlement for your Primetime Cloud DRM operation.

Primetime Cloud DRM uses anonymous license delivery by default. This means that all license requests sent to Primetime Cloud DRM will return a valid license without performing any additional authentication / authorization checks (unless you have applied a policy constraint that calls for using Adobe Primetime authentication).

The license request contains the DRM policy that was employed during the packaging / encryption of the content. The DRM policy is used to generate the DRM license returned to the client. In the default scenario, you must make all DRM policy decisions at content packaging time. Customers that want finer control over these workflows have the following options:

1. Integrate Primetime authentication to add extra entitlement checks prior to playback. 
1. Create an on-premises entitlement service that Primetime Cloud DRM will query before allowing any device to play content that you have packaged.

Your on-premises entitlement service must supply a response to Primetime Cloud DRM that includes the following two pieces of data:

* `isAllowed` 
* `drmPolicyToUse`

These determine if a device is allowed to play the content, and which DRM policy to use to generate the DRM license (if `isAllowed` is true).

This document covers what you need to do to accomplish Option 2 above: Implement your own on-premises external entitlement service and make it available to Primetime Cloud DRM for content that you have packaged.
