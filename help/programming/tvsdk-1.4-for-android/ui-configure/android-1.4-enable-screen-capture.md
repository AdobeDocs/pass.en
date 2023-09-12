---
keywords: setSecure;VideoEngineView
title: Enable screen capture
description: Enable screen capture
copied-description: yes
exl-id: 5dd1bf4e-ab50-4b57-89e4-eacc291a9fe3
---
# Enable screen capture{#enable-screen-capture}

 TVSDK disallows screen capture by default. The player calls `setSecure(true)` on the `com.adobe.ave.VideoEngineView` object at construction time. You have access to this object, as you have to construct a `VideoEngineView` object and supply it to the `VideoEngine` object.

To enable screen capture in your app: 

1. Construct the `com.adobe.ave.VideoEngineView` object.
1. Call `setSecure(false)` on your `VideoEngineView` object.
