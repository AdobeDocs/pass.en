---
title:  PTAI 19.11.1 release notes
description: PTAI 19.11.1 release notes describe what is new or changed, the resolved and known issues in Primetime Ad Insertion in the year 2019.
exl-id: 0cc9067c-cd46-48f4-afa4-de8b15193723
---
# Primetime Ad Insertion 19.11.1 Release Notes

Primetime Ad Insertion 19.11.1 release notes describe what is new or changed, issues resolved and known issues in Primetime Ad Insertion in the year 2019.

## What's new in PTAI 19.11.1

**When:** Monday, November 4, 2019 at 12:01 AM to 01:00 AM EASTERN

Maintenance updates.

## What changed in previous releases

### Version 19.10.2

**When:** Thursday, October 31, 2019 from 01:00 AM to 03:00 AM Eastern

Maintenance updates.

### Version 19.10.1

**When:**  Tuesday, October 22 at 01:00 AM to 02:00 AM EASTERN

Maintenance updates.

### Version 19.9.1

**When:** Tuesday, September 10, 2019 at 12:30 AM to 2:00 AM Eastern Time

Security updates

### Version 19.8.3

**When:** Wednesday, August 28, 2019, 12:30 am – 01:30 am EASTERN

Fixed a bug in which Chromecast players unexpectedly exited playback when ad segments rolled out of the DVR window.

### Version 19.8.2

**When:** Wednesday, August 21, 2019 2:00 AM to 3:00 AM Eastern Time

* SSAI Dashboard: Session Stats section. You can export the session events via Download CSV option.

* Maintenance updates

### Version 19.8.1

**When:** Tuesday, August 6, 2019 2:30 AM Eastern Time to Tuesday, August 6, 2019 4:30 AM Eastern Time

* SSAI Dashboard: Added new section, Session Stats, to the SSAI Dashboard
  * If you have the Session ID for an SSAI session that had debug mode enabled (ptdebug=true), you will be able to look up the following activity that occurred in that session:
    * Ad requests/responses
    * Inserted ads
    * Fired beacons (server-side tracking only)

  * You can look up activity for a specific Session ID up to 30 days after that SSAI session took place
  * You can export the events
* Database: Security updates

### Version 19.7.1

**When:** Wednesday, July 10

* SSAI: For ptcueformat values that support EXT-X-CUE-OUT ad break signaling in live streams, added a generic macro to pass data from attributes in the EXT-X-ASSET tag Example: Tag that accompanies the #EXT-X-CUE-OUT tag: #EXT-X-ASSET:CAID=75BCD15,GENRE=News,Program=NewsAt10 Macros: # can be used to pass News (from the GENRE attribute) to an ad call URL # can be used to pass NewsAt10 (from the Program attribute) to an ad call URL Exception: For backwards compatibility, # and # have the same functionality. Both macros can be used to pass the value of the CAID attribute, after converting the value from hex to long The long value is 123456789 for the hex value, 75BCD15, in the above example. Both macros would be used to pass 123456789 to an ad call URL The macro always starts with #. The macro is case-sensitive, but the attribute in the EXT-X-ASSET tag is not. That is, PROGRAM and Program are both allowed in the EXT-X-ASSET tag
* SSAI: Configuration changes for a specific customer for the following:
  * Sliding window (live playlist) length of four minutes
  * If a socket timeout exception is thrown when the Manifest Server fetches source content, the Manifest Server will return HTTP response code (404) instead of 500
* Security updates

### Version 19.6.1

**When:** Wednesday, June 12, 2019 11:30 PM PST to Thursday, June 13, 2019 12:30 AM PST

* CRS: Normalization rule for creatives from RevJet
  * Added creative URL normalization rule for RevJet, used by CRS and SSAI
  * TVSDK: If you serve or plan to serve ads from RevJet, normalization rules will need to be added to the CRS Rules JSON in order to use CRS with their creatives. Please speak with your Technical Account Manager for assistance
* CRS: Normalization rule for creatives from Innovid
  * Added creative URL normalization rule for Innovid, used by SSAI
  * The normalization rule used by CRS was added in a prior release
  * TVSDK: The normalization rule to add in the CRS Rules JSON was provided after a prior release, but to be safe, please speak with your Technical Account Manager to review all normalization rules you have in place.
    >[!NOTE]
    >
    >Most Innovid creative URLs will be transcoded and stitched successfully without the normalization rule. Occasionally, however, Innovid creative URLs with dynamic parameters are encountered. The normalization rule is needed to handle these instances.

