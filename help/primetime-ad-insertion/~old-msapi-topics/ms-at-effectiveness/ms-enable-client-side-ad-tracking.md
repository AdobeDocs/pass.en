---
description: You can enable client-side ad tracking by adding the pttrackingmode and pttrackingversion parameters to your Bootstrap URL request.
title: Enable client-side ad tracking
---

# Enable client-side ad tracking {#enable-client-side-ad-tracking}

You can enable client-side ad tracking by adding the `pttrackingmode` and `pttrackingversion` parameters to your Bootstrap URL request.

 With client-side ad tracking enabled, you can also retrieve ad tracking metadata using the Tracking API URL. For more details, see [Query Parameters](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-ms-interface.md).

To perform client-side ad tracking, use the Tracking API URL.

1. Add the following query parameters to the manifest server request URL:

   * `pttrackingmode=simple`
   * `pttrackingversion={format version}`

For example:

```URL
https://. . .?. . .&pttrackingmode=simple&pttrackingversion=v1
```
