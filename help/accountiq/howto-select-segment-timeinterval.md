---
title: Define a segment and time interval
description: Define a segment and time interval
exl-id: 86fe010d-3202-4ce2-b803-ff44f5538d7e
---
# Define a segment and time interval {#define-segment}

All analysis or viewing reports in [!UICONTROL Account IQ] begin with defining segment and selecting time interval for evaluation. [Segment](/help/accountiq/product-concepts.md#segmet-def) refers to all the subscribers or viewers that meet your criteria (subscribing to an MVPD and viewing sepcific channels) of evaluation.

![](assets/segment-panel.png)

*Figure: Segment and time interval selection*

At the top of all the reports pages in [!UICONTROL Account IQ], there is a panel to define segment by selecting MVPDs, channel programmers, and [!UICONTROL Granularity and Time Interval].

## Segment selection {#select-segment}

### Select MVPDs in segment {#select-segment-mvpds}

To select MVPDs from **[!UICONTROL MVPDs in segment]** option:

1. Click or tap the **[!UICONTROL MVPDs in segment]** dropdown option.

   >[!NOTE]
   >
   >**All** industry MVPDs are selected by default. From here, you can select either of the **Top 10 MVPDs by sharing score**, **Top 10 MVPDs by usage**, **Top 10 MVPDs by accounts**, or individual MVPDs. However, to select individual MVPDs you need to deselect **All**.

1. Click or tap the desired MVPDs.

    You can remove an MVPD from the selection by deselecting it.

1. Click or tap **[!UICONTROL Apply selection]** for your selection to take effect. Otherwise, you will loose the selection you made.

   >[!NOTE]
   >
   >If you select Isolation mode, then none of the other MVPDs can be selected.

### Select channels in segment {#select-segment-channels}

To select the desired programmer channels from the **[!UICONTROL Channels in segment]** option:

1. Click or tap the **[!UICONTROL Channels in segment]** dropdown option.

   >[!NOTE]
   >
   >**All** programmer channels for your company are selected by default. To select individual channels or programmers you must first deselect **All**.

1. Click or tap the desired channels or programmers.

   The top level list items in the **[!UICONTROL Channels in segment]** are [programmer](/help/accountiq/product-concepts.md#programmer-def) companies and the list items under programmer names are their [channels](/help/accountiq/product-concepts.md#channel-def). You can either select individual channels under programmers, or select programmers and all the activities of the channels under that programmer are included in report and graph results.

   ![](assets/programmer-channels.png)


   *Figure: Programmers and channels listed in channels selector*

   >[!IMPORTANT]
   >
   >Outcomes of selecting individual channels under a programmer are not the same as those of selecting the programmer.
   >
   >
   >When you select individual channels, activities of those channels are broken down individually in some reports. However, when you select the parent programmer of all those channels, all of the activity of those channels are included but are not broken down individually in reports.

1. Click or tap **[!UICONTROL Apply selection]** for your selection to take effect.

>[!NOTE]
>
>You cannot select more than 10 items in the MVPD or programmer pulldown menus.

### Deselect MVPDs and channels {#deselect-segment-mvpds-channels}

In addition to changing your selection in the **[!UICONTROL MVPDs in segment]** and **[!UICONTROL Channels in segment]** segment selectors, you can deselect the previously selected MVPDs and channels by:

* Selecting the **[!UICONTROL Remove]** icon (![remove icon](assets/remove-icon.png)) on the names of these selected MVPDs and channels displayed below segment selector.

* You can also use **[!UICONTROL Clear Selection]** to remove all the previously selected MVPDs or channels.

![](assets/segment-panel-selection.png)

*Figure: Selected MVPDs and channels in segment and time interval panel*

## Granularity and Time Interval selection {#granularity-timeinterval}

To select a time period of evaluation:

1. Select the **[!UICONTROL Granularity and Time Interval ]** from the date picker.

1. Select either **[!UICONTROL Week]** or **[!UICONTROL Month]** from **[!UICONTROL Aggregate By]** option to set granularity for your evaluation.

   ![](assets/granularity-timeinterval-weekwise.png)
   
   
   *Figure: Date picker to select Granularity and Time Interval*

1. Once you have selected granularity, you can use forward or backward arrows to move forward or backward in time.

1. Specify a time period in past (in month or week based on selected granularity)  for evaluation.

1. Select **[!UICONTROL Apply Selection]** to make sure your selection takes effect.
