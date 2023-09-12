---
title: Best practices for companion banner ads
description: Best practices for companion banner ads
copied-description: yes
exl-id: e7d15916-9059-4993-a588-baf7d7ddc534
---
# Best practices for companion banner ads {#best-practices-for-companion-banner-ads}

TVSDK supports companion banner ads, which are ads that accompany a linear ad and often remain on the page after the linear ad ends. Your application is responsible for displaying the companion banners that are provided with a linear ad.

When displaying companion ads, follow these recommendations:

* Attempt to present as many of a video ad's companion banner ads as will fit in your player's layout. 
* Present a companion banner only if you have a location that matches the ad's specified height and width.

  >[!IMPORTANT]
  >
  >Do not resize the ad.

* Begin presenting the companion banner(s) as soon as possible after the ad begins. 
* Do not overlay the main ad/video container with companion banners. 
* You can display companion banners after the ad ends.

The standard practice is to display each companion banner until you have a replacement for the ad.
