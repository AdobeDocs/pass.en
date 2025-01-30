---
title: Allow MVPDs in the Selection Dialog
description: Allow MVPDs in the Selection Dialog
exl-id: 2c0e0f06-ddc6-4bea-90dc-d7ef8e78d27e
---
# (Legacy) Allow MVPDs in the Selection Dialog {#allow-mvpds-selection-dialog}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

## Issue {#issue}

The Programmer may want to test or check the user experience of new MVPD integrations before going public to end users.

## Solution {#solution}

In the `displayProviderDialog()` callback, Adobe Pass Authentication returns all of the MVPDs integrated with the selected Programmer (Requestor ID). But the Programmer can apply a filter on the return array of MVPDs and display only those that are in both lists.

## Example {#example}

This example demonstrates how to display only CableCompany_1 and CableCompany_2 inside the MVPD selector dialog, and to not show CableCompany_NewIntegration.
 
```C
function displayProviderDialog(mvpdList) {
    var allowlisted = new Array();
    for (var i = 0; i < mvpdList.length; i = i + 1) {
        var currentMvpd = mvpdList[i];
        if ( isAllowListed(currentMvpd.ID) ) {
            allowlisted.push(currentMvpd);
        }
    }
    displayAllowlisted(allowlisted);
}

function isAllowListed(mvpdID) {
    // Implement allowlisting on MVPD IDs.
    return (mvpdID === 'CableCompany_1' || mvpdID === 'CableCompany_2');
}

function displayAllowlisted(list) {
    // TODO: Implement site-specific logic here.
}

```
