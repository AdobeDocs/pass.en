---
description: New APIs have been introduced that will instruct TVSDK to ignore network connectivity state when downloading manifests. 
title: Offline Playback with Android
exl-id: 9ac50d3e-5839-4eb9-8811-efde56cfe375
---
# Offline Playback with Android {#offline-playback-with-android}

The following APIs have been introduced that will instruct TVSDK to ignore network connectivity state when downloading manifests. Network connectivity state is generally used during Adaptive Bitrate streaming (ABR), to determine whether to attempt a fallback or wait for the network to resume.

```
NetworkConfiguration::setOfflinePlayback(boolean)
boolean NetworkConfiguration::getOfflinePlayback()
```

You can enable this setting and ignore the network connectivity.

Set `com.adobe.mediacore.system.NetworkConfiguration::setOfflinePlayback` to true. The default value for a boolean is false.

```
// example of NetworkConfiguration
// wherever you currently set up MediaResource and MediaPlayerItemConfig
NetworkConfiguration networkConfig = mediaPlayerItemConfig.getNetworkConfiguration();
networkConfig.setOfflinePlayback(true);
mediaPlayerItemConfig.setNetworkConfiguration(networkConfig);
```
