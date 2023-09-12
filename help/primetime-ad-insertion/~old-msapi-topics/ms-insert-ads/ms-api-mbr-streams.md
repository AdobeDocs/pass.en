---
description: Client requests for ad insertion typically specify more than one bit rate in the variant M3U8-formatted playlist. The manifest server generates and returns a new variant M3U8 file containing a separate M3U8 link for each bit rate. It also generates a unique group ID to tie these M3U8s together.
title: Multiple bit rate streams
---

# Multiple bit rate streams {#multiple-bit-rate-streams}

Client requests for ad insertion typically specify more than one bit rate in the variant M3U8-formatted playlist. The manifest server generates and returns a new variant M3U8 file containing a separate M3U8 link for each bit rate. It also generates a unique group ID to tie these M3U8s together.

The manifest server uses the information in the client's Bootstrap URL request to retrieve the content variant playlist. It generates a new variant playlist containing manifest server links to the stream-level content. The client uses these to construct ad insertion requests. The manifest server's stream-level content links have the following format: 

```
https://manifest.auditude.com/auditude/{live/vod}/{publisherAssetID}/{rendition}/
  {groupID}/{base64-encoded url of the bit rate stream}.[m3u8]?{Query parameters}
```

* **`live/vod`** The manifest server sets this value based on the content's playlist type: Live/linear (#EXT-X-PLAYLIST-TYPE:EVENT) or VOD (#EXT-X-PLAYLIST-TYPE:VOD)

* **`publisherAssetID`** Publisher's unique ID for the specific content provided in the Bootstrap URL request.

* **`rendition`** The manifest server sets this based on the BANDWIDTH value of the content stream, and uses it to match the bit rate of the ad to the bit rate of the content. The ad bit rate cannot exceed the bit rate of the content unless the ad rendition with the lowest bit rate does so.

* **`groupID`** The manifest server generates this value and uses it to ensure that it places ads consistently, no matter for which bit rate renditions the client requests ads.

* **`base64-encoded url of the bit rate stream`** The manifest server URL-safe base64 encodes the content stream's absolute URL. Each stream has its own URL.

* **`Query parameters`** Query parameters provided in the Bootstrap URL request.

