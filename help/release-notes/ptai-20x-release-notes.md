---
title:  PTAI 20.12.1 release notes
description: The PTAI release notes describe what is new or changed, the resolved and known issues in Primetime Ad Insertion in the year 2020.
exl-id: 47e36e42-b6a0-408c-93da-f63c929396b5
---
# Primetime Ad Insertion 20.12.1 Release Notes

Primetime Ad Insertion 20.12.1 release notes describe what is new or changed, issues resolved and known issues in Primetime Ad Insertion in the year 2020.

## What's new in PTAI 20.12.1

**When:** Tuesday, December 08, 2020 from 01:00 AM to 04:00 AM Eastern Time

**Changes**

* Includes hotfix to address intermittent client connectivity (5xx) issues in Primetime Ad Insertion encountered on Nov 30, 2020.

## Enhancements and fixes in previous release versions

### Version 20.11.1

**When:** Thursday, November 5, 2020 from 2:00 AM to 05:00 AM Eastern Time

**Changes**

* Maintenance updates.

### Version 20.10.2

**When:** Thursday, Oct 29, 2020 from 12:01 AM to 06:00 AM Eastern Time

**Changes**

* Maintenance updates.

### Version 20.10.1

**When:** Tuesday, October 13, 2020 from 03:00 AM to 07:00 AM Eastern Time

**Changes**

* Maintenance updates.

### Version 20.9.3

**When:** Wednesday, September 30, 2020 at 3:30 AM to 6:30 AM Eastern Time

**Changes**

* Added Bootstrap API parameter `ptparallelstream`. This allows customers with players that request CMAF demuxed audio or video streams in parallel to ensure that ads in audio and video tracks are consistent. Set the parameter value to true to enable this feature or omit to disable.

### Version 20.9.2

**When:** Tuesday, September 15, 2020 from 3:30 AM to 6:30 AM Eastern Time

**Enhancements**

* Provided support for the inclusion of non-linear ad types using `EXT-X-MARKER` tags.
For more information or to enable this feature, contact your technical support representative.

* Provided support for limiting overall ad resolution time, if providers take too long to respond. To enable limiting, set the bootstrap API parameter `ptadtimeout` to a value in milliseconds.

  >[!NOTE]
  >
  >This timeout applies only to ad requests, not to ad creative requests.

### Version 20.9.1

**When:** Tuesday, September 1, 2020 from 3:30 AM to 7:30 AM Eastern Time

**Changes**

* Fixed the issue for customers using HLS/CMAF, where EXT-X-MAP was sometimes missing CDN tokens or EXT-X-MAP tags sometimes incorrectly rolled out of the DVR window.

### Version 20.8.4

**When:** Wednesday, August 19, 2020 from 03:30 AM to 07:30 AM Eastern Time

**Enhancements and fixes**

Maintenance updates.

### Version 20.8.1

**When:** Tuesday, August 4, 2020 from 3:00 AM to 6:00 AM Eastern Time

**Enhancements and fixes**

Maintenance updates.

### Version 20.7.1

**When:** Thursday, July 9, 2020 from 03:00 AM to 05:00 AM Eastern Time

**New Features and enhancements**

* SCTE35 enhancement to use either of Provider Ad Start/End messages or Break Start/End messages to identify the cue.

* Updated X-ADBE-AI-X1 header with additional information to help troubleshooting.

* Enhanced metrics aggregation.

* Enhanced SSAI Console Dashboard for Session Stats panel

### Version 20.6.2

**When:** Thursday, June 18, 2020 from 03:00 AM to 04:00 AM Eastern Time

**Enhancements**

Improved stream synchronization for video clients requiring millisecond precision. Contact Adobe Support to enable millisecond precision for `#EXT-X-PROGRAM-DATE-TIME tags`.

### Version 20.6.1

**When:** Tuesday, June 2, 2020 from 03:00 AM to 05:00 AM Eastern Time

**New Features**

Contact Adobe Support to enable the following new features via server-side configuration:

* Manifest Manipulation: HLS segment and resource URLs can now be transformed between HTTP and HTTPS to increase performance by reducing TLS handshakes on back-end requests. It can also be used to unify ad/content fragments onto the same CDNs.

* Long Form VOD: Improved APIs to maintain session keep-alive with long form VOD assets.

**Bug fixes**

* Fixed an issue where WebVTT fragments were always requested under http protocol regardless of the original protocol requested.

* Fixed an issue where EXT-X-DISCONTINUITY tags were removed from the top of the playlist when switching from ads back to content. Contact Adobe Support to enable this fix.

