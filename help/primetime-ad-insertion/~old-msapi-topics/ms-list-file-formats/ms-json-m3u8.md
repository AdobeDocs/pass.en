---
description: If pttrackingmode=simple or ptplayer=ios-mobileweb, the manifest server sends back a JSON-formatted file containing Master-M3U8, a URL for the client to use to request the M3U8 file describing the content.
title: JSON format for URL for requesting variant manifest playlist
---

# JSON format for URL for requesting variant manifest playlist {#json-format-for-url-for-requesting-variant-manifest-playlist}

If `pttrackingmode=simple` or `ptplayer=ios-mobileweb`, the manifest server sends back a JSON-formatted file containing Master-M3U8, a URL for the client to use to request the M3U8 file describing the content.

This is the format of the JSON file containing the `Master-M3U8` URL.

```
{
"Master-M3U8": "https://manifest.auditude.com/auditude/variant/{publisherAssetID}/
  {sessionId}/{Base 64 of the url of the content}.m3u8
  ?u={Ad Request Id}
  &z={Ad Zone Id}
  &pttrackingmode=simple
  &pttrackingversion=v1
  &{other query parameters}"
}
```