---
title: Policy update list
description: Policy update list
copied-description: yes
exl-id: 78078e95-775e-4c64-ab0f-d8bf644f3aee
---
# Policy update list {#policy-update-list}

You can use Policy Update Lists to communicate policy changes to a License Server. If a policy is modified after it is used to package content, it is desirable to have the License Server aware of the most recent version of the policy, so that version can be used to issue a license.

To create a Policy Update List for the first time, click **[!UICONTROL Add policies]** to view all available policies on the server. For any policies that have been updated since they were used to package content, select the **[!UICONTROL update]** radio button.

If you no longer want to use a policy to issue any licenses and the policy was already used to package content, you may wish to revoke the policy. To do so, select the **[!UICONTROL revoke]** radio button. When the desired policies have been selected, choose **[!UICONTROL Create Policy Update List]**. A file called [!DNL PolicyUpdateList.dat] will be saved in the [!DNL Resources] Directory.

To modify an existing Policy Update List, click **[!UICONTROL Add policies]** to view all available policies on the server. Choose the additional policies to add or revoke. Existing entries in the Policy Update List can be changed in the upper section of the screen. Policies that are marked **[!UICONTROL updated]** may be changed to **[!UICONTROL revoked]**, but once a policy is **[!UICONTROL revoked]**, it cannot be changed back to **[!UICONTROL updated]**.

When the desired changes have been made, choose **[!UICONTROL Create Policy Update List]**, and the [!DNL PolicyUpdateList.dat] file is regenerated. If a policy is already in the policy update list and was updated since the last time the list was generated, the most recent version of the policy will be used when the Policy Update List is generated again.
