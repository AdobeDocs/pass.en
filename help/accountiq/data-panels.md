---
title: Data panels on Dashboard
description: The Dashboard helps to pinpoint the instances of password sharing by analyzing a wide array of subscriber data.
exl-id: 616da2a5-c9fe-40ea-90cf-f565bc13e764
---
# Data panels on Dashboard {data-panels}

Once you've selected segment, granularity and time interval, the dashboard displays the following tables and graphs for credential sharing statistics of the subscriber accounts in the selected segment:

* [Average sharing score - aggregated for the current segment](#aggregated-sharing)
* [MVPDs and Programmers in segment](#mvpds-programmers-segment) 
* [Sharing score by channels and MVPDs](#sharin-score-by-channels-and-mvpds)
* [Accounts sharing probability](#accounts-sharing-probability) 
* [Number of accounts and usage by sharing probability level](#number-of-accounts-usage-sharing-probability)

The Average sharing score - aggregated for the current segment is available for both Programmer and MVPD users.

## Average sharing score - aggregated for the current segment {#aggregated-sharing}

The Aggregated Sharing Score panel provides a top line readout summarizing the quantity and impact of sharing in terms of accounts and streaming volume.

The values help you understand the magnitude of credential sharing by your subscribers, hence providing a measure of the need to act upon it.

![](assets/aggregate-sharing-score.png)


*Figure: Average sharing score panel - aggregated for the current segment*

The following three metrics are components of the Average Sharing Score.

### Sharing level {#sharing-level}

The sharing level gauge shows the percentage of all your subscriber accounts (in the defined segment) that are shared, during the selected time interval.  

A value calculated based on an average of the sharing probability computed for every account in the set of selected MVPDs that has streamed from a one of the selected programmer channels during the selected time interval.

![](assets/sharing-level.png)


*Figure: Sharing level*

The Trend indicator shows the percentage change in the value of the metric in from the previous time interval.

### Usage from shared accounts {#usage-from-shared-accounts}

This gauge indicates what percent of the usage of all the subscriber accounts is from the shared accounts for the defined segment and time period. The gauge marks the ranges of usage (from shared accounts) on the scale of 0 to 100%. These ranges—named Low, Medium, High, and Abnormal—are based on the industry average.

You can also see the Trend indicator, which depicts a rise or fall in the usage from shared accounts as compared to the previous time interval.

![](assets/usage-4mshared-accounts.png)


*Figure: Usage from shared accounts*

### Overall sharing score {#overall-sharing-score}

Overall sharing score is composite of sharing scores including "Sharing level" and "z Usage from shared accounts".

It provides a value meant to reflect the relative impact of sharing when compared to the industry. It's purpose is similar to that of a credit score, summarizing the situation with a single number. But in this case, the higher the number the greater the potential harm.

![](assets/overall-sharing-score.png)


*Figure: Overall sharing score*

## MVPDs and Programmers in segment {#mvpds-programmers-segment}

+++Programmer- MVPDs in segment

When you log in as a Programmer user, this table provides a comparative view of the different Aggregated Sharing Scores for the MVPDs in the current segment.

Select the column headings to view the data in ascending and descending order.

![](assets/sharing-scores-by-mvpds-in-segment.png)

*Figure: Sharing Score by MVPDs in segment*

+++

+++MVPD- Programmers in segment

When you log in as a MVPD user, this table provides a comparative view of the different Aggregated Sharing Scores for the Programmers in the current segment.

Select the column headings to view the data in ascending and descending order.

![](assets/sharing-scores-by-programmers-in-segment.png)

*Figure: Sharing Score by Programmers in segment*

+++

<br/>

Sharing score by channels and MVPDs is only available for Programmers and doesn't exist for MVPD users. 

## Sharing score by channels and MVPDs  {#sharin-score-by-channels-and-mvpds}

When you log in as a Programmer user, this table provides a comparative view of sharing scores of the selected channels for the MVPDs in the current segment.

Select the column headings to view the data in ascending and descending order.

![](assets/sharing-scores-by-channels-mvpds.png)


*Figure: Sharing scores by channels and MVPDs*

The Accounts sharing probability is available for both Programmer and MVPD users.

## Accounts sharing probability {#accounts-sharing-probability}

This chart partitions accounts into ranges of sharing probability quintiles from very low (0-20%) to very high (80=100%).

>[!NOTE]
>
>The bar graph uses a logarithmic scale.


![](assets/dashboard-ac-sharing-prob.png)


*Figure: Numbers and percentages of subscriber accounts in different sharing probability ranges*

<br/>

The Number of accounts and usage by sharing probability level is available for both Programmer and MVPD users.

## Number of accounts and usage by sharing probability level {#number-of-accounts-usage-sharing-probability}

This panel provides tabular view of  accounts partitioned into ranges of sharing probability quintiles from very low (0-20%) to very high (80-100%) with each quintile's associated usage from shared accounts.

![](assets/no-acc-usage-prob-level.png)


*Figure: Number of accounts, trends, and usages falling in various probability ranges*

