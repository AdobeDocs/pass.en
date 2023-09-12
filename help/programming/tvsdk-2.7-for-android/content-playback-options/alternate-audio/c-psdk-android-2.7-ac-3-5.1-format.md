---
description: The Audio Codec 3 (AC-3, also known as Dolby Digital®) 5.1 format, allows content providers to compress the size of multichannel audio files without impairing the sound quality. AC-3 is a 5.1 format, which means that it provides five full-bandwidth channels for a richer user experience.
title: AC-3 5.1 format
exl-id: 16647d69-9cb4-4bb8-8ad9-cac8811ea66d
---
# AC-3 5.1 format {#ac-format}

The Audio Codec 3 (AC-3, also known as Dolby Digital®) 5.1 format, allows content providers to compress the size of multichannel audio files without impairing the sound quality. AC-3 is a 5.1 format, which means that it provides five full-bandwidth channels for a richer user experience.

For more information, see [Dolby Digital 5.1](https://www.dolby.com/us/en/technologies/dolby-digital.html).

TVSDK supports the following AC-3 5.1 features:

* AC-3 surround audio 
* Mixed/unmixed streams for surround audio type 
* Ability to query the device to see if the surround audio codec is available on the device.

  The results determine which preferred audio codec type is selected. The manifest with audio codec type that the device is not going to use is discarded. For example, if the AC-3 format has been selected, profiles with the Advanced Audio Coding (AAC) format are not considered. 
* Passthrough mode

  In passthrough mode, instead of decoding the media from the AC-3 5.1 format to a multichannel pulse-code modulation (PCM) format, the TVSDK gets modified or unmodified (depending on the device) Dolby media from the Decoder. This media is sent to the audio device (speaker or receiver) so that the audio device can decode and play back the Dolby surround stream.

>[!IMPORTANT]
>
>TVSDK supports the AC-3 5.1 features only on the device Amazon Fire TV 1st generation.

The following AC-3 5.1 features are not supported:

* Multichannel AAC audio 
* ABR across different codecs (AAC - AC3)

## Select supported media {#section_0D7E717BE18B418D817EE017EF2375D1}

Here is the typical workflow that occurs when TVSDK finds a manifest with AC-3 and AAC media:

1. TVSDK queries which codec the device can support. 
1. The codec with the higher quality is selected.

   Here is the order in which quality is selected:

    1. AC-3 
    1. AAC

1. TVSDK ignores profiles with other audio codec types.

>[!TIP]
>
>The application cannot obtain information about ignored profiles.

## Determine the output mode {#section_D2AFBF33D3904AC2A7C653A60C3A0CD3}

While processing AC-3 media, if an Android device is connected to the speaker system, the decision to play content in surround mode or stereo mode depends on how the device is configured.  

|   | Surround sound  | Stereo speaker  |
|---|---|---|
|  Device configuration Dolby on (or auto)  | Device configuration Dolby on (or auto)  | Stereo mode  |
|  Device configuration Dolby off  | Stereo mode  | Stereo mode  |
