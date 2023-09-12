---
description: Use the HTTP GET command to interact with the manifest server.
title: Send a command to the Manifest Server
---

# Send a command to the Manifest Server {#send-a-command-to-the-manifest-server}

Use the HTTP GET command to interact with the manifest server.

1. Send an `HTTP GET` request for a bootstrap URL constructed using the following pattern:

   ```
   https://{manifest-server:port}/auditude/variant/
    {PublisherAssetID}/{Content URL (base64)}.m3u8
    ?{query parameters}
   ```

* **PublisherAssetID** Required. Publisher's unique ID for the specific content.

* **Content URL** Required. URL of the content M3U8 file, Base64 encoded to be safe within the manifest server URL. The content URL must point to a variant M3U8 file, even if there is only one bit rate stream.

* **Query parameters** Some are required, some optional. These constitute the most varied part of the request. They tell the manifest server which sort of client is making the request and what it wants the manifest server to do.

   For example:

   ```
   https://manifest.auditude.com/auditude/variant/
    {publisherAssetID}/{Content URL (base64)}.m3u8?
   u={Asset ID}&z={zone}&_sid_=0&pttrackingmode=simple
   &pttrackingversion=v2&live=false
   ```

   **HTTP vs. HTTPS requests**

   The manifest server creates URLs using the same HTTP protocol of the client's request. If a player makes a non-secure HTTP (http) request, the manifest server returns manifest URLs and Auditude tracking URLs with the http protocol. If a player makes a secure HTTP (https) connection, manifest server, it returns manifest URLs and Auditude tracking URLs with the https protocol. 

   >[!NOTE]
   >
   >The manifest server cannot change the protocol (HTTP or HTTPS) of content segments (.ts) and 3rd-party tracking beacons. You must contact the content and 3rd-party ad providers to have them configure the desired protocols.