### Version 19.5.2

**When:** Wednesday, May 22 2:30 AM Eastern Time to Wednesday, May 22 4:30 AM Eastern Time

* Added support for CMAF (HLS/fMP4 content)
  * SSAI: Handle CMAF manifests
  * SSAI: Initiate transcoding requests and retrieve CRS assets depending on the content format (HLS/ts and HLS/fMP4)
  * CRS: Added workflow to repackage ads to CMAF format (HLS/fMP4)
* SSAI: Fixed an issue that prevented unmuxed ads from being inserted into unmuxed content, when both the content and ad don’t have audio-only streams (EXT-X-STREAM-INF)
* SSAI: Added support for Limelight (LLNW) CDN auth tokens for content segments
  * When `pttoken=limelight` or `pttoken=llnw` is added to the bootstrap URL, we will add a secret header when retrieving the source master playlist, then we will append the query parameters from LLNW’s X-Adobe-Sig header to the content segments
* SSAI: Added another pttoken value (`pttoken=centurylink`) for CenturyLink CDN auth token support, which was released July 30, 2018
  * `pttoken=centurylink` has the same behavior as `pttoken=level3`, and both the values are valid

### Version 19.5.1

**When:** Thursday, May 9 2:30 AM Eastern Time to Thursday, May 9 4:30 AM Eastern Time

* SSAI: Security updates
* CRS Dashboard: Truncated the “FqAdId Sample” string to 255 characters due to data storage constraints (8-bit)
  * The “FqAdId Sample” string includes the Ad System and Ad ID from every XML response in the ad’s Wrapper chain for inserts of all CRS ads with SSAI (Creative Stats section of the CRS Dashboard)
* SSAI and CRS Dashboards: Software version updates

### Version 19.4.1

**When:** Wednesday, April 10 2:30 AM Eastern Time to Wednesday, April 10 4:30 AM Eastern Time

* CRS: The CRS Repackaging API will no longer support HTTP POST commands. The CRS Repackaging API will automatically redirect (301) HTTP POST commands to HTTPS
  * Starting May 20, HTTP->HTTPS redirection for HTTP POST commands will be turned off
  * If you use the CRS Repackaging API to repackage ads in advance, please switch your POST commands to HTTPS by May 20
* CRS: Redesigned the architecture and workflow for uploading CRS assets to customers’ CDN origins
  * Job processes per CDN origin are separated, so upload bottlenecks for one CDN origin will not affect uploads to other CDN origins
  * Other benefits: CRS job-processing times and upload rates to customers’ CDN origins are improved
* SSAI: Added ClickThrough and ClickTracking URLs for video ads to the sidecar JSON v2 format
  * A new JSON array property, “videoClicks”, will follow the “trackingURLs” property
  * The “event” value names will be “clickThrough” and “clickTracking”, and they will not have a startTime value
* SSAI: For CRS assets, added functionality to extend a CRS asset’s lookup record expiration by 30 days whenever it is inserted
  * Previous behavior: CRS asset lookup records are stored in memcache in each pod. CRS asset lookup records are automatically removed 30 days after being added to memcache. To repopulate a creative’s CRS asset lookup record in a pod after it has been removed from memcache, that creative needs to be encountered 3 times in that pod
  * New behavior: When a pod accesses a CRS asset lookup record in order to insert the CRS asset, the CRS asset lookup record’s expiration will be extended by 30 days in that pod. As a result, CRS assets that are frequently used will not be removed from a pod’s memcache until 30 days after it was most recently used
  * The new behavior is system wide and can be toggled off if a performance drop is detected
* SSAI: Updated WebVTT manifest-manipulation behavior for live streams only
  * Previous behavior: In the WebVTT manifest only, remove EXT-X-DISCONTINUITY tags that would be inserted before each inserted ad and after the last segment of the inserted ad break
  * New behavior: Added a new parameter, vttdisc, with accepted values of true and false, to the SSAI bootstrap URL
    * vttdisc=true: EXT-X-DISCONTINUITY tags will be inserted in the WebVTT manifest before each inserted ad and after the last segment of the inserted ad break, matching the behavior for audio/video and audio-only manifests
    * vttdisc=false (same as previous behavior): In the WebVTT manifest only, remove EXT-X-DISCONTINUITY tags that would be inserted before each inserted ad and after the last segment of the inserted ad break
    * If the vttdisc parameter is omitted or has a value other than true/false, vttdisc will default to true
