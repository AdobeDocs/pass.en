---
title: PTAI 21.11.1 release notes
description: The PTAI release notes describe what is new or changed, the resolved and known issues in Primetime Ad Insertion in the year 2021.
exl-id: 39a05f6d-431a-4416-81b1-21d82c0dbd69

---
# Primetime Ad Insertion 21.11.1 Release Notes

Primetime Ad Insertion 21.xx.x release notes describe what is new or changed, issues resolved and known issues in Primetime Ad Insertion in the year 2021.

## What's new in PTAI 21.11.1

When:  Tuesday, November 9, 2021 from 1:30 AM to 04:30 AM Eastern Time

* [!UICONTROL EXT-X-IMAGE-STREAM-INF] is now configurable per zone.

* Roku Trick Play is fully supported.

## Enhancements and fixes in previous release versions

### Version 21.10.1

When:  Tuesday, October 12, 2021 from 7:45 AM to 1:45 PM Eastern Time

* Consolidated servers, removed non-production and non-useful servers.

### Primetime Ad Insertion Maintenance release

When: Tuesday, September 28, 2021 from 5:00 AM to 6:00 AM Eastern Time

* Updates to Load Balancer stack from AWS's Elastic Load Balancer to AWS's Application Load Balancer for enhanced functionality and scalability. These Load Balancers are used to route ad request traffic to Auditude backend from the Ad Insertion layer (SSAI/CSAI).

### Version 21.9.1

When: Tuesday, September 7, 2021 from 02:30 AM to 05:30 AM Eastern Time

* Updates to infrastructure components behind Primetime Ad Insertion’s mediation and reporting components (Primetime Ads GUI).

### Version 21.8.1

When: Tuesday, August 24, 2021 from 2:00 AM to 05:00 AM Eastern Time

* Added support for DASH Live/ Linear streams (VOD is already supported).

### Version 21.5.1

When:  Wednesday, May 26, 2021 from 3:30 AM to 06:30 AM Eastern Time

**Changes**

* Added support for deprecated segmentation type 0x01 (UPID) for SCTE-based cue formats.

* Added new telemetry for upcoming dashboard changes.

### Version 21.4.1

**When:** Thursday, April 22, 2021 from 2:00 AM to 5:00 AM Eastern Time

**Changes**

* Session request limiting will be enabled to protect against potential DDOS attacks. Sessions will be limited to 10 requests per second, with a ceiling of 100 queued requests. We do not anticipate any impact to players that behave according to HLS/DASH specifications.

* Other maintenance and security enhancements

### Version 21.2.2

**When:** Tuesday, February 23, 2021 from 1:00 AM to 04:00 AM Eastern Time

**Changes**

* Added support for EXT-X-IMAGE-STREAM-INF stream insertion/synchronization in HLS streams. The feature is enabled through a server-side configuration. Contact your technical account representative to enable the feature.

### Version 21.2.1

**When:** Wednesday, February 3, 2021 from 1:00 AM to 04:00 AM Eastern Time

**Changes**

* Added support for DASH output optimization: time-based node consolidation.

### Version 21.1.2

**When:** Tuesday, January 19, 2021 from 12:30 AM to 08:30 AM Eastern Time

**Changes**

* Maintenance update: Upgrade of Primetime Ad Insertion backend memcache clusters.

### Version 21.1.1

**When:** Wednesday, January 13, 2021 from 01:00 AM to 04:00 AM Eastern Time

**Changes**

* Added support for affiliate avails for SCTE35-based cue formats.
