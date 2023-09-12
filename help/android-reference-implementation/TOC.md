---
product: primetime
audience: end-user
user-guide-title: Primetime Reference Implementation Help
user-guide-description: Helps understand the TVSDK and modify the feature managers to customize your personal player.
---

# PSDK 1.4 for Android Reference Implementation {#reference-implementation}

+ [Android Reference Implementation Overview](home.md)
+ Primetime reference implementation {#reference}
   + [How to use the Primetime reference implementation](ref-implementation/how-to-use-ref-player.md)
   + [Reference implementation structure](ref-implementation/ref-player-structure.md)
   + How to use feature managers {#feature-managers}
      + [How to use feature managers](ref-implementation/using-feature-managers/how-to-use-feature-managers.md)
      + [Creating feature managers by passing configuration information to the MediaPlayer...](ref-implementation/using-feature-managers/creating-feature-managers.md)
      + [Turning features on or off using ManagerFactory](ref-implementation/using-feature-managers/turning-features-on-off.md)
      + [Handling events](ref-implementation/using-feature-managers/handling-events.md)
   + Set up your development environment {#setup-dev}
      + [Set up your development environment](set-up-dev-environment/set-up-dev-environment-overview.md)
      + [Download and configure prerequisite software](set-up-dev-environment/download-prereqs-android.md)
      + [Build the Primetime reference implementation](set-up-dev-environment/install-the-ref-player-project.md)
   + Explore the code {#explore-code}
      + [PlayerFragment](set-up-dev-environment/exploring-code/player-fragment.md)
      + [Feature managers](set-up-dev-environment/exploring-code/about-psdk-feature-managers.md)
      + [ConfigProvider](set-up-dev-environment/exploring-code/config-provider.md)
      + [SettingsActivity](set-up-dev-environment/exploring-code/settings-activity.md)
      + [Catalog format](set-up-dev-environment/exploring-code/catalog-format.md)
      + [JSON object for Primetime ads](set-up-dev-environment/exploring-code/json-pt-ads.md)
      + [JSON object for direct ad breaks](set-up-dev-environment/exploring-code/json-direct-ad-breaks.md)
      + [JSON object for custom ad markers](set-up-dev-environment/exploring-code/json-custom-ad-markers.md)
      + [JSON object for entitlement resource ID](set-up-dev-environment/exploring-code/json-entitlement-resource-id.md)
      + [Example JSON feed format](set-up-dev-environment/exploring-code/example-json-feed-format.md)
   + Implement video playback {#implement-video}
      + [Essential operations of video playback](implement-video-playback/video-playback.md)
      + [Enable video playback](implement-video-playback/enable-video-playback.md)
      + [DRM content protection](implement-video-playback/content-protection.md)
   + [Multiple bit rates](implement-video-playback/mbr.md)
   + Set up a player for DVR playback with ads {#dvr}
     + [DVR without ad insertion](implement-video-playback/dvr/dvr-without-ad-insertion.md)
     + [DVR with ad insertion](implement-video-playback/dvr/dvr-with-ad-insertion.md)
     + [Choosing a custom starting point for DVR](implement-video-playback/dvr/dvr-custom-start-point.md)
     + [Set a custom start time in the reference implementation](implement-video-playback/dvr/set-custom-start-time-dvr.md)
   + [Display QoS playback and device statistics](implement-video-playback/qos-statistics.md)
   + Insert ads {#insert-ads}
     + [Ad insertion](insert-ads/ad-insertion.md)
     + [Ad insertion types](insert-ads/ad-insertion-types.md)
     + [Add advertising](insert-ads/add-advertising.md)
     + [Related API documentation](insert-ads/aps-callbacks-ad-insertion.md)
   + Late-binding audio {#late-binding-audio}
     + [Overview](late-binding-audio/late-binding-audio-overview.md)
     + [Integrate late-binding audio](late-binding-audio/aa-enable.md)
     + [Select the audio tracks](late-binding-audio/select-audio-tracks.md)
     + [Related API documentation](late-binding-audio/aa-api-callbacks.md)
   + Primetime authentication entitlement flows {#primetime-authentications}
     + [Overview](paytvpass-entitlement/paytvpass-entitlement-overview.md)
     + [Entitlement Manager Overview](paytvpass-entitlement/entitlement-overvivew.md)
     + [Integrate Primetime authentication](paytvpass-entitlement/integrate-pass.md)
     + [Configure Adobe Analytics Reporting](paytvpass-entitlement/pass-analytics-setup.md)
     + [Related API documentation](paytvpass-entitlement/pass-apis-callbacks.md)
   + Video Analytics {#video-analytics}
     + [Video Analytics](video-analytics/video-analytics-overview.md)
     + [Create the Video Analytics Manager](video-analytics/create-video-analytics-manager.md)
     + [Configure Video Analytics](video-analytics/configure-video-analytics-manager.md)
     + [Related API documentation](video-analytics/va-apis-callbacks.md)
   + [Build a custom user interface](build-custom-ui.md)
   + [Troubleshooting](troubleshooting.md)
