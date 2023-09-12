---
description: While the default creative repackaging service (CRS) scenario is to use one Content Delivery Network (CDN), you can deploy CRS assets on more than one CDN.
title: Multiple CDN support for CRS ad delivery
---

# Multiple CDN support for CRS ad delivery {#multiple-cdn-support-for-crs-ad-delivery}

While the default creative repackaging service (CRS) scenario is to use one Content Delivery Network (CDN), you can deploy CRS assets on more than one CDN.

## Requirements

You can use multiple CDNs for the following reasons:

* A requirement to scale up for large viewing events
* A requirement to match the CDN source of the CRS asset with the CDN source of the main content.
* A requirement to use a different CDN from the CRS default CDN (Akamai).

When the manifest server makes a look-up for transcoded requests, it uses a bootstrap URL that contains a number of query parameters. If you have set up a multi-CDN environment, the bootstrap URL will also need to contain the `ptcdn` parameter. The manifest server uses this parameter to identify the CDN server from which to get the transcoded version of the ad.

For more details, see [Multi CDN Support](../../~old-creative-repackaging-service/multi-cdn-supportt.md) in the CRS documentation. 
