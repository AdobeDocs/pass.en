---
description: Downloading video and audio in parallel, rather than in a series, reduces startup delays.
title: Parallel downloads
exl-id: 6c93154b-8de4-448b-bc33-776fcc1f6243
---
# Parallel downloads {#parallel-downloads}

Downloading video and audio in parallel, rather than in a series, reduces startup delays.

Parallel downloads allows video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback.

<!-- 

Removed as part of "no DASH use cases" for 2.5.1, May 31st, 2017 release.
<p>Parallel downloads allows DASH video-on-demand (VOD) files to be played, optimizes the available bandwidth usage from a server, lowers the probability of getting into buffer under-run situations, and minimizes the delay between download and playback. </p>

 -->

Without parallel downloads, TVSDK issues a request for the video segment, and after the video segment is loaded, it requests one or two audio segments. With parallel downloads, the audio and video segments are downloaded simultaneously, not sequentially. Also, because there are two connections and two HTTP requests per segment in parallel, the data reaches the screen faster.

>[!NOTE]
>
>This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. HLS content is often unmuxed, especially with alternate audio.

<!-- 

See comment above (DASH use case removed).
  This feature applies only to content where the audio and video are encoded into different files (unmuxed content) and does not apply to MP4 content, which is always muxed. Most DASH content is unmuxed, and HLS content is often unmuxed, especially with alternate audio. 
-->

The HTTP connection might experience delays at the following stages:

* When establishing the TCP/IP connection to server

  Although the client and server have agreed to communicate, no HTTP communication has occurred yet. This type of delay depends on the infrastructure between the client and the server. This process requires finding a path through the internet between the client and the server and making sure all devices, such as routers and firewalls, on the route agree to the data transfer. 
* When sending an HTTP request for a segment or a manifest over the TCP/IP connection.

  The server receives the request, processes it, and starts sending the data back to the client. The degree of delay depends on the load and the complexity of the software on the server and somewhat on the upload connection speed when the client sends the request.
