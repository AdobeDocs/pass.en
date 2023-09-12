---
description: You can use the Primetime Player Objective-C API to customize the behavior of the player.
title: Media player classes
exl-id: b58efff0-2455-4db5-93a0-4624291dc526
---
# Media player classes {#media-player-classes}

You can use the Primetime Player Objective-C API to customize the behavior of the player.

These classes describe your media player and its resources.

| Class | Description |
|---|---|
| PTABRControlParameters | Encapsulates all adaptive bit-rate control parameters. Supported parameters are:<ul><li>minBitRate</li><li>maxBitRate</li><li>initialBitRate</li></ul> |
| PTDefaultMediaPlayerClientFactory | Default implementation of PTMediaPlayerClientFactoryin the TVSDK. It provides the availablePTOpportunityResolver, PTContentResolver, andPTAdPolicySelector instances. |
| PTMediaPlayer | Defines the root component for the Primetime Player framework.Applications create an instance of this class to play back a media. This component dispatches notifications to let your application know the status of the player at any given time. |
| PTMediaPlayerClientFactory | Protocol that describes the methods that a custom media player client factory should implement to provide the available PTOpportunityResolver ,PTContentResolver and PTAdPolicySelector instances. |
| PTMediaPlayerItem | Represents a specific audio-video media. |
| PTMediaPlayerView | Manages the view component of the Primetime Player framework. |
| PTMediaProfile | Represents the profile of a single stream in the variant playlist. |
| PTMediaSelectionOption | Represents an audiovisual media resource to accommodate different language preferences, accessibility requirements, or custom application configurations. Valid option types:<ul><li>Subtitles (PTMediaSelectionOptionTypeSubtitle)</li><li>Alternate audio (PTMediaSelectionOptionTypeAudio)</li><li>Closed captions (PTMediaSelectionOptionTypeCC)</li><li>Undefined (PTMediaSelectionOptionTypeUndefined)</li></ul> |
| PTOpportunityResolver class,PTOpportunityResolver protocol | Class used for processing in-manifest cues that will be used as placements for the Adobe Primetime ad decisioning process. |
| PTOpportunityResolverDelegate | Protocol that describes the methods that the custom opportunity resolver ( PTOpportunityResolver ) should use to communicate to the delegate the status of the resolving of the opportunity. |
| PTSDK | Describes the version of the TVSDK and its capabilities. |
| PTSDKConfig | Exposes TVSDK global settings and allows an application to subscribe to custom HLS tags. |
| PTTextStyleRule | Defines constants that represent text style attribute keys that form the dictionary of rules. |
