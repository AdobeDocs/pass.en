---
title: Update the reference implementation DB
description: Update the reference implementation DB
copied-description: yes
exl-id: b337bf9c-7add-47b8-9576-db7fa067c51d
---
# Update the reference implementation DB{#update-the-reference-implementation-db}

To control usage models under which a license is issued to a designated user, add entries to the reference implementation database. 

1. Add entries to the `Customer` table.

   The `Customer` table includes user names and passwords to authenticate users. It also indicates whether a user has a subscription (a license that is issued under the *Subscription* usage model). 

1. Grant a user access under the Download-to-own or Video-on-demand usage models.

       Add entries to the `CustomerAuthorization` table to specify:

    * The usage model 
    * Each segment of content that a user can access

For more information on how to populate each table, see the [!DNL PopulateSampleDB.sql] script (included on your Primetime DRM DVD in the [!DNL Reference Implementation/Server/Reference Implementation Server/dbscript/] directory).
