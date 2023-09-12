---
title: Debugging headers
description: Debugging headers
copied-description: yes
exl-id: 42c19089-2c61-4622-b53a-c28b8d495ef8
---
# Debugging Headers (X-ADBE-AI-X1) {#debugging-headers}

SSAI sends HTTP headers that can be used to gather information and determine performance for production sessions, located in the X-ADBE-AI-X1 header.

Example header:
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

The description for the fields is as follows:

| Name | Description | Example |
|--- |--- |--- |
| isActivePreroll | Whether an ad call for pre-roll was sent | 0 |
| isActiveMidroll | Whether an ad call for midroll-roll was sent | 1 |
| Request ID | Internal SSAI | 1594181097704 |
| Session ID | Session ID of the request | 15126333-5ba9-49b8-a219-4f37e60d259c |
| Stream Type | u=variant, l=live, v=vod | v |
| isBootstrap | Whether this request is a bootstrap call | 0 |
| Ad Break Count | Total number ad breaks in this manifest | 1 |
| Total Ad Break Duration | Total duration of ad break, in seconds | 30 |
| Ad Calls Count | Number of ad calls sent in this request | 2 |
| Redirect Ad Calls Count | Number of redirect ad calls sent in this request | 1 |
| Total Ad Call Duration | Total Ad Call processing time | 199 |
| Inserted Ad Count | Number of ads inserted into the manifest | 2 | 
| Source Manifest Request Time | Time spent fetching content only | 185 |
| Total Request Time | Total time spent fetching content and ads | 497 |
| Ad Manifest Fetch Time (total) | Total amount of time fetching ad manifests | 204 |
| Ad Manifest Fetch Time (actual) | Actual amount of time fetching ad manifests in-parallel | 104 |
| Content Cache Hits | Number of content cache hits | 0 |
| Content Cache Miss | Number of content cache misses | 1 |
| Ad Manifest Cache Hit | Number of ad manifest cache hits | 0 |
| Ad Manifest Cache Miss | Number of ad manifest cache misses | 4 |
