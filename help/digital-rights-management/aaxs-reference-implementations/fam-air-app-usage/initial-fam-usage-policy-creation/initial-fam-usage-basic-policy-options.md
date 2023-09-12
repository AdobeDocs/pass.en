---
title: Basic Policy Options
description: Basic Policy Options
copied-description: yes
exl-id: d5ddd54d-9301-42da-b7fd-0b838eb6cf9d
---
# Basic Policy Options {#basic-policy-options}

The following table describes the Basic Policy preferences: 

|  Preference  | Description  |
|---|---|
|  Policy Duration  | Specifies the validity period of content protected with this policy.  |
|  | Start at  | Licenses cannot be used until this date/time.  |
|  | End at  | Licenses cannot be used after this date/time.  |
|  | End after  | Specifies the amount of time a license is valid (in minutes), starting from the time it is packaged.  |
|  License Caching  | Specifies whether licenses may be cached by the client.  |
|  | | Licenses cannot be used after this date/time.  |
|  | Delete after  | Specifies the amount of time a license is valid (in minutes), starting from the time it the license is issued by the license server.  |
|  | Cache Indefinitely  | License may be cached on the client indefinitely.  |
|  | No License Caching  | License may not be cached by the client. A new license must be obtained from the server each time the user plays the content.  |
|  Authentication  | |
|  | Anonymous  | No authentication is required to view the content.  |
|  | Authenticated  | Username/password authentication is required.  |
|  Enable License Chaining  | Allows a license to be updated using a parent root license for batch updating of licenses. Once the leaf license expires, the server may issue the client a root license, which will renew all content protected with this policy.  |
