---
description: A MediaResource represents the content that is about to be loaded by the MediaPlayer instance.
title: MediaPlayer and MediaResource classes
exl-id: c4219dff-de75-4b8a-ad33-e0a721c38de7
---
# MediaPlayer and MediaResource classes {#mediaplayer-and-mediaresource-classes}

A MediaResource represents the content that is about to be loaded by the MediaPlayer instance.

<!--<a id="section_431AB7221E0249BF949EC72EEB9B428A"></a>-->

TVSDK provides the means to load and prepare content for playback by using the `replaceCurrentResource` method in `MediaPlayer`. This method takes two arguments, an instance of `MediaPlayerResource` and, optionally, an instance of `MediaPlayerItemConfig`, which you can use to pass application-defined custom parameters.

* For more details see  mediaplayer-reuse-or-remove . 
* For details of `MediaPlayerResource`, see  media-resource-create
