---
description: The feature managers serve as wrappers around the TVSDK library.
title: Reference implementation structure
exl-id: cf102ccc-2e31-4197-a321-e485f77ba754
---
# Reference implementation structure {#reference-implementation-structure}

The feature managers serve as wrappers around the TVSDK library.

 In Java, classes are structured in a hierarchy. For example, all the UI-related code under `com.adobe.primetime.reference.ui` and all the feature managers are under `com.adobe.primetime.reference.manager`.

The Primetime reference implementation contains the following packages:  

|Package|Description|
|--- |--- |
|[com.adobe.primetime.reference](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/PrimetimeReference.html)|This class extends  android.app.Application.|
|[com.adobe.primetime.reference.advertising](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/advertising/package-summary.html)|Contains code for custom ads.|
|[com.adobe.primetime.reference.config](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)|Contains the interface code required for configuring the feature managers.|
|[com.adobe.primetime.reference.drm](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/drm/package-summary.html)|Contains helper classes for DRM.|
|[com.adobe.primetime.reference.feeds](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/feeds/package-summary.html)|The adapters and item adapters for interface, platform, and reference information. Also includes the  FeedAdapterFactory,  ContentRenditionInfo, and  XMLParserHelper code.|
|[com.adobe.primetime.reference.logging](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/logging/package-summary.html)|Provides classes for logging locally and remotely.|
|[com.adobe.primetime.reference.manager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/package-summary.html)|This is where you can find the feature managers as well as the  ManagerFactory. For optional features that you can enable or disable, there are two feature managers: <ul><li>One feature manager that is the name of the feature, for example,  CCManager. This feature manager is turned off and provides the default off behavior.</li><li>One feature manager that has On appended to the feature manager name, for example,  CCManagerOn. This feature manager provides sample code for the enabled feature.</li></ul>|
|[com.adobe.primetime.reference.ui.catalog](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/catalog/package-summary.html)|Contains UI code for the catalog.|
|[com.adobe.primetime.reference.ui.log](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/log/package-summary.html)|Contains UI code for the log.|
|[com.adobe.primetime.reference.ui.player](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/package-summary.html)|Contains UI code for the player.|
|[com.adobe.primetime.reference.ui.settings](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/settings/package-summary.html)|Contains UI code for settings.|
|[com.adobe.primetime.reference.utils](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/package-summary.html)|Contains general utility classes.|
|[com.adobe.primetime.reference.utils.http](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/utils/http/package-summary.html)|Contains `HTTP-specific` utility classes.|
