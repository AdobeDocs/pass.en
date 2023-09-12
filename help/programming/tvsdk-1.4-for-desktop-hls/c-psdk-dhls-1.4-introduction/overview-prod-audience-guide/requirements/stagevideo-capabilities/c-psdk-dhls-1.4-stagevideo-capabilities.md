---
description: On devices that support GPU (hardware) acceleration, you can use a flash.media.StageVideo object to process video on the device hardware. The availability of StageVideo depends upon the versions and capabilities of different parts of your system including Flash Player, video hardware, OS, drivers, browser, network connection, and viewing context.
title: StageVideo capabilities and restrictions
exl-id: 228ea2d0-5950-43f5-8cfd-640d1c482b05
---
# Overview {#stagevideo-capabilities-and-restrictions-overview}

On devices that support GPU (hardware) acceleration, you can use a flash.media.StageVideo object to process video on the device hardware. The availability of StageVideo depends upon the versions and capabilities of different parts of your system including Flash Player, video hardware, OS, drivers, browser, network connection, and viewing context.

The `StageVideo` class lets you take advantage of hardware acceleration to present video at the highest possible performance level for a device. The availability and performance of `StageVideo` is affected by the following factors:

* **Hardware acceleration** - When hardware acceleration is available, `StageVideo` processes video on the device hardware. When hardware acceleration is not available, the `StageVideo` responds depends on which version of Flash you are running:

    * *Flash 15 and later* - When hardware acceleration is not available, `StageVideo` falls back to software, and you do not have to do anything.     
    
      >[!TIP]
      >
      >When hardware acceleration is not available, performance can degrade significantly.

    * *Flash 14 and earlier* - When hardware acceleration is not available, `StageVideo` becomes unavailable. In a small set of configurations where hardware acceleration is not supported by the browser or GPU, or is turned off in the Flash Player, video display with the TVSDK HLS stack will fail. In the *HDS* pipeline, you can switch from `StageVideo` to an alternate, such as the Video object, that processes video in the CPU.

* **Presentation context** - During full screen viewing, `StageVideo` is always available and performance will be at the maximum level that is available on the device. When not viewing full-screen, the video presentation falls under the context of the browser, where the browser's settings and capabilities are used. 

* **wmode** - In the browser context, the `wmode` setting is critical to performance. Adobe recommends that you keep `wmode` set to `direct` to ensure the best possible performance in the browser context. 

  >[!NOTE]
  >
  >The combination of factors that include `wmode`, `StageVideo`, and Flash result in different capabilities and restrictions, depending upon how fast your hardware runs and which version of Flash you are using.

    * *Flash 15 and later* - `StageVideo` is available with all available `wmode` settings. However, if you set `wmode` to a setting other than `direct`, performance will be lower. 
    
    * *Flash 14 and earlier* - If you set `wmode` to a setting other than `direct`, `StageVideo` is not available in all browsers.
