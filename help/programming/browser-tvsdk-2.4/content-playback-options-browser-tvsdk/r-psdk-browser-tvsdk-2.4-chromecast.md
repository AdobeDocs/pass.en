---
description: You can cast any of the streams from a TVSDK-based sender app and have the stream played back on Chromecast with Browser TVSDK.
title: Google Cast app for Browser TVSDK
exl-id: 71077467-8040-4f04-a43b-cc963701c426
---
# Google Cast app for Browser TVSDK{#google-cast-app-for-browser-tvsdk}

You can cast any of the streams from a TVSDK-based sender app and have the stream played back on Chromecast with Browser TVSDK.

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

There are two components of a Cast-enabled app:

* The sender app, which acts as the remote control.

  Sender apps include smart phones, personal computers, and so on. The app can be developed using native SDKs for iOS, Android, and Chrome. 
* The receiver app, which runs on Chromecast and plays the content. 

  >[!IMPORTANT]
  >
  >This app can only be an HTML5 app.

The sender and the receiver communicate by using the Cast SDKs to pass messages.

## Basic Workflow {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

Here is an overview of the process:

1. The sender app establishes a connection with the receiver app. 
1. The sender app sends a message to load the media on the receiver app. 
1. The receiver app begins playback. 
1. The sender app sends playback control messages, such as play, pause, seek, fast forward, fast rewind, rewind, volume change, and so on, to the receiver app. 
1. The receiver app reacts to these messages.

## Message format {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

You must define the messages so that the sender and receiver can understand. Here is an example of a seek message: 

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 

```

When sending custom messages such as the seek message through the Cast SDKs, a custom message namespace is required. Here is an example in JavaScript: 

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 

```

## Establishing a connection {#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>Browser TVSDK APIs are not involved when establishing the connection.

To establish a connection, the sender and receiver must complete the following tasks:

* The sender must review the documentation for platform at [Sender App Development](https://developers.google.com/cast/docs/sender_apps). 
* The receiver uses the Cast receiver APIs to establish a connection with the sender app. For example: 

  ```js
  window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
     
  window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
  window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
  window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
     
  var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
  customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
     
  window.castReceiverManager.start(); 
  
  ```

## Message Handling {#section_3E4814546F5946C9B3E7A1AE384B4FF8}

To send messages to the receiver, see the documentation for your sender's platform. 

>[!IMPORTANT]
>
>You must include the custom message namespace, `MSG_NAMESPACE` in all the messages.

For the receiver app, follow the documentation for the cast receiver APIs.

**Example of a Chrome-Based Sender Message** 

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**Chrome Based Sender Event Handling**

Bind event handlers to your UI elements that will send messages when the corresponding events are triggered. For example, for a Chrome-based sender app, the seek event might be sent like this: 

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 

```

**Receiver Message Handling**

From the receiver app, here is an example of how to handle the seek message: 

```js
customMessageBus.onMessage = function (event) { 
    var message = JSON.parse(event.data); 
    switch (message.type) { 
        case "seek":  
            player.seek(parseInt(message.seekTo)); 
            break; 
        //code for handling other events 
        default:  
            break; 
    } 
}; 

```
