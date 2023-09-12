---
description: An opportunity detector is a Browser TVSDK component that detects custom tags in a stream and identifies placement opportunities. These opportunities are sent to the content resolver, which customizes the content/ad insertion workflow based on the placement opportunity properties and metadata.
title: Customize opportunity detectors and content resolvers
exl-id: 1866ed53-acfc-45d3-941e-0ed171aa038b
---
# Overview {#customize-opportunity-detectors-and-content-resolvers-overview}

An opportunity detector is a Browser TVSDK component that detects custom tags in a stream and identifies placement opportunities. These opportunities are sent to the content resolver, which customizes the content/ad insertion workflow based on the placement opportunity properties and metadata.

Browser TVSDK includes the following default opportunity detectors:

* `AdSignalingModeOpportunityGenerator`, which creates initial ad placement opportunities based on the ad signaling mode. 
* `ManifestCuesOpportunityGenerator`, which creates ad placement opportunities from any splice-out tag.

Browser TVSDK also includes default content resolvers, such as `AuditudeResolver`, that provides content that will be inserted based on the metadata key in the player item. `AuditudeResolver` is capable of communicating with Adobe Primetime ad decisioning servers and returning ad breaks to be placed.

You can override the default opportunity detectors and content resolvers to customize the advertising workflow in the following ways:

* Add support for custom tag detection 
* Recognize custom tags for ad insertion 
* Create a customized ad provider
