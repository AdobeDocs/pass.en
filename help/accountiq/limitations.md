---
title: Limitations and known issues
description: Known issues in the product.
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
---
# Known issues and limitations {#known-issues}

Adobe strives to offer robust functionality and seamless user experiences through its offerings. The current version (version 1.2) of Account IQ provides usage and subscription sharing analytics to streaming providers with high degree of confidence. However, following limitations will be addressed in upcoming release versions.

* When estimating sharing scores for individual accounts, Account IQ takes a conservative approach that enables companies to act on sharing with great degree of confidence. However, this approach tends to underestimate the total amount of sharing when aggregated across many accounts.

* The [Overall Sharing Score](/help/accountiq/data-panels.md#overall-sharing-score) currently only factors in [Sharing Level](/help/accountiq/data-panels.md#sharing-level) and [Usage from Shared Accounts](/help/accountiq/data-panels.md#usage-from-shared-accounts). Future versions will factor in additional metrics.

* When defining cohorts in the dashboard or usage patterns, the [MVPDs and Programmers in segment](/help/accountiq/data-panels.md#mvpds-programmers-segment), [Sharing score by channels and MVPDs](/help/accountiq/data-panels.md#sharin-score-by-channels-and-mvpds), and [Usage pattern distribution for MVPDs and Programmers](/help/accountiq/usage-patterns.md#usage-pattern-dis-mvpds-programmers) reports have a limit of 20 categories (MVPDs, channels, etc). Segments exceeding this limit will not display data in these reports.

* The option to export account statistics is limited to export 1000 accounts, as of now.

* The option to select [Segment Type](#segment-type) when defining Operations is limited to **Fixed number of accounts**. The **Variable number of accounts** option will be available in a forthcoming version.

* The Benchmarking, Detection Models, Actions, and Settings sections in the left navigation are currently disabled and will be available in a forthcoming version.

* When [creating Operations](/help/accountiq/operations.md#create-new-operation), you can identify only two kinds of [Actions](/help/accountiq/operations.md#action) as of now — Concurrency Monitory rules and External Actions.

* Currently, Operations can only be created and [scheduled](/help/accountiq/operations.md#schedule). Future versions will allow you to pause, resume, and fully manage them.

* Because of the more limited set of data used, Isolation mode does not truly reflect the amount of sharing. Therefore, MVPD in Isolation mode cannot be compared to any other MVPD. <!--do we need to separate out this limitation, which is from a different persona i.e. only for Programmer persona?-->

* Granularity and Time Interval selector is limited to one week or one month, which means data can be evaluated on a single week or a single month only.

