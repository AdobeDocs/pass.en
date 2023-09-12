---
title: Use Ad Insertion in Live/Linear stream
description: Using Ad Insertion in Live/Linear stream
exl-id: d56ed723-ec72-4bbd-befc-6858c7c9d800
---
# Use Ad Insertion in Live/Linear stream {#ad-insertion-live-linear-stream}

Primetime Ad Insertion gives publishers the ability to handle standard and complex ad insertion situations that occur during live/linear streams.

## Supported Cue Formats {#cue-formats-supported}

Primetime Ad Insertion supports a wide range of standard and non-standard cue formats, including:

* DPI SCTE-35 (SCTE-35 enhanced ad markers)

* [Adobe Digital Program Insertion Signaling Specification](assets/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* Binary SCTE-35 (both HLS and DASH)

* Textual SCTE-35 (both HLS and DASH)

Contact your Primetime support representative for additional details or other supported cue formats.

## Partial Ad Break support {#partial-ad-break-support}

Partial ad breaks can be used in situations where a viewer enters a live/linear stream after an ad break has started.  For instance, if a viewer enters a 2:00 long ad break at the 1:00 mark, partial ad break insertion ensures that ads will be served in the remaining time. Without partial ad break insertion, no ads would be served to this viewer during the break. Primetime Ad Insertion enables partial ad break insertion by default if the appropriate tags are present in the media stream(s).

## Early Return (Early Ad Exit) {#early-return-early-ad-exit}

There are instances where it may be necessary to return early from an ad break in a live/linear stream, such as when a sporting event suddenly returns to action. Each ad decisioning format contains a tag to "cue-out" (ads) or "cue-in" (content.)  If a "cue-in" tag is encountered prior to the end of an ad break, Adobe Primetime Ad Insertion will honor the cue-in.  Please contact your content packager to enable early return.
