---
title: Consume locally generated CRLs
description: Consume locally generated CRLs
copied-description: yes
exl-id: d96418d0-8fd3-4f6d-8480-191fe540080a
---
# Consume locally generated CRLs{#consume-locally-generated-crls}

To consume locally generated certificate revocation lists (CRLs) and policy update lists, use Adobe Access APIs to verify the signature. The APIs verify that the lists have not been tampered with and that they were signed by the correct License Server.

* Call `RevocationList.verifySignature` to check the signature before providing the RevocationList to any APIs.

  For more information, see `RevocationListFactory` in the *Adobe Access API Reference*. 

* Call `PolicyUpdateList.verifySignature`to check the signature before providing the `PolicyUpdateList` to any APIs.

  For more information, see `PolicyUpdateList` in the *Adobe Access API Reference*.
