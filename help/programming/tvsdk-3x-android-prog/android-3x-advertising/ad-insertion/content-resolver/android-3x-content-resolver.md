---
description: An opportunity generator identifies placement opportunities by custom tags in a stream, ad signaling mode custom markers, and so on. The opportunity generator sends these placement opportunities to the content resolver, which customizes the content/ad insertion workflow based on the placement opportunity's properties and metadata.
title: Customize opportunity generators and content resolvers
exl-id: 5d0ebaa6-4708-4602-b9d7-882c389fb030
---
# Overview {#customize-opportunity-generators-and-content-resolvers-overview}

An opportunity generator identifies placement opportunities by custom tags in a stream, ad signaling mode custom markers, and so on. The opportunity generator sends these placement opportunities to the content resolver, which customizes the content/ad insertion workflow based on the placement opportunity's properties and metadata.

 TVSDK includes the following default opportunity generators:

* `ManifestCuesOpportunityGenerator` generates opportunities from the default ad cues ( `#EXT-X-CUE`). 

* `AdSignalingModeOpportunityGenerator` generates an initial opportunity for the specified ad signaling mode. This ignores any cues or timed metadata information. 
* `CustomMarkerOpportunityGenerator` generates opportunities to replace baked-in C3 ads. 
* `AuditudeResolver`'s opportunity generator produces opportunities when lazy ad resolving is on.

TVSDK also includes default content resolvers:

* `CustomRangeResolver` 
* `JSONResolver` 
* `AuditudeResolver`, which can communicate with Primetime ad decisioning.

You can override the default opportunity generators and content resolvers to customize the advertising workflow in ways such as the following:

* Recognize custom tags for ad insertion. For more information, see [Customize opportunity generators and content resolvers](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md).
* Create a customized ad provider.
* Black out content.
