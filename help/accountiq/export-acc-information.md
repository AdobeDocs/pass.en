---
title: Export information for accounts with high sharing score
description: Export information for accounts with high sharing score.
exl-id: df41ddd2-fde3-4861-abd4-6e32f0be9ea5
---
# Export information for accounts with high sharing score {#export-account-info-high-score}

[!UICONTROL Account IQ] allows you to export account sharing details for top 1000 subscriber accounts based on their [sharing probabilities](/help/accountiq/product-concepts.md#account-sharing-probability-def). You can export the account sharing information for the current [segment](/help/accountiq/product-concepts.md#segment-def) and [specified time interval](/help/accountiq/product-concepts.md#time-interval-def) on the [Shared Accounts Reports](/help/accountiq/shared-acc-reports.md) page.

To export the account sharing information of subscriber accounts for a specific segment, follow these steps:

1. Log in with your authorized credentials.
1. Navigate to the **Shared Accounts** tab under **Reports** section.
1. Select the required segment and time interval from segment and time interval panel. Learn [how to select segments and time interval](segments-timeinterval.md).

   If required, refer to the instructions for [creating a new segment](work-with-segments.md#create-new-segment) or [editing a segment](work-with-segments.md#edit-segment).

1. Select **[!UICONTROL Export top 1000 accounts]** option located in the upper-right corner of the segment and time interval panel.

   ![Export top 1000 accounts](assets/export-top-1000-accounts.png)

   *Select Export top 1000 accounts option*

1. The file will automatically download to your local machine.

   The system saves the statistical information for 1000 accounts with the highest sharing probabilities in a CSV file.

1. Find the file on your local machine to open and access the data.

The CSV file contains the data for top 1000 accounts based on the sharing probabilities of the subscriber accounts in the current segment sorted in decreasing order.

![exported data in csv format](assets/exported-csv.png)

*Exported data in CSV format*

## Columns in the exported report {#columns-in-export}

**Week/Month**  

The selected week or month within the **[!UICONTROL Granularity and Time Interval]** option in the segment selector. 

**MVPD** 

If you are a programmer, the column shows the distributor with whom the account is subscribed.

>[!NOTE]
>
> The **MVPD** column is only available for TV Everywhere versions. 

**Subscriber ID** 

The unique identifier for the specific account.

**Minimum # Devices** 

The minimum number of devices from which users are actively streaming content. 

>[!NOTE]
>
>The actual number of devices streaming content is certainly greater than the minimum number of devices specified for a particular account. 

**Minimum # Persons**  

The minimum number of individuals actively streamed content using those devices.

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

>[!NOTE]
>
> **[!UICONTROL # AuthN OK]** may not be available for specific D2C services.

**[!UICONTROL # AuthZ OK]**

The number of times an MVPD has authorized a stream or granted access to content for that account.

>[!NOTE]
>
>**[!UICONTROL # AuthZ OK]** is not available for D2C services. 

>[!NOTE]
>
>For TV Everywhere, **[!UICONTROL # AuthZ OK]** related to **[!UICONTROL # Play Requests]**. It will always be less than **[!UICONTROL # Play Requests]** because Adobe typically caches the authorizations from MVPDs for approximately 24 hours.


**[!UICONTROL # Play Requests]**

The actual number of streams occurred during a specified time period.

   >[!NOTE]
   >
   >The play requests column isn't available in the MVPD version.

**[!UICONTROL # Channels]**

The overall number of channels that the account has watched over a specified period.

>[!NOTE]
>
> For D2C services **[!UICONTROL # Channels]** is equivalent to number of **[!UICONTROL # Video categories]**. 

>[!NOTE]
>
>For TV Everywhere, they include the channels that may not belong to the logged-in programmer. This number for the account includes your channel and other channels accessed during the specified period.


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