* SSAI: Security updates and software version updates
  * Java: Updated Java version to support additional cipher suites for ad calls fired over TLS 1.2 (HTTPS)

### Version 19.2.1

**When:** Wednesday, February 20, 2019 1:30 AM Eastern Time to Wednesday, February 20, 2019 3:30 AM Eastern Time

* SSAI: Added ClickThrough and ClickTracking URLs for video ads to the sidecar JSON v2 format
  * Under the “trackingURLs” property, their “event” value names will be “clickthrough” and “clickTracking”
  * Their startTime values will be the beginning of the ad
* SSAI: For CRS assets, added functionality to extend a CRS asset’s lookup record expiration by 30 days whenever it is inserted
  * Previous behavior: CRS asset lookup records are stored in memcache in each pod. CRS asset lookup records are automatically removed 30 days after being added to memcache. To repopulate a creative’s CRS asset lookup record in a pod after it has been removed from memcache, that creative needs to be encountered 3 times in that pod
  * New behavior: When a pod accesses a CRS asset lookup record in order to insert the CRS asset, the CRS asset lookup record’s expiration will be extended by 30 days in that pod. As a result, CRS assets that are frequently used will not be removed from a pod’s memcache until 30 days after it was most recently used
  * The new behavior is system wide and can be toggled off if a performance drop is detected

* SSAI: Software version updates for NGINX and Kafka
  * NGINX and Kafka are used for firing ad tracking URLs server-side and pushing data to the SSAI and CRS Dashboards
* CRS: Performance improvements to the CRS Dashboard

### Web UI release

**When:** Wednesday, February 13, 4:00 AM – 4:30 AM Pacific

**What:** Primetime ad Decisioning Web UI component

* Fix for the calendar UI issue where user couldn’t select a date beyond 31st Dec 2018 from the calendar component while trafficking a campaign or pulling a report.

### Version 19.1.2

**When:** Wednesday, January 30, 2019 1:30 AM Eastern Time to Wednesday, January 30 3:30 AM Eastern Time

* SSAI: Updated the lookup-key structure that SSAI uses to store and retrieve CRS assets, in order to handle scenarios where ad providers have a dynamic Ad ID or Creative ID for the same ad
  * New lookup-key structure: Zone, Creative URL, and format parameters (target duration, output format, destination CDN)
  * Old lookup-key structure: Zone, Ad System, Ad ID, Creative ID, Creative URL, and format parameters (target duration, output format, destination CDN)
  * The lookup-keys for existing CRS assets will be updated to match the new structure prior to the production release, but please note that new assets transcoded between the lookup-keys update and production release could get missed. If so, they would initiate a new CRS request the next time they are encountered after the release

* CRS: Added the ability to block list/allow list CRS requests from specific ad systems, ad IDs, creative IDs, creative URLs, and/or creative format

  >Note
  >
  >Adobe will add block list rules when ad providers with dynamic values (e.g., dynamic parameter in URL) for the same ad are found. Such block list rules will be disabled after the dynamic component is resolved, either by the provider or through a normalization rule.

  * If you would like to add a block list or allow list rule for your zone, please speak with your Technical Account Manager for assistance.

### Version 19.1.1

**When:** Wednesday, January 9, 2019 1:30 AM Eastern Time to Wednesday, January 9 3:30 AM Eastern Time

* Fixed an issue where misinterpretation of HTTP keep-alive headers can result in an error when validating inbound creative assets hosted on total-stream.net.
* Fixed an issue where single quotation marks (') and double quotation marks (") in Ad ID, Creative ID, and other fields for a repackaging request causes the repackaging request to fail.
* Switched to Java long (data type) to address an issue where reaching the Java int limit of 2,147,483,647 in transcoding job ID values would cause all repackaging requests to fail.
* Database optimizations.

## Resolved issues

Where resolution is associated with a reported issue, a Zendesk reference is displayed. For example ZD#xxxxx.

**PTAI 19.7.1**

ZD#37503 - Json responses for the CRS rules are cached to avoid the duplicate requests.

## Known issues and limitations

**PTAI 19.7.1**

No new limitation added.
