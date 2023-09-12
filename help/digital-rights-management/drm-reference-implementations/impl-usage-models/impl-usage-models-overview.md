---
title: Overview
description: Overview
copied-description: yes
exl-id: 974b9a5e-43f6-4ec8-8048-dfcc1cff0f6f
---
# Overview{#overview}

The Reference Implementation includes a demo mode option that demonstrates how to implement different usage models for a segment of packaged content. The demo mode features business logic for these usage models:

* **Download-To-Own (DTO)** - Users can download the content online or offline, and are issued a permanent license for the content. 
* **Rental/Video-On-Demand (VOD)** - The available content comes with time-based restrictions. For example, users can play content during a 30-day period. Once playback begins, the user has up to 48 hours to finish watching the content. The content must be viewed in 30 days. 
* **Subscription (all-you-can-eat)** - Some services offer paid subscriptions that give users unlimited access to a large library of content as long as they continue to pay a monthly fee. The license server issues a unique license for each segment of content and also issues a root license that expires at the end of the subscription period. Each month, when users renew their subscription, the root license must also be renewed. 

  >[!NOTE]
  >
  >For the preceding usage models, after acquiring a license, users must enter their credentials so that the server can verify that the users have a rental account.

* **Ad-funded** - Content is monetized by including advertising as part of the experience. With this model, content can be distributed and does not require user authentication.

In usage model demo mode, the business logic on the server controls the attributes for generated licenses. At packaging time your DRM policy only has to indicate whether or not authentication is required.

To enable all four usage models, you only need to include two DRM policies:

* One DRM policy that allows anonymous access for the Ad-funded model 
* One DRM policy that requires user name/password authentication for the other three usage models.

When a user requests a license, a client application can determine whether to prompt the user for authentication based on the authentication information in the DRM policies.
