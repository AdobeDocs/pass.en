---
title: Isolation mode MVPDs
description: Learn about isolation mode MVPDs for TV Everywhere programmers
---

# Isolation mode MVPDs for TV Everywhere programmers {#isolation-mode-tve}

>[!IMPORTANT]
>
> Isolation Mode MVPDs limitation is only applicable for TV Everywhere programmers.

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