### Version 20.5.1

**When:** Tuesday, May 5, 2020 from 04:00 AM to 05:00 AM Eastern Time

* Fixed an issue to ensure that correct CORS headers are provided when If-Modified-Since headers are sent.

* Bug fixes on the CRS dashboard.

* Maintenance updates.

### Version 20.3.4

**When:** Wednesday, April 1, 2020 from 03:00 AM to 04:00 AM Eastern Time

* Fixed an issue that caused subtitles to go out of sync after ad insertion in VOD/ WebVTT.

* Security updates.

### Version 20.3.3

**When:** Thursday, March 26, 2020 from 03:00 AM to 04:00 AM Eastern Time

* SSAI 4XX and 5XX responses now correctly supply CORS-related headers, allowing cross-domain javascript webview clients to successfully read error responses.

* Fixed an issue with X-Forwarded-For headers, where IPv6 addresses were not correctly URL encoded when passed to the ad servers.

* Fixed an issue with CMAF/demuxed audio streams, where in certain scenarios EXT-X-MEDIA-SEQUENCE numbers would increment incorrectly.

### Version 20.3.2

**When:** Wednesday, March 11, 2020 from 05:30 AM to 07:00 AM Eastern Time

* Improvements to SCTE35 signal handling.

* Maintenance updates.

### Version 20.3.1

**When:** Thursday, March 05, 2020 from 02:30 AM to 04:30 AM Eastern Time

* Performance improvements:

  * Added cache support for both master/media m3u8 manifests. These manifests now respond to Cache-Control: public and Max-Age headers, which can often improve video start performance.
  
  * Added support for forcing https creatives to be fetched over http, which can also improve video start performance.
  
* Security and maintenance fixes.

### Version 20.2.1

**When:** Thursday, February 13, 2020 from 04:30 AM to 05:30 AM Eastern Time

* Added support for stitching ad assets that contain multiple audio-only streams based on language/codec/bitrate.
* Minor performance enhancements and maintenance updates.

### Version 20.1.3

**When:** Tuesday, January 28, 2020 from 2:00 AM to 03:00 AM Eastern Time

* **VMAP with FER support for nbc CueFormat**

  Convert cues from FER stream into FW timeline override params, when `ptcueformat=nbc` is used and the stream is a VOD stream with in-manifest cues and baked-in ads.

* Sanitize user-agent field in HTTP Header before forwarding to third-party Ad providers/ CDN.

* Filter out control/non-printable characters (ASCII code < 32) from user-agent HTTP headers before sending to Auditude and other ad-providers, CDNs. Auditude Ad-Call used to fail for such invalid headers.

* Purge old V1 Objects from NetStorage Groups to keep object count within safe limits of Akamai.

### Version 20.1.2 (Hotfix)

**When:** Monday, January 20, 2020 from 02:00 AM to 03:00 AM Eastern Time

* Maintenance updates.

### Version 20.1.1

**When:** Wednesday, January 15, 2020 from 04:00 AM to 05:00 AM Eastern Time

* The Creative Repackaging Service now delivers quicker ad insertion by automatically block listing malformed creatives.

* Added phase 1 support for new SCTE 35 cue format in server-side ad insertion.

* Maintenance upgrades.

## Resolved issues {#Resolved-issues}

Where resolution is associated with a reported issue, a Zendesk reference is displayed. For example, `ZD#xxxxx`.

**PTAI 20.9.1**

* Fixed the issue for customers using HLS/CMAF, where EXT-X-MAP was sometimes missing CDN tokens or EXT-X-MAP tags sometimes incorrectly rolled out of the DVR window.

**PTAI 20.6.1**

* `WebVTT` fragments were always requested under http protocol regardless of the original protocol requested.

* `EXT-X-DISCONTINUITY` tags are removed from the top of the playlist when switching from ads back to content. Contact Adobe Support to enable this fix.

**PTAI 20.5.1**

* Issues with CORS headers when If-Modified-Since headers are sent.

* Issues in CRS dashboard.

**PTAI 20.3.4**

* Issue that caused subtitles to go out of sync after ad insertion in VOD/ WebVTT.

**PTAI 20.3.3**

* Issue with X-Forwarded-For headers, where IPv6 addresses were not correctly URL encoded when passed to the ad servers.

* Issue with CMAF/demuxed audio streams, where in certain scenarios EXT-X-MEDIA-SEQUENCE numbers increment incorrectly in certain scenarios

## Known issues and limitations

**PTAI 20.10.1**

No new limitation added.
