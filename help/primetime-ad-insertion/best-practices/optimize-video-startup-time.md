---
title: Optimize video start-up times
description: Optimizing video start-up times
exl-id: 5a89c774-0fed-4378-9cf8-98c4c843ae0d
---
# Optimize video start-up times overview {#optimize-video-start-up-times}

Primetime Ad Insertion provides several features to optimize video start-up time, such as caching and rules for route/protocol optimization. Here are some other recommendations to ensure faster video start-up times when using Primetime Ad Insertion:

* Serve all ads and content from Content Delivery Networks (CDNs)

* Reduce or remove TLS handshakes between Primetime Ad Insertion and the CDNs. For more information, see [Optimize routes and protocols](optimize-routes-protocols.md).

* Serve ad and content fragments from the same CDN

* Insert cache-control headers for live/VOD content and manifests

* Reduce or remove ad providers or ad creatives that are slow to respond
