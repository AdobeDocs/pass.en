---
title: Limitations
description: Know about limitations and isolation mode MVPD for programmers in Account IQ.
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
---
# General limitations {#general-limitations}

Adobe strives to offer robust functionality and seamless user experiences through its offerings. The current version (version 1.2) of Account IQ provides usage and subscription sharing analytics to streaming providers with high degree of confidence. However, following limitations will be addressed in upcoming release versions:

* When estimating sharing scores for individual accounts, Account IQ takes a conservative approach that enables companies to act on sharing with a great degree of confidence. However, this approach tends to underestimate the total amount of sharing when aggregated across many accounts.

* The [Overall Sharing Score](/help/accountiq/data-panels.md#overall-sharing-score) currently only factors in [Sharing Level](/help/accountiq/data-panels.md#sharing-level) and [Usage from Shared Accounts](/help/accountiq/data-panels.md#usage-from-shared-accounts). Future versions will factor in additional metrics.

* When defining cohorts in the dashboard or usage patterns, the [MVPDs and Programmers in segment](/help/accountiq/data-panels.md#mvpds-programmers-segment), [Sharing score by channels and MVPDs](/help/accountiq/data-panels.md#sharin-score-by-channels-and-mvpds), and [Usage pattern distribution for MVPDs and Programmers](/help/accountiq/usage-patterns.md#usage-pattern-dis-mvpds-programmers) reports have a limit of 20 categories (MVPDs, channels, etc). Segments exceeding this limit will not display data in these reports.

* Currently, the option to export account statistics is restricted to exporting 1000 accounts.

* The option to select [Segment Type](#segment-type) when defining Operations is limited to **Fixed number of accounts**. The **Variable number of accounts** option will be available in a forthcoming version.

* The Benchmarking, Detection Models, Actions, and Settings sections in the left navigation are currently disabled and will be available in a forthcoming version.

* When [creating Operations](/help/accountiq/operations.md#create-new-operation), you can identify only two kinds of [Actions](/help/accountiq/operations.md#action) as of now — Concurrency Monitory rules and External Actions.

* Currently, Operations can only be created and [scheduled](/help/accountiq/operations.md#schedule). Future versions will allow you to pause, resume, and fully manage them.

* Granularity and Time Interval selector is limited to one week or one month, which means data can be evaluated on a single week or a single month only.

## Isolation mode MVPD for programmers {#isolation-mode-prog}

In Isolation Mode, MVPDs (such as, Xfinity) consistently identify subscribers across devices based on the programmers they interact with. In the standard mode, MVPDs consistently identify subscribers across devices irrespective of the programmers.

Here is an example:

![](assets/isolation-diff-new.png)

*Isolation Mode MVPD identifies four different subscribers instead of two*

* If a Subscriber B of an Isolation Mode MVPD (such as, Xfinity) accesses the content offered by two different programmers using the same device, then the MVPD will associate different identifiers with the two different access attempts. It appears that there are two different subscribers accessing the content for the programmers (L and M in the figure).

* For Standard MVPD, if Subscriber B accesses content offered by two different programmers, then the MVPD will associate a single access identifier for both access attempts. 

* MVPDs (such as, Xfinity) in Isolation Mode don't consistently identify a subscriber, even if the subscriber uses the same device across different programmers.

To manage the distortion of data (due to identifying a single subscriber as multiple subscribers based on accessing different programmers), Isolation Mode limits the activity reported about a programmer to the activity only on that programmer's applications. 

*For example, for Isolation Mode in the above image, Programmer L can view data based only on the activity of Identities W and Y, ignoring Identities X and Z*.

>[!IMPORTANT]
>
> The downside is that Programmer L is deprived of sharing information gathered about Subscribers A and B due to activity with any Programmer other than L.

In Isolation mode, all the computations made to obtain the sharing scores and all the associated metrics are made using only the activity of the devices streaming from applications belonging to the selected programmer and channels. The sharing scores and probabilities are calculated only using stream starts from the currently selected channels.

The system automatically operates in Isolation Mode when the selected segment contains an Isolation Mode MVPD which identifies single subscribers as multiple subscribers when streaming from different programmers. All graphs and charts for these segments will reflect the results of this altered behavior.

>[!IMPORTANT]
>
> The behavior in Isolation Mode is incompatible with the standard mode, Isolation Mode MVPD cannot be mixed with other MVPDs and vice versa.

To create a segment that is analyzed in Isolation Mode, drag Isolation Mode MVPD, such as **Xfinity**, to the MVPDs section of the segment definition. 

>[!NOTE]
>
> Since Isolation Mode MVPD cannot be mixed with other MVPDs, the MVPD section of the segment definition will not allow another MVPD to be dragged there.

![](assets/xfinity-in-segment.png)

*Xfinity selection in Isolation mode*

>[!IMPORTANT]
>
> Account sharing is more relevant when measured for streaming across all Programmer's applications. Expect lower **Sharing Scores** and some variation in the metrics when in Isolation Mode.

![](assets/aggregate-sharing-isolation.png)

*Sharing probability gauges in Isolation mode*

The above gauges shows only 9% of all accounts are shared, and among those, only 11% of the content is consumed. Because of the naturally lower scores, the results in Isolation Mode should be interpreted differently from the results in standard mode.

