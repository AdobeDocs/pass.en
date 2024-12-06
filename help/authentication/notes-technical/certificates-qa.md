---
title: Certificates Q&A
description: Certificates Q&A
exl-id: d4e493b0-4467-42b1-9758-16c5941d8051
---
# Certificates Q&A {#certificates-q}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

**Q1:** Is it possible to register certificates across iOS and Android?

**A:** The certificate for iOS and Android is the same in the current configuration. The native certificate is used for both platforms.

</br>

**Q2:** Can the same iOS certificates be used as Primary & Backup certificates in the Production and Staging environments? If it is not recommended, can you offer an explanation?

**A:** There is no point in configuring the same certificate as both Primary and Backup certificate. We have the concept of Primary and Backup certificates so that we can configure multiple certificates for a Programmer in case the Primary certificate expires or is revoked. Having a backup certificate will give Programmers time to change the Primary one without impacting the Release environment. But you can use the same set of Primary and Backup certificates for both the Production and Staging profiles.

</br>

**Q3:** Is a new certificate needed for web pages that will use the new flexible TempPass? 

**A:** The certificate (and any certificate indeed) is configured at Media Company & Programmer level. FlexibleTempPass is an MVPD, you don't need to configure any certificate for it, so if you are integrating an existing Programmer with flexible TempPass, the certificate that is already configured at Programmer / Media Company level will be used.
