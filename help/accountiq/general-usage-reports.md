---
title: General Usage reports
description: General Usage reports
exl-id: 1272073a-61fe-47ec-aced-2e8055b6b11e
---
# [!UICONTROL General Usage] reports {#general-usage-reports}

[!UICONTROL Account IQ] reports are basic analytic tools and analysis that let you drill into your data to isolate [cohorts](/help/accountiq/product-concepts.md#segmet-def), identify anomalies, and build an understanding of your account characteristics.

[!UICONTROL General Usage] reports page provides tools to carve out subgroup metrics based on the number of account devices in use, IPs detected, and respective zip codes.

The reports are all based on the current segment selected using [Segments and time interval](/help/accountiq/segments-timeinterval.md) panel. You can fine tune your selection and further narrow it down by specifying (number of devices, number of IPs, and number of zip codes) thresholds in [Snapshot Overview - Accounts above thresholds](#snapshot-overview) panel.

## Play Requests/Unique Subscribers {#playreq-uniquesubs}

The line graphs here gives you a view of the changes over time of values, such as Play Requests and Unique Subscribers in a selected time interval for the defined segment.

+++ D2C services- Play Requests/Unique Subscribers

![](assets/d2c-line-graph-gu.png)


*Play Requests/Unique Subscribers for D2C services*

+++

+++Programmer- Play Requests/Unique Subscribers

![](assets/progr-line-graph-gu.png)


*Play Requests/Unique Subscribers for programmer user*

+++

+++MVPD- Unique Subscribers

![](assets/mvpd-line-graph-gu.png)

*Unique Subscribers for MVPD user* 

+++

<br/>

The x-axis represents the time based on the current interval and the y-axis represents basic subscriber activity metrics during that period. The line graphs help you visualize and compare activity of the subscribers in the current segment. Depending on the persona the metrics include:

* **AuthN OK**: Number of successful authentications. View [AuthN OK](/help/accountiq/product-concepts.md#authn-ok-def) for more information .

* **AuthZ OK**: Number of successful authorizations. View [AuthZ OK](/help/accountiq/product-concepts.md#authz-ok-def) for more information.

* **Play Requests**: Number of Play Requests. View [Play requests](/help/accountiq/product-concepts.md#play-requests-def) for more information.

* **Unique Subscribers**: Number of successful unique subscribers. View [Unique subscribers](/help/accountiq/product-concepts.md#unique-subscriber-def) for more information.

>[!NOTE]
>
>The availability of metrics varies depending on the persona.

## Snapshot Overview - Accounts above thresholds {#snapshot-overview}

Fine tune your analytics and reports using this additional filter to set various usage thresholds. Once you have selected a segment, you can also use following filters to further analyze subscriber behavior:

* Number of Devices Threshold

* Number of IPs Threshold

* Number of Zip Codes Threshold

When you update threshold values in [Accounts Segment - based on selected thresholds](#account-segments-basedon-segments) panel, you can view the changes in:

* [Devices per week (or month) per account](#devices-week-account)

* [Locations per week (or month) per account](#locations-week-account)

* [IPs per week (or month) per account](#ip-week-account)

* [Historical view of accounts segment](#account-segment-historical-view)

>[!NOTE]
>
>The default value for each of the thresholds is 4. Which means, the General Usage page shows analysis for subscribers using four or more devices, consuming content from four or more different IP addresses, *and* four or more different zip codes.

### Accounts Segment - based on selected thresholds {#account-segments-basedon-segments}

The **Accounts Segment - based on selected thresholds** panel gives you options to set thresholds (between 1 and 10) for number of devices, number of IPs, and number of Zip codes.

The graph shows you the:

* Absolute number of subscriber accounts.

* Percentage out of the total subscriber accounts in the segment that are using the number of devices, from the number of IPs, in the number of Zip codes as specified by the thresholds.

![](assets/select-thresholds.png)

## Devices per week (or month) per Account {#devices-week-account}

The **bar graph** provides insights into usage behavior in terms of how the subscribers are using their devices to access content.

The x-axis plots Number of Accounts, and y-axis plots Number of Devices. Based on the threshold you set for number of devices per account, it marks the absolute number of subscriber accounts consuming content from a specific number of devices in a week's duration.  

![](assets/bar-gr-devices-w-acc.png)

When hovering over a bar (specific to number of devices), a label appears that gives information about the number of subscriber accounts (and the percentage out of total subscriber accounts in the segment) that are streaming channel content using those many devices in a week.

The graph also marks the following:

* A red line to mark the threshold you set.

* A green line to mark the average of the number of different devices used by a subscriber account per week (or month).

 You can assess the extent of sharing by comparing the threshold level with the weekly average number of different devices used by an account.

The graph also gives a glimpse of the percentage of subscriber accounts that are using more number of devices than the set threshold.

The donut chart helps you examine the magnitude of subscriber accounts consuming channel content using devices more than the set threshold (in a time interval) at a glance.

![](assets/donut-devices-w-acc.png)

## Locations per week (or month) per Account {#locations-week-account}

Like [Devices per week (or month) per Account](#devices-week-account), the Locations per week (or month) per Account metric help you analyze the subscriber account usage from different locations to closely identify password sharing. The x-axis plots Number of Accounts, and y-axis plots Number of Locations.

Results from this metric combined with number of [Devices per week (or month) per Account](#devices-week-account) and number of [IPs per week (or month) per Account](#ip-week-account) help you examine the password sharing instances more accurately; such that authentic users are not counted in.

![](assets/graph-loc-week-acc.png)

Once you have defined a segment and set the threshold for the number of locations, you can use the graph to identify the following:

* Number (and percentage) of subscribers that are consuming content from (a specific) x number of locations in a week.

* Percentage of total subscriber accounts that are viewing content from more locations than the threshold.

* Compare the weekly average (number of different locations for an account) with Threshold.

## IPs per week (or month) per Account {#ip-week-account}

The **Number of IPs per week per account** metric lets you analyze password sharing more precisely and with more granularity.

The x-axis plots Number of Accounts, and y-axis plots Number of IPs.

![](assets/graph-ip-week-acc.png)

Once you have defined a segment and set the threshold for the number of IPs, you can use the graph to identify the following:

* Number (and percentage) of subscribers that are consuming content from a specific number of IP in a week.

* Percentage of total subscriber accounts that are viewing content from more IP addresses than the threshold.

* Compare the weekly average (number of different IPs for an account) with the threshold.

## Accounts Segment - Historical View {#account-segment-historical-view}

The Historical View bar graph helps you compare the usage metrics across different time intervals. Also, it collectively plots the various usage metrics, such as [Devices per week (or month) per Account](#devices-week-account), [Locations per week (or month) per Account](#locations-week-account), and [IPs per week (or month) per Account](#ip-week-account).

* The x-axis plots the time interval, and y- axis plots number of subscriber accounts, devices, locations and IPs.

* The orange colored bars signify segments in various time intervals.

* The line graph plots the changes in [Devices per week (or month) per Account](#devices-week-account), [Locations per week (or month) per Account](#locations-week-account), and [IPs per week (or month) per Account](#ip-week-account) values across the time interval based on the threshold.

![](assets/historical-view.png)

* The blue bars signify the total number of active subscribers across the industry for a time interval.

* You can select specific legends, and they help you scale the graph.

![](assets/historical-view-total.png)
