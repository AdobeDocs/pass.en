---
description: Browser TVSDK provides default opportunity generators and content resolvers that place ads in the timeline, and these generators and resolvers are based on nonstandard tags in the manifest. Your application might need to alter the timeline based on opportunities that are identified in the manifest.
title: Opportunity generators and content resolvers
exl-id: a47acd22-8b1b-4c66-a7eb-a4d99afb5f17
---
# Opportunity generators and content resolvers{#opportunity-generators-and-content-resolvers}

Browser TVSDK provides default opportunity generators and content resolvers that place ads in the timeline, and these generators and resolvers are based on nonstandard tags in the manifest. Your application might need to alter the timeline based on opportunities that are identified in the manifest.

An *`opportunity`* represents a point of interest on the timeline that usually indicates an ad placement opportunity. This opportunity can also indicate a custom operation that might affect the timeline. An *`opportunity generator`* identifies specific opportunities (tags) in the timeline and notifies TVSDK that these opportunities have been tagged.

Opportunities are identified in a timeline in `TimedMetata`. The `ManifestCuesOpportunityGenerator` creates opportunities based on the `TimedMetadata` objects that are created for each splice-out ad tag (in `MediaPlayerItemConfig.adTags`) that has been detected in the manifest. The `AdSignalingModeOpportunityGenerator` creates the initial opportunity that is based on the `MediaPlayerItem` type and its associated ad signaling mode.

>[!TIP]
>
>If the `AdvertisingMetadata.livePreroll` or the `AdvertisingMetadata.preroll` property is set, `AdSignalingModeOpportunityGenerator` generates a pre-roll opportunity for live streams.

When your application is notified about an opportunity (tag), your application might alter the timeline by, for example, inserting a series of ads. By default, Browser TVSDK calls the appropriate *`content resolver`* to implement the required timeline changes or actions. Your application can use the default Browser TVSDK advertisement content resolver or register its own content resolver.

You can also use `MediaPlayerItemConfig.adTags` to add more ad marker tags/cues for the default `ManifestCuesOpportunityGenerator` class and use `MediaPlayerItemConfig.subscribedTags` so that TVSDK can notify your application about additional tags that might have advertising workflow information..

>[!TIP]
>
>The default values of `MediaPlayerItemConfig.adTags` and `MediaPlayerItemConfig.subscribeTags` is `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.
