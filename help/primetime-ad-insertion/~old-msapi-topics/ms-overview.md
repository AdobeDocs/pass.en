---
description: The manifest server coordinates the systems that provide content, provide ads, play video, and track ads. It receives M3U8-encoded playlists (manifests) that client video players receive from content providers, stitches ads from ad providers into the manifests, and passes the stitched manifests to video players. It supports both client-side and server-side ad tracking. It conducts its interactions using an HTTP-based web service interface.
title: Overview of Manifest Server interactions
---

# Overview of Manifest Server interactions {#overview-of-manifest-server-interactions}

The manifest server coordinates the systems that provide content, provide ads, play video, and track ads. It receives M3U8-encoded playlists (manifests) that client video players receive from content providers, stitches ads from ad providers into the manifests, and passes the stitched manifests to video players. It supports both client-side and server-side ad tracking. It conducts its interactions using an HTTP-based web service interface.

A typical configuration contains:

* The Primetime manifest server
* The Primetime Creative Repackaging Service (CRS)
* A client, controlling a video player
* A publisher, usually with a Content Management System (CMS)
* A Content Delivery Network (CDN)
* An ad server
* A receiver for ad tracking reports

The workflow varies based on a number of factors, such as if the CDN is Akamai, or if the client is performing ad tracking. For a diagram of the workflow for client-side ad tracking, see [Client-side tracking workflow](/help/primetime-ad-insertion/~old-msapi-topics/ms-at-effectiveness/notvsdk-csat-overview.md#section_cst_flow).

The manifest server interacts with video-delivery clients by receiving and responding to HTTP GET requests. The responses are M3U8-encoded manifests describing ad-stitched content, optionally including a JSON or VMAP structure (sidecar) containing detailed ad-tracking instructions (see [File formats](/help/primetime-ad-insertion/~old-msapi-topics/ms-list-file-formats/ms-api-file-formats.md)).

A typical workflow looks like the following:

1. The publisher sends the content URL and information for the ad server to the client.
1. The client uses the information from the publisher to generate a manifest server URL and sends a GET request to that URL. This is known as the Bootstrap URL.
1. The manifest server establishes a session with the client.
1. The manifest server obtains content manifests from the CDN, which may include ad break information.
1. The manifest server redirects the client to the master/variant manifest it generated for the client.

   >[!NOTE]
   >
   >If the Bootstrap URL query parameters contains the `pttrackingmode=simple` or `ptplayer=ios-mobileweb` setting, the manifest server returns the master/variant manifest URL in a JSON object, and the client sends a GET request to that variant manifest URL.

1. The client chooses a stream in the generated variant manifest to play, sending ad information to the manifest server. 
1. The manifest server passes the client-supplied information to the ad server and receives ads and ad-tracking URLs from the ad server. If a supplied ad is not in HLS format, the manifest server sends it to CRS for conversion to HLS. 
1. The manifest server stitches ads into the content manifest and sends the new stitched manifest to the client. 
1. The client plays the content with the stitched-in ads and makes requests at the specified times to the specified tracking URLs.

Primetime ad insertion supports clients on many video-delivery platforms. Not all clients are built on the Primetime TVSDK package, but all clients send GET requests to the same basic URL. Query parameters distinguish one client request from another by telling the manifest server:

* which client is making the request, 
* what that client wants, 
* and what ad-tracking information to provide.

## CORS {#section_BEA7F298660944BE92801E4C82FCD038}

The manifest server uses the Cross-Origin Resource Sharing standard (CORS). It looks for an `Origin` header in the requests it receives. If the header is present, it replies with

* `Access-Control-Allow-Origin: *`string from the Origin header`*` 
* `Access-Control-Allow-Credentials: true` 
* `Access-Control-Allow-Methods: GET`

If not, it replies with:

* `Access-Control-Allow-Origin: *` 
* `Access-Control-Allow-Methods: GET`