---
title: Throttling mechanism
description: Throttling mechanism
---

# Throttling mechanism {#throttling-mechanism}

## Introduction {#introduction}

Adobe, in its role as your data processor, must take appropriate measures to ensure that our customers' users equitably use resources and the service is not flooded with unnecessary API requests. For this we have put in place a throttling mechanism.
One Concurrency Monitoring application can be used by multiple users and one user can have multiple sessions. Therefore, the service will have limits configured for the number of accepted calls per user/session within a specific time interval.
When the limit has been reached,  the requests will be marked with a specific response status (HTTP 429 Too Many Requests). Any subsequent call done after a “429 Too Many Requests” response is received should be done with at least one minute cool down period to ensure it will obtain a valid business response.

## Mechanism overview {#mechanism-overview}

The mechanism determines the maximum number of accepted calls for each Concurrency Monitoring endpoint within a specific time interval. 
Once this maximum number of calls have been reached, our service will respond with '429 Too many requests'. The 429 response "Expires" header includes the timestamp when the next call would be considered valid, or when the throttling expires. Right now, the throttling expires after one   minute from the first 429 response.

The endpoints configured with throttling are:
1. Create a new session: POST /sessions/{idp}/{subject}
2. Heartbeat call: POST /sessions/{idp}/{subject}/{sessionId}
3. Terminate a session: DELETE /sessions/{idp}/{subject}/{sessionId}

The throttling is configured on two levels:
1. session: same unique {sessionId} parameter sent in `Heartbeat` call  and `Terminate a session` call.
2. user: same unique {subject} parameter sent in `Create a new session` call.

The limit for session level throttling is set to 200 requests within one minute.\
The limit for user level throttling is set to 200 requests within one minute.\
Both these limits (session level throttling and user level throttling) are configurable, and we will update them in case they will be reached through valid integration scenarios. For this we recommend support team to be contacted. 

**Scenario for session level throttling:**

| Time      | Request send to CM                      | Number of requests | Response received from CM                                                    | Explanation                                                                     |
|-----------|-----------------------------------------|--------------------|------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Second 10 | POST /sessions/idp1/subject1/session1   | 50                 | All calls receive ‘202 Accepted’                                             | 50 calls consumed from the limit                                                |
| Second 50 | POST /sessions/idp1/subject1/session1   | 151                | 150 calls receive ‘202 Accepted’ and 1 call receives ‘429 Too many requests’ | 200 calls consumed from the limit and 1 call will receive 429 response          |
| Second 61 | DELETE /sessions/idp1/subject1/session1 | 1                  | 1 call receives ‘429 Too many requests’                                      | No calls in the limit available yet                                             |
| Second 70 | DELETE /sessions/idp1/subject1/session1 | 1                  | 1 call receives ‘202 Accepted’                                               | Limit set to 200 available calls because 60 seconds have passed since second 10 |

**Scenario for user level throttling:**

| Time      | Request send to CM           | Number of requests | Response received from CM                                                    | Explanation                                                                     |
|-----------|------------------------------|--------------------|------------------------------------------------------------------------------|---------------------------------------------------------------------------------|
| Second 10 | POST /sessions/idp1/subject1 | 50                 | 50 calls receive ‘202 Accepted’                                              | 50 calls consumed from the limit                                                |
| Second 50 | POST /sessions/idp1/subject1 | 151                | 150 calls receive ‘202 Accepted’ and 1 call receives ‘429 Too many requests’ | 200 calls consumed from the limit and 1 call will receive 429 response          |
| Second 61 | POST /sessions/idp1/subject1 | 1                  | 1 call receives ‘429 Too many requests’                                      | No calls in the limit available yet                                             |
| Second 70 | POST /sessions/idp1/subject1 | 1                  | 1 call receives ‘202 Accepted’                                               | Limit set to 200 available calls because 60 seconds have passed since second 10 |

**429 Response example:**

```
HTTP/2 429
date: Thu, 15 Feb 2024 07:54:20 GMT
content-length: 0
vary: Origin
vary: Access-Control-Request-Method
vary: Access-Control-Request-Headers
cache-control: no-store
expires: Thu, 15 Feb 2024 07:54:41 GMT
strict-transport-security: max-age=31536000 ; includeSubDomains
x-xss-protection: 1; mode=block
x-frame-options: DENY
x-content-type-options: nosniff
```

## Customer integration recommendations {#customer-integration-recommendations}

With a correct implementation, the customers will not receive “429 Too Many Requests” response.
Still, Adobe recommends that each customer handles “429 Too Many Requests” response appropriately using the technical details presented above. When handling the response, "Expires" header should be used to determine when to send the next valid request. 
