---
description: While the AES-128 encryption method encrypts the entire transport stream (TS) container including headers, the SAMPLE-AES encryption only encrypts the audio and part of the video data.
title: Sample AES encrypted HLS streams
exl-id: 04bda50f-5ca4-4a00-bb5a-97259a2cb005
---
# Sample AES encrypted HLS streams{#sample-aes-encrypted-hls-streams}

While the AES-128 encryption method encrypts the entire transport stream (TS) container including headers, the SAMPLE-AES encryption only encrypts the audio and part of the video data.

In encrypted streams, a protected block is identified over which the protection process is completed. H.264 video protected blocks are the body of types 1 and 5 of network adaptation layer (NAL) units. A protected block of audio is an audio frame, and audio must be in the AAC format.

>[!IMPORTANT]
>
>You must have the key and the initialization vector (IV). Browser TVSDK uses the key and IV to decrypt the stream before playing it.

Each protected block contains an integer of 16-byte blocks that are encrypted using the AES-128 cipher block-chaining (CBC) mode with no padding. CBC occurs in each protected block, and at the start of each new protected block, the IV must be reset to its original value.

The following codecs are supported:

* For video, H.264 is supported. 
* For audio, sample-AES is supported only for AAC.
