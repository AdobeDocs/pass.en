---
description: You can customize or override ad behaviors.
title: Set up customized playback
exl-id: aaa4d1c2-c425-4a2e-8377-0a3072f3fb18
---
# Set-up customized playback {#cset-up-customized-playback}

You can customize or override ad behaviorr by registering the ad policy instance with TVSDK.

To customize ad behaviors, do one of the following:

* Implement the `AdPolicySelector` interface and all its methods.
This option is recommended if you need to override all the default ad behaviors.

* Extend the `DefaultAdPolicySelector` class and provide implementations for only those behaviors that require
customization.
This option is recommended if you need to override only some of the default behaviors.

For both options, complete the following tasks:

To customize ad behaviors:

1. Implement the AdPolicySelector interface and all of its methods.

1. Assign the policy instance to be used by TVSDK through the advertising factory.

>[!IMPORTANT]
>
>Custom ad policies that are registered at the beginning of >playback are cleared when the MediaPlayer instance is >deallocated.Your application must register a policy >selector instance each time a new playback session is created.

For example:

```

    class CustomContentFactory extends ContentFactory {
     ...
    @Override
    public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem mediaPlayerItem) {
    return new CustomAdPolicySelector(mediaPlayerItem);
    }
     ...
    }
    TVSDK 1.4 for Android Programmer's Guide 46
    // register the custom content factory with media player
    MediaPlayerItemConfig config = new MediaPlayerItemConfig();
    config.setAdvertisingFactory(new CustomContentFactory());
    // this config will should be later passed while loading the resource
    mediaPlayer.replaceCurrentResource(resource, config);
```

1. Implement your customizations.
