---
description: When an entire playlist is missing, for example, when the M3U8 file specified in a top-level manifest file does not download, TVSDK attempts to recover. If it cannot recover, your application determines the next step.
title: Missing playlist failover
exl-id: aab2dde3-aee2-4ade-b8f9-91c72df0c747
---
# Missing playlist failover{#missing-playlist-failover}

When an entire playlist is missing, for example, when the M3U8 file specified in a top-level manifest file does not download, TVSDK attempts to recover. If it cannot recover, your application determines the next step.

If the playlist that is associated with the middle-resolution bit rate is missing, TVSDK searches for a variant playlist at the same resolution. If it finds the same resolution, it starts downloading the variant playlist and the segments from the matching position. If TVSDK does not find the same resolution playlist, it will try to cycle through other bitrate playlists and their variants. An immediately lower bitrate is the first choice, then its variant, and so on. If all of the lower bitrate playlists and their variants are exhausted in the attempt to find a valid playlist, TVSDK will go to the top bitrate and count down from there. If a valid playlist cannot be found, the process fails, and the player moves to the ERROR state.

Your application can determine how to handle this situation. For example, you might want to close the player activity and direct the user to the catalog activity. The event of interest is the `STATE_CHANGED` event, and the corresponding callback is the `onStateChanged` method. Here is code that monitors whether the player changes its internal state to ERROR:

```java
case ERROR: 
    getActivity().finish(); // this is where we close the current activity (the Player activity) 
    break;
```

For more information, see the [!DNL PlayerFragment.java] file in your SDK: 

```
[…]/samples/PrimetimeReference/src/PrimetimeReference/src/com/adobe/primetime/reference/ui/player/
```

If the client side network is down, you can use this code to verify.

```
psdkutils::PSDKString 
getNetworkDownVerificationUrl() const { return 
_networkDownVerificationUrl; }
```

API will provide the url that is used to verify if the client side network is down. This should be a valid url, which returns http response code 200 on http requests.

```
psdkutils::PSDKErrorCode 
 setNetworkDownVerificationUrl(psdkutils::PSDKString value) {  
_networkDownVerificationUrl = value; return psdkutils::kECSuccess; }
```

If setNetworkDownVerificationUrl is not set, TVSDK uses the MainManifest url by default to figure if the network is down.
