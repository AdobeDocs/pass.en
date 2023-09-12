---
description: Events from Browser TVSDK indicate the state of the player, errors that occur, the completion of actions that you have requested, such as a video starting to play, or actions that occur implicitly, such as an ad completing.
title: Listen for Primetime Player events
exl-id: e16fa356-5286-4cae-b7ce-74a2e8093d62
---
# Overview {#listen-for-primetime-player-events-overview}

Events from Browser TVSDK indicate the state of the player, errors that occur, the completion of actions that you have requested, such as a video starting to play, or actions that occur implicitly, such as an ad completing.

Because your application needs to respond to many of these events, you need to implement event-handing routines and register these routines with Browser TVSDK. The routines call the relevant Browser TVSDK methods to respond appropriately.

Here is some additional information about events:

* The real-time nature of video playback requires asynchronous (nonblocking) activity for many Browser TVSDK operations. 
* Browser TVSDK supports an event-driven video player.

  It provides events that correspond to all important steps in the playing process. You register those events with your platform's event mechanism and create event handlers that will be called when those events occur. *`Event Handlers`* are also known as callback routines or event listeners. Browser TVSDK provides a complete range of methods that can be used by the event handlers. 
* Your application generally initiates non-blocking operations, such as requesting that a video start playing.

  Browser TVSDK communicates asynchronously with your application by dispatching events, such as when the video starts playing and an event when the video finishes. Other events can indicate status changes in your player and error conditions. Your event handlers take appropriate actions.
