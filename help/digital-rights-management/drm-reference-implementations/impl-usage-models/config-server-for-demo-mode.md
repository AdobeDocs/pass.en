---
title: Configure usage model demo mode
description: Configure usage model demo mode
copied-description: yes
exl-id: 593acfbd-fd37-4bab-ac8e-5cb62963fac4
---
# Configure usage model demo mode{#configure-usage-model-demo-mode}

Before the Reference Implementation server can issue licenses for the usage model demo, you must configure the server to specify how licenses are generated for each of the four usage models. This means you need to specify a DRM policy for each usage model. The Reference Implementation includes the following sample DRM policies in the [!DNL Reference Implementation/Server/Reference Implementation Server/resources/] directory:

* `dto-policy.pol` - (Download-To-Own)
* `vod-policy.pol` - (Rental/Video-On-Demand)
* `sub-policy.pol` - (Subscription)
* `ad-policy.pol` - (Ad-funded)

>[!NOTE]
>
>You can substitute these sample policies with your own DRM policies.

1. Set these properties in [!DNL flashaccess-refimpl.properties] to specify the DRM policy that you plan to apply to each usage model:

   ```
   # DRM Policy file name for Download To Own usage 
   RefImpl.UsageModelDemo.Policy.DTO=dto-policy.pol 
   # DRM Policy file name for Rental usage 
   RefImpl.UsageModelDemo.Policy.VOD=vod-policy.pol 
   # DRM Policy file name for Subscription usage 
   RefImpl.UsageModelDemo.Policy.Subscribe=sub-policy.pol 
   # DRM Policy file name for Ad Supported (free) usage 
   RefImpl.UsageModelDemo.Policy.Free=ad-policy.pol
   ```

1. Copy your sample policy files to the directory you specify in the `config.resourcesDirectory` property in [!DNL flashaccess-refimpl.properties].
