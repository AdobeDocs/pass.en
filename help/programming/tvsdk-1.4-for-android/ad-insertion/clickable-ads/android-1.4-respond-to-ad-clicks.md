---
description: When a user clicks on an ad or a related button, your application must respond. TVSDK provides you with information about the destination URL for the click.
title: Respond to clicks on ads
exl-id: dc1f1ad7-2f11-4a6c-8459-e02cf8a2e0aa
---
# Respond to clicks on ads{#respond-to-clicks-on-ads}

When a user clicks on an ad or a related button, your application must respond. TVSDK provides you with information about the destination URL for the click.

1. To set up an event listener for TVSDK, and provide the click-through information, register an `AdClickedEventListener.onAdClicked`.

   When a user clicks on an ad or a related button, TVSDK dispatches this notification, including information about the destination for the click.
1. Monitor user interactions on clickable ads.
1. When the user touches or clicks the ad or button, to notify TVSDK, call `notifyClick` on the `MediaPlayerView`.
1. Listen for the `onAdClick(AdClickEvent event)` event from TVSDK.
1. To retrieve the click-through URL and related information, use the getter methods for the `AdClickEvent` instance.
1. Pause the video.

   For more information about pausing the video, see [Pause and resume playback.](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md).
1. Use the click-through information to display the ad click-through URL and the related information.

       You could, for example, display the information in one of the following ways:

    * In your application by opening the click-through URL in a browser.

      On desktop platforms, the video ad playback area is used to invoke click-through URLs at user clicks. 
    * Redirect users to their external mobile web browser.

      On mobile devices, the video ad playback area is used for other functions, such as hiding and showing controls, pausing playback, expanding to full screen, and so on. On these devices, a separate view, such as a sponsor button, is used to launch the click-through URL.

1. Close the browser window in which the click-through information is displayed and resume playing the video.

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

For example: 

```java
private AdStartedEventListener adStartedEventListener = new AdStartedEventListener() { 
    @Override 
    public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        if (ad == null) { 
            return; 
        } 
 
        _pubOverlay.startAd(adPlaybackEvent.getAdBreak(), ad); 
 
        if (areClickableAdsEnabled() && ad.isClickable()) { 
            _isClickableAdPlaying = true; 
            _playerClickableAdFragment.show(); 
        } 
 
    } 
}; 
 
private AdCompletedEventListener adCompletedEventListener = new AdCompletedEventListener() { 
    @Override 
    public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        _pubOverlay.stopAd(adPlaybackEvent.getAdBreak(), ad); 
 
        _isClickableAdPlaying = false; 
        if (ad.isClickable()) { 
            _playerClickableAdFragment.hide(); 
        } 
    } 
}; 
 
private AdClickedEventListener adClickedEventListener = new AdClickedEventListener() { 
    @Override 
    public void onAdClicked(AdClickEvent adClickEvent) { 
        AdClick adClick = adClickEvent.getAdClick(); 
        Ad ad = adClickEvent.getAd(); 
 
        String url = adClick.getUrl(); 
        if (url == null || url.trim().equals("")) { 
        } else { 
            Uri uri = Uri.parse(url); 
            Intent intent = new Intent(ACTION_VIEW, uri); 
            try { 
                startActivity(intent); 
            } catch (Exception e) { 
            } 
        } 
 
    } 
}; 

```
