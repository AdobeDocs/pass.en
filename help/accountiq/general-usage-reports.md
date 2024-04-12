---
title: General usage reports
description: Learn about general usage reports
exl-id: 1272073a-61fe-47ec-aced-2e8055b6b11e
---
# [!UICONTROL General usage] reports {#general-usage-reports}

[!UICONTROL Account IQ] reports are basic analytic tools that let you drill into your data to isolate [cohorts](/help/accountiq/product-concepts.md#segmet-def), identify anomalies, and build an understanding of your account characteristics.

[!UICONTROL General usage] reports page provides tools to carve out subgroup metrics based on the number of account devices in use, IPs detected, and their respective zip codes.

The reports are all based on the current segment selected from the [Segments and time interval](/help/accountiq/segments-timeinterval.md) panel. You can fine tune your selection and further narrow it down by specifying (number of devices, number of IPs, and number of zip codes) thresholds in the [Snapshot Overview-Accounts above thresholds](#snapshot-overview) panel.

## Play requests and unique subscribers {#playreq-uniquesubs}

The line graphs here gives you a view of the changes over time of values, such as Play Requests and Unique Subscribers in a selected time interval for the defined segment.

+++ D2C services: Play Requests/Unique Subscribers

![](assets/d2c-line-graph-gu.png)


*Play Requests/Unique Subscribers for D2C services*

+++

+++Programmers: Play Requests/Unique Subscribers

![](assets/progr-line-graph-gu.png)


*Play Requests/Unique Subscribers for programmers*

+++

+++MVPDs: Unique Subscribers

![](assets/mvpd-line-graph-gu.png)

*Unique Subscribers for MVPDs* 

+++

<br/>

The x-axis represents the time based on the current interval and the y-axis represents basic subscriber activity metrics during that period. The line graphs help you visualize and compare activity of the subscribers in the current segment. Depending on the version of Account IQ the metrics include:

* **AuthN OK**: Number of successful authentications. Read more about [AuthN OK](/help/accountiq/product-concepts.md#authn-ok-def).

* **AuthZ OK**: Number of successful authorizations. Read more about [AuthZ OK](/help/accountiq/product-concepts.md#authz-ok-def).

* **Play Requests**: Number of play requests. Read more about [Play requests](/help/accountiq/product-concepts.md#play-requests-def).

* **Unique Subscribers**: Number of successful unique subscribers. Read more about [Unique subscribers](/help/accountiq/product-concepts.md#unique-subscriber-def).

>[!NOTE]
>
>The availability of metrics varies depending on the version of Account IQ.

## Snapshot overview-accounts above thresholds {#snapshot-overview}

Fine tune your analytics and reports using this additional filter to set various usage thresholds. Once you have selected a segment, you can also use following filters to further analyze subscriber behavior:

* Number of Devices Threshold

* Number of IPs Threshold

* Number of Zip Codes Threshold

When you update threshold values in [Accounts Segment-based on selected thresholds](#account-segments-basedon-segments) panel, you will view the effect in:

* [Devices per week (or month) per account](#devices-week-account)

* [Locations per week (or month) per account](#locations-week-account)

* [IPs per week (or month) per account](#ip-week-account)

* [Historical view of accounts segment](#account-segment-historical-view)

>[!NOTE]
>
>Each threshold is set to a default value of 4. Which means, the General Usage page shows analysis for subscribers using more than four devices, consuming content from more than four different IP addresses, *and* more than four different zip codes.

### Accounts segment-based on selected thresholds {#account-segments-basedon-segments}

The **Accounts Segment-based on selected thresholds** panel gives you options to set thresholds (between 1 and 10) for number of devices, number of IPs, and number of Zip codes.

The graph shows you the:

* Absolute number of subscriber accounts.

* Percentage out of the total subscriber accounts in the segment that are using the number of devices, from the number of IPs, in the number of Zip codes as specified by the thresholds.

![](assets/select-thresholds.png)

## Devices per week (or month) per account {#devices-week-account}

This bar graph provides insights into usage behavior in terms of how the subscribers are using their devices to access content.

The x-axis plots Number of Accounts, and y-axis plots Number of Devices. Based on the threshold you set for number of devices per account, it marks the absolute number of subscriber accounts consuming content from a specific number of devices in a week's duration.  

![](assets/bar-gr-devices-w-acc.png)

When hovering over a bar (specific to number of devices), a label appears that gives information about the number of subscriber accounts (and the percentage out of total subscriber accounts in the segment) that are streaming channel content using those many devices in a week.

The graph also marks the following:

* A red line to mark the threshold you set.

* A green line to mark the average of the number of different devices used by a subscriber account per week (or month).

The donut provides an alternate view of the devices in use by accounts in the current segment above the set threshold.

![](assets/donut-devices-w-acc.png)

## Locations per week (or month) per account {#locations-week-account}

Similar to the metric for [Devices per week (or month) per account](#devices-week-account), the Locations per week (or month) per Account metric lets you analyze the subscriber account usage from different locations. The x-axis plots Number of Accounts, and y-axis plots Number of Locations.

![](assets/graph-loc-week-acc.png)

Once you have set the threshold for the number of locations, you can use the graph to identify the following:

* Number (and percentage) of subscribers that are consuming content from (a specific) x number of locations in a week.

* Percentage of total subscriber accounts that are viewing content from more locations than the threshold.

* Compare the weekly average (number of different locations for an account) with threshold.

## Ips per week (or month) per account {#ip-week-account}

Similar to the metric for **Number of Locations per week per account**, the **Number of IPs per week per account** metric lets you evaluate the amount of change at the source of streaming for the current segement.

The x-axis plots Number of Accounts, and y-axis plots Number of IPs.

![](assets/graph-ip-week-acc.png)

Once you have defined a segment and set the threshold for the number of IPs, you can use the graph to identify the following:

* Number (and percentage) of subscribers that are consuming content from a specific number of IP in a week.

* Percentage of total subscriber accounts that are viewing content from more IP addresses than the threshold.

* Compare the weekly average (number of different IPs for an account) with the threshold.

## Accounts segment-historical view {#account-segment-historical-view}

The Historical View bar graph helps you compare the usage metrics across different time intervals. Also, it collectively plots the various usage metrics, such as [Devices per week (or month) per account](#devices-week-account), [Locations per week (or month) per account](#locations-week-account), and [IPs per week (or month) per account](#ip-week-account).

* The x-axis plots the time interval, and y- axis plots number of subscriber accounts, devices, locations and IPs.

* The orange colored bars signify segments in various time intervals.

* The line graph plots the changes in [Devices per week (or month) per account](#devices-week-account), [Locations per week (or month) per account](#locations-week-account), and [IPs per week (or month) per account](#ip-week-account) values across the time interval based on the threshold.

![](assets/historical-view.png)

* The blue bars signify the total number of active subscribers across the industry for a time interval.

* You can select specific legends, and they help you scale the graph.

![](assets/historical-view-total.png)
