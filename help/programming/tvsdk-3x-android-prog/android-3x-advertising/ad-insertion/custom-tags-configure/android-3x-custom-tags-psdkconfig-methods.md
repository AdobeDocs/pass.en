---
description: You can globally configure custom tag names in TVSDK with the MediaPlayerItemConfig class.
title: Config class methods for tags
exl-id: 0a07ebdf-7336-4d4d-b7df-294afb3fd606
---
# Config class methods for tags {#config-class-methods-for-tags}

You can globally configure custom tag names in TVSDK with the MediaPlayerItemConfig class.

TVSDK automatically applies the global configuration to any media stream that does not specify a stream-specific configuration.

`MediaPlayerItemConfig` exposes these methods to manage the custom tags:  

**Subscribe to specific custom tags**

|<b>Method</b>|<b>Description</b>|
|--- |--- |
|`public final String[] getSubscribedTags`|Retrieves the current list of subscribed tags.|
|`public final void setSubscribedTags(String[] tags);`|Sets the list of subscribed tags that will be exposed to the application.  Your application is also automatically subscribed to all tags transmitted through `setAdTags`.|

**Customize the ad tags used by the default opportunity detector**

|<b>Method</b>|<b>Description</b>|
|--- |--- |
|`public final String[] getAdTags;`|Retrieves the current list of ad tags.|
|`public final void setAdTags(String[] tags);`|Sets the list of ad tags that will be used by default opportunity generator.|

Remember the following:

* The setter methods do not allow the tags parameter to contain null values.

  If encountered, TVSDK throws an `IllegalArgumentException`. 
* The custom tag name must contain the `#` prefix.

  For example, `#EXT-X-ASSET` is a correct custom tag name, but `EXT-X-ASSET` is incorrect. 

* You cannot change the configuration after the media stream has been loaded.
