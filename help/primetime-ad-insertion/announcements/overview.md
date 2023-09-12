---
title: Adobe Primetime Ad Insertion Announcements
description: Announcements about recent feature releases and other related news about Primetime Ad Insertion
exl-id: 7d85d3a2-6786-47bd-8d45-ec162aea0ab3
---
# Primetime Ad Insertion Announcements

## Reducing Programmatic Ad Errors via Ad Resolution Timeouts

Published December 1, 2020

Adobe is focused on helping our Primetime Ad Insertion customers maximize the monetization of their ad inventory. We pay particular attention to reducing the complexities of fulfilling programmatic demand, which accounts for over three-quarters of US digital video ad spend according to eMarketer. Programmatic selling enables publishers to maximize demand for their ad inventory, leading to higher fill rates and yield. But it also increases exposure to ad errors like malformed VAST responses, HTTP errors and others that can lead to lost revenue and/or poor viewer experiences. 

One common problem is slow ad responses from programmatic partners. Typically, programmatic ad transactions occur in milliseconds. However, sometimes a single demand source may take an excessive amount of time to respond. A delay from a single provider can impact the entire ad fulfillment process, causing temporary blank screens for the viewer, unfilled ad slots or, in extreme cases, the need to restart a video stream. Unfortunately, identifying and bypassing slow demand sources is a major challenge.

To address this problem, Adobe has added new tools to Primetime Ad Insertion that allow customers to set time constraints for ad resolution. Setting these rules causes slow demand sources to be bypassed automatically, ensuring the video players get ad responses in a timely manner. This allows publishers to greatly limit disruptions from slow demand sources, helping them maximize inventory fill rates and deliver uninterrupted, TV-quality viewing experiences.

To enable ad resolution timeout in Primetime Ad Insertion, modify your bootstrap APIs to include the ptadtimeout parameter (duration in milliseconds).  Any ad requests that do not complete before the timeout duration will not be stitched (any fallback ads will be processed).
