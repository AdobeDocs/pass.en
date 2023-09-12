---
description: All requests for ad insertion use the same URL structure and the same basic query parameters. Additional query parameters enable the manifest server to work with a variety of clients and situations.
title: Requests for ad insertion
---

# Requests for ad insertion {#requests-for-ad-insertion}

All requests for ad insertion use the same URL structure and the same basic query parameters. Additional query parameters enable the manifest server to work with a variety of clients and situations.

|Parameter|Description|
|--- |--- |
|u|The asset ID is an MD5 hash of the  ad_request_id from the Adobe Primetime ad decisioning metadata. Provided by your Adobe Technical Account Manager.|
|z|The zone id for the asset that needs to be provided to Auditude. Provided by your Adobe Technical Account Manager.|
|`__sid__`|A unique id that the manifest server will use to generate the session id.|

>[!NOTE]
>
>The `__sid__` parameter is surrounded by double underscore characters.

The manifest server maintains sessions for individual clients or groups of clients to ensure that the sequences of API interactions for different clients stay separate. The `__sid__` that the client sends in the bootstrap URL to the manifest server should be unique within its environment. The manifest server uses it to construct a globally unique ID, which it returns to the client.

The remaining query parameters pertain to different clients and situations.