---
description: Streaming over the Internet requires a constant and stable connection to play a stream from a remote server. However, the variability of a viewer's Internet connection or streaming playback means that remote playback might not have the quality of media played locally.
title: AC-3 5.1 format
exl-id: dcc43c1b-b9ce-44a1-a4c9-50ccfc5d572d
---
# AC-3 5.1 format{#ac-format}

Streaming over the Internet requires a constant and stable connection to play a stream from a remote server. However, the variability of a viewer's Internet connection or streaming playback means that remote playback might not have the quality of media played locally.

Primetime cannot protect from such failures as an ISP outage or a cable disconnection. However, Primetime streaming provides failover protection to protect playback from certain remote server failures or operational failures, making a better experience for viewers. TVSDK implements failover protection to minimize playback interruptions and achieve a seamless playback despite transmission problems. The video player automatically switches to a backup media set when entire renditions or fragments are unavailable.

The Audio Codec 3 (AC-3, also known as Dolby Digital®) 5.1 format, allows content providers to compress the size of multichannel audio files without impairing the sound quality. AC-3 is a 5.1 format, which means that it provides five full-bandwidth channels for a richer user experience.

For more information, see [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

>[!IMPORTANT]
>
>TVSDK version 1.4 supports the AC-3 5.1 format only on Amazon FireTV.

TVSDK supports the following AC-3 5.1 features:

* AC-3 surround audio 
* Mixed/unmixed streams for surround audio type 
* Ability to query the device to see if the surround audio codec is available on the device.

  The results determine which preferred audio codec type is selected. The manifest with audio codec type that the device is not going to use is discarded. For example, if the AC-3 format has been selected, profiles with the Advanced Audio Coding (AAC) format are not considered. 
* Passthrough mode

  In passthrough mode, instead of decoding the media from the AC-3 5.1 format to a multichannel pulse-code modulation (PCM) format, the TVSDK gets modified or unmodified (depending on the device) Dolby media from the Decoder. This media is sent to the audio device (speaker or receiver) so that the audio device can decode and play back the Dolby surround stream.

TVSDK supports the AC-3 5.1 features only on the device Amazon Fire TV 1st generation.

The following AC-3 5.1 features are not supported:

* Multichannel AAC audio 
* ABR across different codecs (AAC - AC3)

## Selecting supported media {#section_E1DFA1F472EA4BDE846C71A3343E275A}

Here is the typical workflow that occurs when TVSDK finds a manifest with AC-3 and AAC media:

1. TVSDK queries which codec the device can support. 
1. The codec with the higher quality is selected.

   The order of quality is AC-3 > AAC. 
1. TVSDK ignores profiles with other audio codec types.

>[!TIP]
>
>The application cannot obtain information about ignored profiles.

## Determining the output mode {#section_64145D9824594C36AADBF0482C528767}

While processing AC-3 media, if an Android device is connected to the speaker system, the decision to play content in surround mode or stereo mode depends on how the device is configured.  

|   | Surround sound  | Stereo speaker  |
|---|---|---|
|  Device configuration Dolby on (or auto)  | Device configuration Dolby on (or auto)  | Stereo mode  |
|  Device configuration Dolby off  | Stereo mode  | Stereo mode  |
