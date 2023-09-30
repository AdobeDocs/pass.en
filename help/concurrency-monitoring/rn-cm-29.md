---
title: Adobe Concurrency Monitoring 2.9 Release Notes
description: Adobe Concurrency Monitoring 2.9 Release Notes
exl-id: fd793b1f-b704-492b-850c-dae6478b575a
---
# Concurrency Monitoring 2.9 Release Notes {#rn-cm29} 

This page describes new features, changes, and known issues with this release.

## Release date {#release-date}

03/14/2019

 
## Release overview {#release-overview}

* Starting with this version we have introduced a new report for understanding concurrent usage: a histogram for concurrency-level, showing:

* the number of users who have reached each concurrency level (i.e. how many users have ever had 2 concurrent streams, 3 concurrent streams, and so on) during each granularity interval
* the total duration for each concurrency level, in minutes (the average value can be computed by simply dividing this value by the above count)
* the total number of times users have encountered each concurrency level, to estimate the impact of a given rule in terms of both impacted users and aggregated user experience
More details are on the [Usage Reports](/help/concurrency-monitoring/cm-usage-reports.md) page. 

We also improved SQL injection protection and added several bug fixes. 

## Known Issues {#known-issues}

None.
