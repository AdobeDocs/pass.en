---
description: A MediaResource represents the content that is about to be loaded by the MediaPlayer instance.
title: MediaPlayer and MediaResource classes
exl-id: d3ac1a8d-3549-417a-83e9-c561a3d12127
---
# MediaPlayer and MediaResource classes{#mediaplayer-and-mediaresource-classes}

A MediaResource represents the content that is about to be loaded by the MediaPlayer instance.

<!--<a id="section_B09A012C97454AF58CE2269B800D8027"></a>-->

The TVSDK library provides a simple means to load and prepare content for playback by using the `replaceCurrentItem` method in the MediaPlayer interface. This method receives an instance of the MediaResource class as the sole input argument. The MediaResource class is composed of the following information:

* A URL, which represents the location of the content that is about to be loaded. 
* A type, which is the type of content that is about to be loaded.

  This is a simple enumeration in the `MediaResource` class that defines the types of content that can be loaded by the MediaPlayer. Possible values are HLS and HDS. Each value is associated with the string representing the file extensions commonly used, `m3u8` for HLS and `f4m` for HDS. 
* Some metadata, which is an instance of the `Metadata` class.

  This dictionary-like structure might contain additional information about the content that is about to be loaded, such as information about the alternate/ad content that should be placed in the main content.

The metadata is the medium through which information that is related to alternate content is passed to TVSDK. The `Metadata` interface defines the API for a generic key-value store, where both the key and the value are plain strings.
