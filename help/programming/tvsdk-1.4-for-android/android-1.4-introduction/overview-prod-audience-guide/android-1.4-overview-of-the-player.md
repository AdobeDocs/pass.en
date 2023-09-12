---
description: TVSDK for Android includes a variety of features and provides the following main capabilities 
title: Primetime TVSDK features
exl-id: 7df03752-98aa-4317-8e41-a284472cabbb
---
# Primetime TVSDK features{#primetime-tvsdk-features}

TVSDK for Android includes a variety of features and provides the following main capabilities:

* VOD and live/linear playback

    * Management of the playback window, including methods that play, stop, pause, seek, and retrieve the playhead position 
    * Support for full-event replay 
    * Closed captioning (608, 708, WebVTT) and alternate forms of audio for increased accessibility 
    * Control for text styling in captions 
    * DVR capability , fast forward/fast rewind (trick-play mode) 
    * Adaptive bit rate (ABR) logic and initial set up of ABR controls 
    * Live manifest failover support 
    * Adjustable playback buffers 
    * Fragment duration, size, and time-to-download tracking support

* Advertising

    * VPAID 2.0 
    * Client-side ad stitching

        * Partial Ad-Break Insertion, that enables a TV-like experience of being able to join in the middle of an ad. 
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
    * Notifications that help TVSDK and your application to communicate asynchronously about the status of videos, advertisements, and other elements , and also that log activity

* Logging

    * Debug logging 
    * Tracking support for fragment duration, size, and time-to-download
