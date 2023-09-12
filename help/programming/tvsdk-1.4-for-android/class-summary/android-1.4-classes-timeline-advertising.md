---
description: These classes provide information about ads that occur within a timeline.
title: Timeline advertising classes
exl-id: fb31a235-6578-4da1-b732-713a2f9b24be
---
# Timeline advertising classes{#timeline-advertising-classes}

These classes provide information about ads that occur within a timeline.

Package: [com.adobe.mediacore.timeline.advertising](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/package-summary.html)

Package: [com.adobe.mediacore.timeline.advertising.auditude](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/package-summary.html)

| Name | Description |
|--- |--- |
|[Ad](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/Ad.html)|Class that defines the Ad abstraction and holds all ad information. It is defined by a unique ID, a duration, and a `MediaResource`. The `MediaResource` contains the URL where the actual ad content resides.|
|[AdAsset](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdAsset.html)|Class that represents an asset to be displayed. Class representing an ad asset.|
|[AdBreak](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreak.html)|Class that gives a unified view on several ads that will be played at some point during playback.|
|[AdBreakPlacement](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPlacement.html)|Ad break placement operation class.|
|[AdBreakPolicy](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdBreakPolicy.html)|Enumeration that defines the ad playback policy related to the user bypassing ads while seeking.|
|[AdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdClick.html)|Class that represents a click instance associated with an asset. This instance contains information about the click-through URL and the title that can be used to provide additional information to the user.|
[AdPolicyInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicyInfo.html)|Interface that defines properties for AdPolicySelector API calls. These properties provide the context for enforcing each ad behavior.|
|[AdPolicySelector](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/AdPolicySelector.html)|An ad policy selector interface for enforcing ad behaviors. Applications can conform to this interface by implementing all the required methods or by extending the existing default policy selector class to customize specific behaviors.|
|`auditude.AuditudeAdProvider`|Deprecated. Use AuditudeResolver.|
|[AuditudeResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeResolver.html)|Class that handles primetime ad resolving in the Phrase process.|
|[AuditudeTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/auditude/AuditudeTracker.html)|Class that implements the ContentTracker interface and defines Primetime ad-tracking events.|
|[ContentResolver](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentResolver.html)|Class that handles the ad-resolving part in the Phrase process.|
|[ContentTracker](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/ContentTracker.html)|Interface that defines the protocol that you must implement if you want to create an ad-tracking module that is designed to integrate with the library or a custom ad tracker. This interface requires that you define the way ad-progress events are reported to the remote ad-tracking system.|
|[PlacementInformation](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/advertising/PlacementInformation.html)|Class that abstracts a placement information request. Each resolved ad must have one placement information attached to it. The placement information describes where the ad is intended to be placed on the timeline. It contains information such as: <ul><li>Placement position (in ms) </li><li>Type of the placement (pre-roll, mid-roll, or post-roll) </li><li>Duration of the main content chunk that is about to be replaced</li></ul>|
