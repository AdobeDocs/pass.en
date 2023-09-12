---
description: Browser TVSDK supports companion banner ads, which are ads that accompany a linear ad and often remain on the page after the linear ad ends. Your application is responsible for displaying the companion banners that are provided with a linear ad.
title: Companion banner ads
exl-id: 73b5c9b0-abac-47ed-a21d-3f8f90cc5b55
---
# Overview {#companion-banner-ads-overview}

Browser TVSDK supports companion banner ads, which are ads that accompany a linear ad and often remain on the page after the linear ad ends. Your application is responsible for displaying the companion banners that are provided with a linear ad.

When displaying companion ads, follow these recommendations:

* Attempt to present as many of a video ad's companion banner ads as will fit in your player's layout. 
* Present a companion banner only if you have a location that matches the specified height and width of the companion banner. 

  >[!TIP]
  >
  >Do not resize the banner.

* Present the companion banner(s) as soon as possible after the ad begins. 
* Do not overlay the main ad/video container with companion banners. 
* Continue to display companion banners after the ad ends.

  The standard is to display each companion banner until you have a replacement for this banner.
