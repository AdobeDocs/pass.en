---
description: TVSDK provides default opportunity generators and content resolvers that place ads in the timeline, and these generators and resolvers are based on nonstandard tags in the manifest. Your application might need to alter the timeline based on opportunities that are identified in the manifest, such as indicators for a blackout period.
title: Opportunity generators and content resolvers
exl-id: 7d31067c-a6da-4c4f-ab77-4a1358ac0323
---
# Opportunity generators and content resolvers {#opportunity-generators-and-content-resolvers}

TVSDK provides default opportunity generators and content resolvers that place ads in the timeline, and these generators and resolvers are based on nonstandard tags in the manifest. Your application might need to alter the timeline based on opportunities that are identified in the manifest, such as indicators for a blackout period.

An *`opportunity`* represents a point of interest on the timeline that usually indicates an ad placement opportunity. This opportunity can also indicate a custom operation that might affect the timeline, such as a blackout period. An *`opportunity generator`* identifies specific opportunities (tags) in the timeline and notifies TVSDK that these opportunities have been tagged. Opportunities are identified in a timeline in by including a nonstandard (non-HLS) tag.

When your application is notified about an opportunity, your application might alter the timeline by inserting a series of ads, by switching to an alternate stream (blackouts), or by otherwise editing the timeline content. By default, TVSDK calls the appropriate *`content resolver`* to implement the required timeline changes or actions. Your application can use the default TVSDK advertisement content resolver or register its own content resolver.

You can also use `MediaPlayerItemConfig.setAdTags` to add more ad marker tags/cues so that TVSDK can recognize and use `MediaPlayerItemConfig.subscribedTags` and notify your application about additional tags that might have advertising workflow information.

One possible use of a custom resolver is for blackout periods. To handle these periods, your application could implement and register a blackout opportunity detector that is responsible for handling blackout tags. When TVSDK encounters this tag, it polls all the registered content resolvers to find the first one that handles the specified tag. In this example, it is the blackout content resolver, which can, for example, replace the current item with alternate content on the player for the duration that is specified by the tag.
