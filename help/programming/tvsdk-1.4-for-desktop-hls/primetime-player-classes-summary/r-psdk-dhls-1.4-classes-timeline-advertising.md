---
description: These classes provide information about ads that occur within a timeline.
title: Timeline advertising classes
exl-id: 2ac1f6b7-48b2-4d9c-b39d-a7e6f1ff2ac5
---
# Timeline advertising classes {#timeline-advertising-classes}

These classes provide information about ads that occur within a timeline.

 Package: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/package-detail.html)
 Package: [com.adobe.mediacore.timeline.advertising.policy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/package-detail.html) 

|  Name  | Description  |
|---|---|
| [Ad](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/Ad.html)  |Class that defines the Ad abstraction and holds all ad information. It is defined by a unique ID, a duration, and a `MediaResource`. The `MediaResource` contains the URL where the actual ad content resides.  |
| [AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html)  | Class that represents an asset to be displayed. Class representing an ad asset.  |
| [AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html)  | Class that gives a unified view on several ads that will be played at some point during playback.  |
| [AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakPolicy.html)  | Enumeration that defines the ad playback policy related to the user bypassing ads while seeking.  |
| [AdBreakTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdBreakTimelineItem.html)  | Timeline item associated with the specific ad break.  |
| [AdBreakWatchedPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdBreakWatchedPolicy.html)  | Enumeration class for possible policies on when to mark an ad break as having been watched.  |
| [AdClick](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html)  | Class that represents a click instance associated with an asset. This instance contains information about the click-through URL and the title that can be used to provide additional information to the user.  |
| [AdPolicy](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicy.html)  | Enumeration class for possible policies on where to resume playing an ad break after seeking or trick-play mode.  |
| [AdPolicyMode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicyMode.html)  | Enumeration class that lists ways in which the player is playing, such as seeking or normal play.  |
|  [AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html)  |Interface that defines properties for `AdPolicySelector` API calls. These properties provide the context for enforcing each ad behavior.  |
|  [AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/policy/AdPolicySelector.html)  | An ad policy selector interface for enforcing ad behaviors. Applications can conform to this interface by implementing all the required methods or by extending the existing default policy selector class to customize specific behaviors.  |
| [AdTimelineItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdTimelineItem.html)  | Timeline item associated with a specific ad.  |
|[AuditudeAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AuditudeAdResolver.html)  | Class that handles primetime ad resolving in the TVSDK process.  |
| [AdType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/AdType.html)  | Enumeration of all ad types supported by the TVSDK.  |
| [MetadataAdResolver](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/advertising/MetadataAdResolver.html)  | Class.  |
