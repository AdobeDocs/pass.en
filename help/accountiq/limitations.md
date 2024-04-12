---
title: Limitations
description: Know about limitations and isolation mode MVPD for programmers in Account IQ.
exl-id: 08d65716-8b6a-4300-acda-fec63e1e6815
---
# Limitations {#limitations}

## Common limitations across D2C and TV Everywhere

The D2C and TV Everywhere versions of Account IQ provides usage and subscription sharing analytics to streaming providers. However, these versions have certain limitations, which will be addressed in future releases.

* When estimating sharing scores for individual accounts, Account IQ takes a conservative approach that enables companies to act on sharing with a great degree of confidence. However, this approach tends to underestimate the total amount of sharing when aggregated across many accounts.

* The [Overall sharing score](/help/accountiq/data-panels.md#overall-sharing-score) currently includes [Sharing level](/help/accountiq/data-panels.md#sharing-level) and [Usage from shared accounts](/help/accountiq/data-panels.md#usage-from-shared-accounts). Future releases will include more metrics.

* When defining segments on the dashboard or usage patterns, the [Video categories in segment](/help/accountiq/data-panels.md#video-categories-segment), [Sharing score by channels and MVPDs](/help/accountiq/data-panels.md#sharin-score-by-channels-and-mvpds), and [Usage pattern distribution for video categories](/help/accountiq/usage-patterns.md#usage-pattern-dis-video-categories) reports can only display data for upto 20 [video categories](product-concepts.md#video-category-def). Segments containing more than 20 video categories will not show data in these reports.

* Currently, the option to export account statistics is restricted to exporting 1000 accounts.

* When defining Operations, the option to select [segment type](/help/accountiq/operations.md#segment) is limited to **Fixed number of accounts**. The **Variable number of accounts** option will be available in a future releases.

* The **Benchmarking**, **Detection Models**, **Actions**, and **Settings** sections in the left navigation are currently disabled and will be available in a future releases.

* When creating Operations, you can identify only two kinds of [actions](/help/accountiq/operations.md#action) — Concurrency Monitory rules and External Actions.

* Currently, you can only [create](/help/accountiq/operations.md#create-new-operation) and [schedule](/help/accountiq/operations.md#schedule) Operations. Future releases will allow you to pause, resume, and completely manage them.

* You can only analyze data for a single week or month at a time when selecting Granularity and Time Interval. 

## Isolation mode MVPDs for TV Everywhere programmers {#isolation-mode-tve}

In Isolation Mode, MVPDs (such as, Xfinity) consistently identify subscribers across devices based on their interactions with specific programmers. In the standard mode, MVPDs consistently identify subscribers across devices irrespective of the programmers involved.

Here is an example:

![](assets/isolation-diff-new.png)

*Isolation Mode MVPDs identifies four different subscribers instead of two*

* If a Subscriber B of an Isolation Mode MVPD (such as, Xfinity) accesses the content offered by two different programmers using the same device, then the MVPD will associate different identifiers with the two different access attempts. It appears that there are two different subscribers accessing the content for the programmers (L and M in the figure).

* For Standard MVPDs, if Subscriber B accesses content offered by two different programmers, then the MVPD will associate a single access identifier for both access attempts. 

* MVPDs (such as, Xfinity) in Isolation Mode don't consistently identify a subscriber, even if the subscriber uses the same device across different programmers.

To prevent data distortion caused by counting a single subscriber as multiple subscribers due to accessing different programmers, Isolation Mode restricts reported activity about a programmer to only their applications.

For example, Programmer L can view data based only on the activity of Identities W and Y, ignoring Identities X and Z in the previous image.

>[!IMPORTANT]
>
> The downside is that Programmer L is deprived of sharing information gathered about Subscribers A and B due to activity with any Programmer other than L.

In Isolation Mode, sharing scores and associated metrics are calculated solely from the activity of devices streaming from the selected programmer's and channel's applications. The sharing scores and probabilities are calculated from stream starts on the currently selected channels.

The system automatically operates in Isolation Mode when the selected segment contains an Isolation Mode MVPD which identifies single subscribers as multiple subscribers when streaming from different programmers. All graphs and charts for these segments will reflect the results of this altered behavior.

>[!IMPORTANT]
>
> The behavior in Isolation Mode is incompatible with the standard mode, Isolation Mode MVPD cannot be mixed with other MVPDs and vice versa.

To create a segment that is analyzed in Isolation Mode, drag Isolation Mode MVPD, such as **Xfinity**, to the MVPDs section of the segment definition. 

>[!NOTE]
>
> Since Isolation Mode MVPDs cannot be mixed with other MVPDs, the MVPD section of the segment definition will not allow another MVPD to be dragged there.

![](assets/xfinity-in-segment.png)

*Xfinity selection in Isolation Mode*

>[!IMPORTANT]
>
> Account sharing is more relevant when measured for streaming across all Programmer's applications. Expect lower **Sharing Scores** and some variation in the metrics when in Isolation Mode.

![](assets/aggregate-sharing-isolation.png)

*Sharing probability gauges in Isolation Mode*

The above gauges shows only 9% of all accounts are shared, and among those, only 11% of the content is consumed. Because of the naturally lower scores, the results in Isolation Mode should be interpreted differently from the results in standard mode.

