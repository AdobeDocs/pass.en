---
description: Closed captions and subtitles have some unique differences, and you enable them in different ways.
title: Subtitles and closed captions
exl-id: 6602e9cf-d1e8-405b-83b7-bdd7d93b88f1
---
# Requirements for subtitles and closed captions {#requirements-for-subtitles-and-closed-captions}

Closed captions and subtitles have some unique differences, and you enable them in different ways.

Subtitle streams run in parallel with the main content. Closed captions are part of the data packets of the MPEG-2 video streams.

You should be aware of the following requirements for closed captions and subtitles:

* **Closed captions**

    * Closed captions are typically in the same language as the audio and also represent background sounds as text. 
    * Closed captions are part of the data packets of the MPEG-2 video streams in the video transmission stream. 
    * Closed captions are supported to the extent provided by the AV Foundation framework.

* **Subtitles**

    * Subtitles are typically in a different language and do not include background sounds. 
    * Subtitles are in streams that run in parallel with the main content.

      The `PTMediaPlayer` plays the main content and ads, where the main content could be live/linear or VOD, and ads could be pre-roll, mid-roll, or post-roll.

  Here are some additional requirements for subtitles in iOS:

    * For timestamps, the `X-TIMESTAMP-MAP` value, which is specified in the header section of the `WebVTT` file, must match the video timestamp. 
    
    * For the system, you must use iOS 6.1 or later.

>[!IMPORTANT]
>
>The requirements for subtitles do not apply to closed captions.
