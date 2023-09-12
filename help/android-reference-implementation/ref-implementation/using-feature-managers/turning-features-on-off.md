---
description: You can turn features on or off without going through the code by using the manager factory.
title: Turning features on or off using ManagerFactory
exl-id: 4e288a6e-80e5-43c1-aba2-374723dd9957
---
# Turning features on or off using ManagerFactory{#turning-features-on-or-off-using-managerfactory}

You can turn features on or off without going through the code by using the manager factory.

The enablement argument in the example below determines whether the feature is used or not. If it is false, the feature manager is created but provides just the default functionality to the player, as if the feature manager were not created. If it is true, the feature manager is created, the feature is enabled, and the media player accepts input from the configuration file.

For example, in the `com.adobe.primetime.reference.ui.player.PlayerFragment.java` file:

```java
adsManager = ManagerFactory.getAdsManager( 
<b>true</b>, config, mediaPlayer);

```

**API documentation**: [ManagerFactory](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/ManagerFactory.html)
