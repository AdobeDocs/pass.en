---
title: Policy Information Point
description: Policy Information Point
exl-id: 964bb28d-cfef-4a37-b6c4-10cc59be0b47
---
# Policy Information Point {#pip}

>[!NOTE]
>
>This page is deprecated as it applies to the previous version of the API which is no longer recommended for new integrations

The following diagram shows the flow in case the customer opts for the **Policy Information Point**, in which case CM is merely used for querying the activity and all the access logic is embedded in the client application):

![](../assets/pip-workflow.png)

 

The diagram below illustrates how stream counting works for a user that watches content from 2 devices.

![](../assets/pip-sequence.png)

In a nutshell, the usual message flow is as follows: 

1. Initially, for a user that has never used the service, a web page is loaded / an application is opened, where a Concurrency Monitoring Service instrumented application makes a Session Initialization call. 
1. The Concurrency Monitoring Service returns the new stream resource for heartbeats, as well as the current user activity.
1. During video playback, the instrumented application makes heartbeat calls to the Concurrency Monitoring Service, showing that the user is currently consuming a video.
1. At any other point, other instrumented applications can make Status query calls to the Concurrency Monitoring Service, which will return the current user activity. 
1. At video playback end, the instrumented application can make a heartbeat call with "event=stop", signifying that the video has stopped, and that the current stream should not be counted as an active stream anymore.
