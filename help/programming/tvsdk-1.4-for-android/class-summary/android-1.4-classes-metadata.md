---
description: These classes provide metadata for advertising, namespaces, and tracking.
title: Metadata classes
exl-id: 3d98c5e1-6792-419b-9638-f156f1eafd1b
---
# Metadata classes{#metadata-classes}

These classes provide metadata for advertising, namespaces, and tracking.

 Package: [com.adobe.mediacore.metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/package-summary.html) 

|  Name  | Description  |
|---|---|
| [AdvertisingMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html) | Class that provides properties that should be configured for resolving ads for a given media item. All the required properties must be set to configure the player for successfully resolving ads.  |
| AuditudeMetadata  | Deprecated. Use AuditudeSettings.  |
| [AuditudeSettings](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/AuditudeSettings.html)  |Class that extends Java `AdvertisingMetadata` specifically for  Phrase. Provides properties to be configured for resolving  Phrase ads for a given media item. You must set all the required properties, including zone ID, media ID, and ad server URL, to configure the player for successfully resolving ads.  |
| [Metadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/Metadata.html) | Defines the generic interface for configuring all available metadata for your player and additional objects. |
| [MetadataNode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/MetadataNode.html) | Generic data-structure-like class for storing arbitrary key-value pairs.  |
| [TimedMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html) | Class for the raw representation of the timed metadata inserted into a media stream. |
