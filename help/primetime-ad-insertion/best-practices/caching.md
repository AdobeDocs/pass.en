---
title: Caching
description: Caching
copied-description: yes
exl-id: c12c2345-db55-468a-b4b5-5a9e1364a46d
---
# HTTP Caching {#caching}

Primetime Ad Insertion by default respects HTTP cache control headers when fetching ad creatives as well as content.  This can drastically reduce the amount of network requests required for Primetime Ad Insertion to make to the CDN across all clients.  For caching, Adobe recommends the following settings and involve sending the HTTP header `max-age` from your CDN.  Contact your CDN representative to enable these headers on your video streams and ad streams.

## For Live/Linear content {#caching-live-linear-content}

* Master manifest: 24 hours, or Cache-Control: max-age=86400
* Media manifest: 1 second, or Cache-Control: max-age=1

## For VOD content {#caching-vod-content}

* Master manifest: 24 hours, or Cache-Control: max-age=86400
* Media manifest: 24 hours, or Cache-Control: max-age=86400
