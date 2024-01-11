---
title: Throttling mechanism
description: Throttling mechanism
---

# Throttling mechanism {#throttling-mechanism}

## Introduction {#introduction}

Adobe, in its role as your data processor, must take appropriate measures to ensure that our customers' users equitably use resources and the service is not flooded with unnecessary API requests. For this we have put in place a throttling mechanism.\
For each Concurrency Monitoring end-point, the service will have limits configured for the number of accepted calls per device within a specific time interval. When the limit has been reached,  the requests will be marked with a specific response status (HTTP 429 Too Many Requests).
Any subsequent call done after a “429 Too Many Requests” response is received should be done with at least 1 minute wait period to ensure it will obtain a valid business response.

## Definitions {#definitions}

A throttling mechanism determines the maximum number of accepted calls for each Concurrency Monitoring end-point within a specific time interval.

| Concept |  Description  |
|--|-----|
| Throttling mechanism | API throttling is the process of limiting the number of API requests a user can make in a certain period.     |
| Limit  |   The maximum number of accepted calls to a specific end-point withing a specific time interval  |
| Algorithm |  The throttling algorithm implemented  |
| Throttling level |  The end point parameter on which the throttling is configured  |
| Bucket refill rate |  Bucket refill time expressed in milliseconds. Any call after receiving “429 Too Many Requests” should be done after bucket refill time |

## Technical solution overview {#technical-solution-overview}

Concurrency monitoring throttling mechanism uses a Token bucket algorithm. All requests weigh 1 TOKEN. The bucket refill time is 60000 ms (1 minute).  
The endpoints configured with thottling are:
1. Create a new session: POST /sessions/{idp}/{subject}
2. Heartbeat call: POST /sessions/{idp}/{subject}/{sessionId}
3. Terminate a session: DELETE /sessions/{idp}/{subject}/{sessionId}

The throttling is configured on two levels:
1. session: same unique {sessionId} parameter sent in `Heartbeat` call  and `Terminate a session` call.\
2. user: same unique {subject} parameter sent in `Create a new session` call.

The bucket capacity for session level throttling is set to 200 within one minute.\
The bucket capacity for user level throttling is set to 200 within one minute.\
Both these limits are configurable and we will update them in case they will be reached through valid integration scenarios.

## Customer integration recommendations {#customer-integration-recommendations}

With a correct implementation the customers will not receive “429 Too Many Requests” response.\
Still, Adobe recommends that each customer handles “429 Too Many Requests” response appropriately using the technical details presented above.

## Questions and answers

_Is there any possibility to get the 429  response code again after a 1 minute timeout?_ – After reaching a 429 status, there is a 60 seconds cool down period, after which you can resume normal operations.