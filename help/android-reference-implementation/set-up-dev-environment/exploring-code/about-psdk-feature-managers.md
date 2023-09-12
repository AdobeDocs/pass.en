---
title: Feature managers
description: Feature managers provide a way for you to control individual features without traversing the entire TVSDK in search of code for one feature that could be scattered in multiple locations.
exl-id: dbf2dc8b-6067-4d94-9c3c-553452b7ffd9
---
# Feature managers {#feature-managers}

Feature managers provide a way for you to control individual features without traversing the entire TVSDK in search of code for one feature that could be scattered in multiple locations. Feature managers condense code into one class per feature. The feature managers wait for triggers from TVSDK events and then inform the class that uses the feature manager to handle the result. The feature manager provides the required information to the class.

The feature managers perform the following tasks:

* **Triggers TVSDK features.**
  These are function calls to trigger a TVSDK feature. For example, `PlaybackManager.play()` is called when the player application needs to start the video playback. 

* **Listens to TVSDK events.**
  The feature manager needs to listen to TVSDK events to acquire information from the TVSDK. For example, `AdsManager` listens to TVSDK Ads events to be notified when ad breaks start. 

* **Dispatches events to the handler.**
  After the feature managers receive and process the events from the TVSDK, they notify the client side to handle the event. For example, after `AdsManager` receives an ad break start event, it tells the player fragment to reflect this change in the UI (disable the scrub bar, show the ad overlay, etc.).

The Primetime reference implementation includes the following feature managers:  

|  Feature manager  | Default file  | Feature  |  |
|---|---|---|---|
| Video playback | PlaybackManager  | HLS playback and control, DVR playback and control, buffer control, and multi-bit rate handling.  | Required  |
| DRM content protection  | DrmManager  | Content protection.  | Required  |
| Ad insertion  | AdsManager  | Ad insertion, including Adobe Primetime ad decisioning direct ad break, and custom ad break.  | Optional  |
| Closed captions  | CCManager  | Closed captioning and VTT subtitles.  | Optional  |
| Late-binding audio  | AAManager  | Late binding audio.  | Optional  |
| QoS  | QosManager  | QoS statistics.  | Optional  |
|  Entitlement  | EntitlementManager  | Primetime authentication entitlement integration.  | Optional  |

The reference implementation contains basic default classes, listed above, and corresponding classes with the suffix of On. The default classes provide the default TVSDK behaviors while the classes with the On suffix include all the code required to trigger the TVSDK feature and listen to TVSDK events for that feature.

* For optional features, the default code operates as if the feature is turned off. 
* Classes with the On suffix operate as if the feature is turned on.
