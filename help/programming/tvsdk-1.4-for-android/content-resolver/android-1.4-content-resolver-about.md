---
description: An opportunity detector is a TVSDK component that detects custom tags in a stream and identifies placement opportunities. These opportunities are sent to the content resolver, which customizes the content/ad insertion workflow based on the placement opportunity properties and metadata.
title: Opportunity generators and content resolvers
exl-id: e396eaa9-444d-4173-a534-74b29309a151
---
# Opportunity generators and content resolvers {#opportunity-generators-and-content-resolvers}

An opportunity detector is a TVSDK component that detects custom tags in a stream and identifies placement opportunities. These opportunities are sent to the content resolver, which customizes the content/ad insertion workflow based on the placement opportunity properties and metadata.

 TVSDK includes  a default opportunity detector:

* `SpliceOutPlacementOpportunityDetector`, which understands default ad cues

TVSDK also includes default content resolvers that provide content to be inserted based on the metadata key in the player item:

* `AuditudeResolver` for `AUDITUDE_METADATA_KEY`, which is capable of communicating with Adobe Primetime ad decisioning (previously known as Auditude) servers and returning ad breaks to be placed. 

* `MetadataResolver` for `JSON_METADATA_KEY` 

* `CustomAdMarkersContentResolver` for `TIME_RANGES_METADATA_KEY`

You can override the default opportunity detectors and content resolvers to customize the advertising workflow in the following ways:

* Add support for custom tag detection 
* Recognize custom tags for ad insertion 
* Create a customized ad provider 
* Black out content

TVSDK provides default opportunity generators and content resolvers that place ads in the timeline, and these generators and resolvers are based on nonstandard tags in the manifest. Your application might need to alter the timeline based on opportunities that are identified in the manifest, such as indicators for a blackout period.

An *`opportunity`* represents a point of interest on the timeline that usually indicates an ad placement opportunity. This opportunity can also indicate a custom operation that might affect the timeline, such as a blackout period. An *`opportunity generator`* identifies specific opportunities (tags) in the timeline and notifies TVSDK that these opportunities have been tagged. Opportunities are identified in a timeline in by including a nonstandard (non-HLS) tag.

When your application is notified about an opportunity (tag), your application might alter the timeline by, for example, inserting a series of ads, by switching to an alternate stream (blackouts) or by otherwise editing the timeline content. By default, TVSDK calls the appropriate *`content resolver`* to implement the required timeline changes or actions. Your application can use the default TVSDK advertisement content resolver or register its own content resolver.

You can also use `MediaPlayerItemConfig.setAdTags` to add more ad marker tags/cues so that TVSDK can recognize and use `MediaPlayerItemConfig.subscribedTags` and notify your application about additional tags that might have advertising workflow information.

One possible use of a custom resolver is for blackout periods. To handle these periods, your application could implement and register a blackout opportunity detector that is responsible for handling blackout tags. When TVSDK encounters this tag, it polls all the registered content resolvers to find the first one that handles the specified tag. In this example, it is the blackout content resolver, which can, for example, replace the current item with alternate content on the player for the duration that is specified by the tag.
