---
title: Use cases
description: Use cases in Concurrency Monitoring.
exl-id: 6cc30bb6-e985-4d9a-9f99-a7f04ae8deb7
---
# Use Cases {#use-cases}

The main use case of the Stream Counting Service is counting the number of concurrent video streams watched by a user and provide a decision regarding its concurrent usage for the same account id.

In order to monitor usage by subscriber, there is a need for a centralized service that can aggregate user activity regardless of whether it happens on the programmer's web site or application, on the MVPD's content portal or on a syndicated property. 

The main use cases supported by this centralized service should be:

1. As soon as a subscriber starts watching a video, the application can **initialize a streaming session** and start **reporting activity** data.
1. In the same central service, another instance will receive ***CM decisions*** - in case the application has one or more policies registered in the CM service, the service will respond with access decision based on the current activity.

## Common Use Cases {#common-use-cases}

### Basic Stream Limiting

Limit the number of concurrent streams per subscriber across all your applications.

### Device-Based Restrictions

Allow only a certain number of streams per device type (mobile, tablet, TV, etc.).

### Content-Specific Rules

Apply different limits for live content vs. VOD content.

### Location-Based Policies

Restrict streaming based on geographic location or network type.

## Creating a session {#create-session}

This API call allows the client to create a new CM session when the user presses the "play" button to watch some content. The server response will contain the new stream URL (containing the stream ID) for keeping it alive and the time when the stream will timeout. It is expected that the client application will report activity through heartbeats. The session initialization call has to include metadata in the form of key/value pairs sent as form data (or query string parameters). Furthermore, the response will also include a flag to indicate whether the playback is "policy compliant". If it is not, then the playback isn't allowed.

## Reporting activity {#reporting-activity}

Once a session is created, the application needs to send heartbeats regularly in order for that stream to stay active. Also, it's recommended that the client app stops the stream once the user stops the playback, so that the stream will not count as active until timeout.

The response of the heartbeat call can allow the client application to continue video playback (when it is policy compliant) or it can instruct it to stop the video playback. In the case the video stream is not compliant, the client application has to stop it. The response will provide information in order for the client application to display an error message and/or available actions for the user to continue the playback.
