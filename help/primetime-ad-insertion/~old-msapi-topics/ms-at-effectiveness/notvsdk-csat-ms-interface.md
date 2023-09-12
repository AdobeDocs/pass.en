---
description: Use the optional pttrackingmode, pttrackingversion, and pttrackingposition query parameters to obtain URLs to which to send ad tracking information about the current video. The responses vary with the tracking version and whether the video stream is live or on demand (VOD).
title: API for players to interact with the manifest server
---

# API for players to interact with the manifest server {#api-for-players-to-interact-with-the-manifest-server}

Use the optional `pttrackingmode`, `pttrackingversion`, and `pttrackingposition` query parameters to obtain URLs to which to send ad tracking information about the current video. The responses vary with the tracking version and whether the video stream is live or on demand (VOD).

## Query Parameters {#query-parameters}

**pttrackingmode**

Example: `pttrackingmode=simple`
Specifying simple tells the manifest server that you want tracking information.
Specify it on a request to fetch the M3U8 before you request tracking information.When you don't specify it, the manifest server returns tracking information in the #EXT-X-MARKER tags.
Or, if you specify a valid value other than simple, server-side tracking is invoked.

**pttrackingversion**

Example: `pttrackingversion=v2`
This parameter tells the manifest server which format to use to return tracking information (see [File formats](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).
Specify it on a request to fetch the M3U8 before you request tracking information.When you don't specify it, or specify an invalid value, the manifest server uses v1.

**pttrackingposition**

Example: `pttrackingposition`
This parameter tells the manifest server to return tracking information of the video as a JSON or VMAP object in the M3U8 file.The manifest server ignores the specified value and sends all of the tracking information it has for that session. If no value is passed, manifest server returns the requested M3U8 file.
