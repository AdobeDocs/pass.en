---
title: Shared Accounts reports
description: Shared accounts reports
exl-id: 16c5ded1-2a95-4373-8b90-b445131f333a
---
# Shared Accounts Reports {#shared-accounts-reports}

The Shared Accounts Reports break down the metrics such as number of devices and device types by the selected range of sharing probability, for example **[!UICONTROL Over Moderate Probability]** and **[!UICONTROL Over Low Probability]** for the current segment.

These ranges can then serve as user defined thresholds and the graphs are updated based on the selected thresholds.

Account IQ classifies all the subscriber accounts of the defined segment into the accounts with the following five categories based on their sharing probabilities:

* Very high (80%-100%)
* High (60%-80%)
* Moderate (40%-60%)
* Low (20%-40%)
* Very low (0%-20%)

## Accounts Sharing Probability {#accounts-sharing-probability}

The donut chart here categorizes and shows the percentages (and absolute numbers) of the subscriber accounts from various probability categories.

The red line marks the threshold range selected by users in [Accounts over threshold in current segment](#threshold-selector) panel.

![](assets/accounts-sharing-probability-pie.png)

The bar chart plots number of accounts on y-axis for various categories of sharing probabilities (plotted on x-axis).

![](assets/accounts-sharing-probability-bar.png)

The red line marks the range of threshold, and can be adjusted in the bar chart. The threshold adjusted in the bar chart reflects in the threshold range in donut chart.

<!--![](assets/shared-accounts-rep.gif)-->

### Accounts over threshold in current segment{#threshold-selector}

This panel lets you select a range from the following as threshold for subscriber accounts (based on their haring probabilities):

* Accounts **over very low** sharing **probability**

* Accounts **over low** sharing **probability**

* Accounts **over moderate** sharing **probability**

* Accounts **over high** sharing **probability**

![](assets/threshold-selector-shared-accounts.png)

Once you select the threshold, the panel shows the percentage (and number) of accounts out of all the subscriber accounts in the selected segment.

## Segment - Play requests out of total {#play-request-out-total}

The donut chart shows the percentage (and number) of play requests made by subscribers in the segment; and lets you compare the play requests made by subscribers not in the defined segment.

![](assets/play-req-outof-total.png)

When you move cursor on the donut chart, it also shows subscriber percentages and numbers from various probability ranges.

<!--![](assets/play-request-total.gif)-->

## Segment-Average Number of Devices Per Account{#avg-devices-account}

The bar chart shows average number of devices of each device type in use by subscribers in the current segment and subscribers not in current segment.

![](assets/avg-devices-per-acc.png)

## Segment - Zip codes per Period per Account {#zip-codes-period-account}

This graph informs you about the number of subscribers that are consuming content from different locations in a time frame.

![](assets/zip-period-account.png)

You can zoom in to narrow down and view specifics of a bar in the graph that plots a range of locations.

<!--![](assets/zip-code-period.gif)-->

## Segment - Geographical Span / Period / Account {#geo-span-period-account}

This bar graph plots number of subscriber accounts with respect to different ranges of geographical ranges in miles. The range is based on the maximum distance between the locations from which a subscriber has streamed during the time frame.

<!--Total number of users ...

How many accounts are within 99 miles of each other.....and how many are apart. 

Based on points on the map.-->

![](assets/geogr-span-account.png)

When you select a bar representing a range of geographical distance, it expands the range to show you more details.

<!--![](assets/geo-span-period-acc.gif)-->
