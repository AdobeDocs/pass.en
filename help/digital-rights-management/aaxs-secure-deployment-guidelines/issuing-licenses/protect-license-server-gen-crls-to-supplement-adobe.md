---
title: Generate CRLs to supplement those published by Adobe
description: Generate CRLs to supplement those published by Adobe
copied-description: yes
exl-id: 05dc2159-fa7f-4772-9f25-c89370b4981e
---
# Generate CRLs to supplement those published by Adobe{#generate-crls-to-supplement-those-published-by-adobe}

Adobe Access lets you create CRLs to supplement the machine CRL published by Adobe. Adobe Access SDK checks and enforces the Adobe CRLs, however, you can disallow additional client machines by creating a CRL that revokes additional machine credentials. To do this, you must pass the CRL to Adobe Access SDK, then, when issuing a license, the SDK checks both the Adobe CRL and your own CRL.

To learn more about generating CRLs, see `RevocationListFactory` in *Adobe Access API Reference*.
