---
title: Limitations
description: Know about limitations and isolation mode MVPD for programmers in Account IQ.
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
---
# Limitations {#limitations}

The D2C and TV Everywhere versions of Account IQ provides usage and subscription sharing analytics to streaming providers. However, the current 1.3 version have certain limitations, which will be addressed in future releases.

* The [Overall sharing score](/help/accountiq/data-panels.md#overall-sharing-score) currently includes [Sharing level](/help/accountiq/data-panels.md#sharing-level) and [Usage from shared accounts](/help/accountiq/data-panels.md#usage-from-shared-accounts). Future releases will include more metrics.

* When defining segments on the dashboard or usage patterns, the [Video categories in segment](/help/accountiq/data-panels.md#video-categories-segment), [Sharing score by channels and MVPDs](/help/accountiq/data-panels.md#sharin-score-by-channels-and-mvpds), and [Usage pattern distribution for video categories](/help/accountiq/usage-patterns.md#usage-pattern-dis-video-categories) reports can only display data for upto 20 [video categories](product-concepts.md#video-category-def). Segments containing more than 20 video categories will not show data in these reports.

* Currently, the option to export account statistics is restricted to exporting 1000 accounts.

* When defining Operations, the option to select [segment type](/help/accountiq/operations.md#segment) is limited to **Fixed number of accounts**. The **Variable number of accounts** option will be available in a future releases.

* The **Benchmarking**, **Detection Models**, **Actions**, and **Settings** sections in the left navigation are currently disabled and will be available in a future release.

* When creating Operations, you can apply only two kinds of [actions](/help/accountiq/operations.md#action) — Concurrency Monitory rules and External Actions.

* Currently, you can only [create](/help/accountiq/operations.md#create-new-operation) and [schedule](/help/accountiq/operations.md#schedule) Operations. Future releases will allow you to pause, resume, and completely manage them.

* You can only analyze data for a single week or month at a time when selecting Granularity and Time Interval. 

* You can't add Isolation Mode MVPDs to the segment definition with any other MVPDs. Some MVPDs don't uniquely identify subscribers across multiple programmer channels. Therefore, those MVPDs are treated separately for TV Everywhere programmers.



