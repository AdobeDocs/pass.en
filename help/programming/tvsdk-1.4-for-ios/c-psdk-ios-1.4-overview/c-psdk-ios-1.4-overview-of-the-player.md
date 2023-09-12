---
description: TVSDK for iOS includes a variety of features.
title: Primetime TVSDK features
exl-id: 1968c072-2651-442d-9e4c-412f7959bcab
---
# Primetime TVSDK features {#primetime-tvsdk-features}

TVSDK for iOS includes a variety of features and provides the following main capabilities:

* VOD and live/linear playback

    * Management of the playback window, including methods that play, stop, pause, seek, and retrieve the playhead position
    * Support for full-event replay 
    * Closed captioning (608, WebVTT) and alternate forms of audio for increased accessibility 
    * DVR capability 
    * Adaptive bit rate (ABR) logic and initial set up of ABR controls 
    * Subscription to non-HLS and HLS tags 
    * Live manifest failover support

* Advertising

    * VPAID 2.0 
    * Client-side ad stitching

        * Seamless ad insertion, including support for VAST/VMAP 
        * Support for custom cue tags for ads 
        * Support for marking, replacing, and deleting C3 ads
        * Customizable content/ad insertion workflow including blackout signaling

* Content protection

    * Access to digital rights management (DRM)-related services 
    * Playback of HLS streams unencrypted or with Protected HTTP Live Streaming (PHLS) 
    * Resolution-based output control, based on DRM policy

* Video and ad tracking

    * QoS event tracking 
    * Notifications that help TVSDK and your application to communicate asynchronously about the status of videos, advertisements, and other elements, and also that log activity 
    * Integration with Adobe Analytics and heartbeat support

* Logging

    * Debug logging
