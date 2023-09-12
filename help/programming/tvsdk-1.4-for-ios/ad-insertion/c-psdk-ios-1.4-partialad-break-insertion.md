---
description: TVSDK provides a TV-like experience of being able to join in the middle of an ad, in live streams.
title: Partial ad-break insertion
exl-id: ae260f1a-8c4a-44b9-8f74-285f93d999e4
---
# Partial ad-break insertion{#partial-ad-break-insertion}

TVSDK provides a TV-like experience of being able to join in the middle of an ad, in live streams.

The partial ad-break insertion feature allows you to mimic a TV-like experience where, if the client starts a live stream inside a mid-roll, it starts playing within that mid-roll. It is similar to switching to a TV channel and the commercials run seamlessly.

For example, If a user joins in the middle of a 90 seconds ad break (three 30 seconds ads), 10 seconds into the second ad (that is, at 40 seconds into the ad break), the second ad is played for the remaining duration (20 seconds) followed by the third ad.

## Track Ad {#section_03AFAEAA8DA44399952DC51C5E12951E}

Ad trackers for the partially played ad (the second ad) are not triggered. In the example above, only the tracker for the third ad is triggered.

## Behavior with pre-roll {#section_7DFBFB12E63343D1A0C614F0CF9F1714}

The feature works when a pre-roll ad is played with live content. The stream plays from the live point after pre-roll ad ends.

Ad break events is sent even if there are no complete ads in this ad break. An ad is considered partial ad, if is skipped for more than one second. For example, if a viewer watches an ad that they skipped for 800 ms, it is considered as a complete ad.
