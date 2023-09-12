---
description: You can specify or override timelines for ad breaks in VOD content using a formatted list of ad and content segments called pods.
title: VOD timeline format
---

# VOD timeline format {#vod-timeline-format}

You can specify or override timelines for ad breaks in VOD content using a formatted list of ad and content segments called pods.

## Pods {#section_606E9456E25E41C8B8537A023DDD96CE}

A pod is an ad break or a content segment. A timeline consists of a sequence of pods, separated by semicolons. The following types of pods exist:

### Ad break

  ```
  B,duration,maximum_number_of_ads,position
  ```

  Duration is in seconds, with precision of .001 (milliseconds); number of ads is an integer. Position is one of the following: 
    * **n** None — no ad
    * **p** Pre-roll — before the content
    * **m** Mid-roll — within the content
    * **t** Post-roll — after the content

  For example, `B,60,2,p` represents a one-minute break for up to 2 ads before the content.

### Content segment - chapter

  ```
  C,duration,number_of_lots
  ```

  Duration is in seconds, with precision of .001 (milliseconds); number of lots (sections of content) is an integer. For example, `C,300,1` represents a single five-minute section of content.