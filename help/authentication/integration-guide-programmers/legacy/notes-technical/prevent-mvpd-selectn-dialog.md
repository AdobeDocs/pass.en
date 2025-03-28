---
title: Prevent MVPDs from appearing in the Selection Dialog
description: Prevent MVPDs from appearing in the Selection Dialog
exl-id: 20faf501-c006-45e2-a725-fb1273ecaffe
---
# (Legacy) Prevent MVPDs from appearing in the Selection Dialog

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

## Issue {#issue-prevent-mvpd-sel-dialog}

You need to prevent ("block-list") specific MVPDs from appearing in the MVPD selector.
 

## Solution {#solution-prevent-mvpd-sel-dialog}

The solution is to do a block-listing when `displayProviderDialog()` is called. 

For example, if you would like CableCompany_1 and CableCompany_2 not to show inside the MVPD selector, you would do something like what is shown in the following example.

```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if (!isBlocklisted(currentMvpd.ID)) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isBlocklisted(mvpdID) {
    // Implement block-listing on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
} 
```
