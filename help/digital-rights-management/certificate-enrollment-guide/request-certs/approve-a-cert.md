---
title: Approve a certificate (Account or Secondary Administrator)
description: Approve a certificate (Account or Secondary Administrator)
copied-description: yes
exl-id: 71e647a8-e325-4095-a0ac-775fb5898e9e
---
# Approve a certificate (Account or Secondary Administrator){#approve-a-certificate-account-or-secondary-administrator}

1. Log onto the Certificate Enrollment site.
1. Select the **[!UICONTROL Certificates]** tab.
1. Review the request to verify that the request is valid.
1. If the request is valid, click **[!UICONTROL Approve]**.

   You may also add a comment. An e-mail is sent to the Requester stating that the request has been approved by one of the company administrators. A copy of this e-mail is sent to the company and Adobe administrators. 

1. If the request is not valid, click **[!UICONTROL Reject]** and enter a comment in the confirmation dialog.

   An e-mail is sent to the Requester stating that the request has been rejected by one of the company administrators. A copy of this e-mail is sent to the company administrators. 

When an administrator approves a certificate request, Adobe verifies the identity of the Requester. Adobe contacts the Requester at the telephone number listed in their profile.

The Adobe administrator attempts to contact the Requester twice within a three-day period. If the Adobe administrator cannot contact the Requester, they leave a message requesting a call-back or they provide a time when they will call again. If the Adobe administrator is not able to reach the Requester, an e-mail is sent to the administrators.

>[!NOTE]
>
>Only the Account and Secondary administrators can change the company telephone number and the challenge phrase of the Requester.

If the identity of the Requester is verified, the Requester receives an e-mail containing the PKCS#7 file ( [!DNL p7b]).

The Requester can copy the PKCS#7 content from the e-mail body and save it to a file or use the file that is attached to the e-mail. Adobe recommends that when you save the PKSC#7 file, you use the base name that you used to generate the private key and CSR file.

>[!NOTE]
>
>The file sent to the Requester contains only the certificate. The file does not contain private key information.
