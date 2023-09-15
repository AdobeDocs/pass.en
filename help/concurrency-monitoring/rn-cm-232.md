---
title: Adobe Pass Concurrency Monitoring 2.3.2 Release Notes
description: Adobe Pass Concurrency Monitoring 2.3.2 Release Notes
---

# Adobe Pass Concurrency Monitoring 2.3.2 Release Notes {#cm-232} 

This page describes new features, changes, and known issues with this release:

Release Date: 12/11/2015

## New Features & Improvements {#new-features}

* New breakdowns available in the Usage Reports. The new breakdowns are available if the application integrated with Concurrency Monitoring sends custom metadata.
    * application - the application ID reported in the call URL
    * mvpd - the MVPD reported in the call URL
    * channel - the custom metadata channel
    * platform - the custom metadata applicationPlatform
* New metrics related to **stream duration** available in the Usage Reports. The new metrics can be used to create a histogram of stream duration. The following intervals in minutes are currently available:
    * duration_0-15
    * duration_15-30
    * duration_30-60
    * duration_60-120
    * duration_over-120
 
## Bug Fixes {#bug-fixes}

N/A 

## Known Issues {#known-issues}

N/A
