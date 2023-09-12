---
title: Request a certificate (Requester)
description: Request a certificate (Requester)
copied-description: yes
exl-id: 290231ec-1146-4bfb-a449-b8ff85704197
---
# Request a certificate (Requester){#request-a-certificate-requester}

1. Log onto the Certificate Enrollment site.

   The user who requests a certificate must be a Requester. 

1. On the Request tab, select the type of certificate (License Server, Packager or Transport).

   >[!NOTE]
   >
   >This option is not shown for the Evaluation and Trial SDK versions. Those SDK versions use one certificate.

1. Do one of the following:

    * Upload the CSR file. 
    * Copy the CSR information from the CSR and paste it into the form.

       >[!NOTE]
       >
       >To copy the CSR information, select the text between, not including, the beginning tag `(-----BEGIN CERTIFICATE REQUEST-----)` and end tag `(-----END CERTIFICATE REQUEST-----)`.

1. Click the **[!UICONTROL Submit Request]** button.

   An e-mail is sent to the Account and Secondary Administrators for review. The Requester is Cc'd.
