---
description: Browser TVSDK provides your video app with information needed to respond to a user's click on a clickable ad.
title: Clickable ads
exl-id: 5fd8b38d-bde7-4d80-bfb0-3390c8f2665c
---
# Overview {#clickable-ads-overview}

Browser TVSDK provides your video app with information needed to respond to a user's click on a clickable ad.

When a user clicks on a clickable ad, a typical response from a video app is to open a new browser window and navigate to the URL associated with the ad. To facilitate this, Browser TVSDK fires ad notifications that your app can use to manage the click-through process.

In your app, you can provide the user with a control to click (e.g., a button) while the clickable ad is playing. You need to create handlers for events fired by Browser TVSDK that are associated with the ad (e.g., ad start, ad clicked, ad complete). Finally, you need to implement the specific behaviors your app will follow upon a user's ad click (e.g., whether or not to pause the ad, display the click-through URL, and so on). 

>[!NOTE]
>
>The reference player included with Browser TVSDK includes one possible working solution for processing click-through ads.
