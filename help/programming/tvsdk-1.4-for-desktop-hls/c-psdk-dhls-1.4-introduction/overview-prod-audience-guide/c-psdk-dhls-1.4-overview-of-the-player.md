---
description: TVSDK for Desktop HLS includes a variety of features and provides the following main capabilities 
title: Primetime TVSDK features
exl-id: d78ca77e-b29c-4fae-8ab9-edc55ab12847
---
# Primetime TVSDK features{#primetime-tvsdk-features}

TVSDK for Desktop HLS includes a variety of features and provides the following main capabilities:

* VOD and live/linear playback

    * Management of the playback window, including methods that play, stop, pause, seek, and retrieve the playhead position. 
    * Closed captioning (608, 708, WebVTT) and alternate forms of audio for increased accessibility 
    * Control for text styling in captions 
    * DVR capability, fast forward/fast rewind (trick-play mode) 
    * Trick play for both live and VOD content 
    * Adaptive bit rate (ABR) logic and initial set up of ABR controls 
    * Live manifest failover support 
    * Adjustable playback buffers 
    * 302 redirect optimization 
    * Fragment duration, size, and time-to-download tracking support

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
    * Session cookie and media auth cookie support 
    * Multiple-domain token packaging

* Video and ad tracking

    * QoS event tracking 
    * Notifications that help TVSDK and your application to communicate asynchronously about the status of videos, advertisements, and other elements, and also that log activity.
    * Integration with Adobe Analytics and heartbeat support

* Logging

    * Debug logging.
    * Tracking support for fragment duration, size, and time-to-download.
