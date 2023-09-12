---
description: From Flash 15 and later, when hardware rendering with StageVideo is not available, StageVideo seamlessly falls back to a software StageVideo object.
title: Flash 15 support for StageVideo
exl-id: 23ef0806-3aa5-4c48-a4f7-4ad9b72bdcc9
---
# Flash 15 support for StageVideo{#flash-support-for-stagevideo}

From Flash 15 and later, when hardware rendering with StageVideo is not available, StageVideo seamlessly falls back to a software StageVideo object.

Consider the following information about the Flash 15 StageVideo fallback to software:

* No code changes are required in your application. 
* No change to TVSDK is required.

  You do not need a TVSDK update to use StageVideo fallback to software. 
* Your applications need to be recompiled for Flash 15. 
* Applications that you recompile for Flash 15 will continue to work with Flash 14 and earlier, as long as these applications do not use any new APIs that were introduced in Flash Player 15.

  If your Flash 14 application needs to use a new Flash 15 API, you must dynamically call the API with a cast to the Object type, so that the application does not fail in Flash Player 14 at runtime.

## HTML Overlays {#html-overlays}

In Flash 15 and later, you can maintain a seamless display of HTML overlays when hardware StageVideo becomes unavailable and falls back to software StageVideo. To enable this feature, set `wmode=opaque`.

Some older browsers do not support hardware acceleration. For more information about these requirements, see [StageVideo minimum requirements](../../../../../tvsdk-1.4-for-desktop-hls/c-psdk-dhls-1.4-introduction/overview-prod-audience-guide/requirements/stagevideo-capabilities/r-psdk-dhls-1.4-requirements-stage-video.md). When you set `wmode=opaque`, the video is rendered with software StageVideo, which can impact performance. Typically, setting `wmode=direct` directly renders video to GPU, which results in much better performance. However, this option also overrides HTML overlays.
