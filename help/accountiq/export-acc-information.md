---
title: Export information for accounts with high sharing score
description: Export information for accounts with high sharing score.
exl-id: df41ddd2-fde3-4861-abd4-6e32f0be9ea5
---
# Export information for accounts with high sharing score {#export-account-info-high-score}

[!UICONTROL Account IQ] allows you to export account sharing details for top 1000 subscriber accounts based on their [sharing probabilities](/help/accountiq/product-concepts.md#account-sharing-probability-def). As a programmer and MVPD user, you can export the account sharing information for the current [segment](/help/accountiq/product-concepts.md#segment-def) and [specified time interval](/help/accountiq/product-concepts.md#time-interval-def) on the [Shared Accounts Reports](/help/accountiq/shared-acc-reports.md).

To export the account sharing information of subscriber accounts for a specific segment, follow these steps:

1. Log in with your authorized programmer or MVPD credentials.
1. Navigate to the **Shared Accounts** tab under **Reports** section.
1. Select a desired segment and time interval from segment and time interval panel. Know [how to select segment and time interval](segments-timeinterval.md).

   If required, refer to the instructions for [creating a new segment](work-with-segments.md#create-new-segment) or [editing a segment](work-with-segments.md#edit-segment).

1. Select **[!UICONTROL Export top 1000 accounts]** option located in the upper-right corner of the segment and time interval panel.

   ![Export top 1000 accounts](assets/export-top-1000-accounts.png)

   *Figure: Select Export top 1000 accounts option*

1. If given the option, choose the location to save the file on your local machine, optionally rename your file in the **File name**, and select **[!UICONTROL Save]**. Alternatively, the file will automatically be saved to the download folder designated by your browser.

   The system saves the statistical information for 1000 accounts with the highest sharing probabilities for current segment and specified time interval to the chosen location on your local machine.

1. Find the saved file on your local device to open and access the data.

>[!NOTE]
>
>The report saves in CSV format. You can open the exported file using a preferred CSV viewer or editor like Microsoft Excel.

The exported CSV file sorts the data in decreasing order based on the sharing probabilities of the subscriber accounts in the current segment for a specified time interval. 

![exported data in csv format](assets/exported-csv.png)

*Figure: Exported data in CSV format*

## Columns in the exported report {#columns-in-export}

**Week/Month**

The selected week or month within the **[!UICONTROL Granularity and Time Interval]** option in the segment selector for which the sharing statistics are sought.

**MVPD**

If you are a programmer user, the column shows which MVPD the subscriber account belongs to.

**Subscriber Id**

The unique identifier for the specific account that is discussed within a row.

**Minimum # Devices**

The bare minimum number of devices from which users are actively streaming content.

>[!NOTE]
>
>The actual number of devices streaming content is certainly greater than the minimum number of devices specified for a particular account.

**Minimum # Persons**

The bare minimum number of individuals actively streamed content using those devices.

>[!NOTE]
>
>The actual number of individuals streaming content is certainly greater than the minimum number of persons assigned to a particular account.

**[!UICONTROL # IPs]**

The number of IP addresses from which content is streamed.

**[!UICONTROL # Locations]**

The number of locations (based on zip code) from which content is streamed.

**[!UICONTROL # Cities]**

The number of cities where the streaming activity has taken place.

**[!UICONTROL # States]**

The number of states where the streaming activity has taken place.

**[!UICONTROL # Clusters]**

The number of distinct [clusters](/help/accountiq/product-concepts.md#cluster-def) where streaming has taken place.

**[!UICONTROL Geographic span (miles)]**

The maximum distance between the streaming locations associated with the account.

**[!UICONTROL # AuthN OK]**

The number of logins users make during the specified period using that account.

**[!UICONTROL # AuthZ OK]**

The number of times an MVPD has authorized a stream or granted access to content for that account.

>[!NOTE]
>
>The **[!UICONTROL # AuthZ OK]** is linked to **[!UICONTROL # Play Requests]**. It's smaller than **[!UICONTROL # Play Requests]** because Adobe typically caches the authorizations from MVPDs for approximately 24 hours.

**[!UICONTROL # Play Requests]**

The actual number of streams occurred during a specified time period.

   >[!NOTE]
   >
   >The play requests column is'nt available for MVPD users.

**[!UICONTROL # Channels]**

The overall number of channels that the account has watched over a specified period.

>[!NOTE]
>
>**[!UICONTROL # Channels]** include the channels that may not belong to the logged-in programmer.
>
>This number for the account includes your channel and other channels accessed during the specified period.

**Usage Pattern**

The values within these columns serve as identifiers corresponding to one of the 14 patterns we use to categorize all user accounts.

 | ID | 1 | 2 | 3 | 4 | 5 and 8 | 6 | 7 | 9 | 10 and 11 | 12 | 13 | 14 |
 |---|---|---|---|---|---|---|---|---|---|---|---|---|
 | Usage Patterns | Regular user | Traveler or commuter | Large family | Close family and friends | Social group sharing | Large group of friends | Concurrent streaming | Community sharing | Uncertain behavior | Small family | Second home | Abnormal Usage |

{style="table-layout:auto"}

*Table: Usage pattern identifiers in exported CSV mapping with usage patterns*

**Sharing Probability**

The likelihood that a specific account is sharing its credentials.

>[!NOTE]
>
> The average of the sharing probability of all the accounts in the selected segment is used to compute the [sharing level](/help/accountiq/data-panels.md#sharing-level) of the [Aggregated sharing score](/help/accountiq/data-panels.md#aggregated-sharing).
