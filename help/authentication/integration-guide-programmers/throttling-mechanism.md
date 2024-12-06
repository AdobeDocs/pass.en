---
title: Throttling mechanism
description: Know about the Throttling mechanism used in Adobe Pass Authentication. Explore an overview of this mechanism in this page.
exl-id: f00f6c8e-2281-45f3-b592-5bbc004897f7
---
# Throttling mechanism {#throttling-mechanism}

All Pass Authentication customers need to be able to access Pass Authentication API for each of their users, according to instructions and their business case.

Pass Authentication introduces a Throttling mechanism to ensure equitable distribution of resources among our customers' users.

This mechanism is important for a few reasons:

- One of the golden rules of multi-tenant architecture is that one user's behavior shouldn't affect someone else.
- Rate limiting is important for APIs as it's easy to make mistakes when integrating with an API. Because APIs are programmatically, it's relatively easy to accidentally send more requests than intended.

## Mechanism overview {#mechanism-overview}

### Client implementations

Pass Authentication provides guidelines and SDK for interacting with the API but does not control how the customer uses it. Some implementations may have a rudimentary implementation and could flood the service with unnecessary API requests, be it accidentally or not, could mean other users experience slowdowns or capacity issues.

The service itself should be able to handle any reasonable capacity. But no matter how scalable or performant a service is, there are always limits. As such, the service must have limits configured for the number of accepted calls within a specific time interval.

### Introducing throttling

Pass Authentication is based on user identification and a token bucket rate limiting algorithm with predefined values to control each user's device access to our API.

### Device identification mechanism

The proposed throttling mechanism uses the identified devices individually, with the help of “X-Forwarded-For” header. Limits will be applied in the same way for each device.

### Required Updates

Server-to-server implementations must forward their client's IP addresses using the “X-Forwarded-For” header mechanism.

You can find more details on how to pass the X-Forwarded-For header [here](legacy/rest-api-v1/cookbooks/rest-api-cookbook-servertoserver.md).

### Actual limits and endpoints

Currently, the default limit allows a maximum of 1 request per second, with an initial burst of 10 requests (one-time allowance on the first interaction of the identified client, which should allow initialization to finish successfully). This should not affect any regular business case across all our customers.

The throttling mechanism will be enabled on the following endpoints:

- /o/client/register
- /o/client/token
- /o/client/scopes
- /o/client/validate
- /api/v2/
- /api/v1/tokens/usermetadata
- /api/v1/tokens/authn
- /api/v1/tokens/authz
- /api/v1/tokens/media
- /api/v1/config/
- /api/v1/checkauthn
- /api/v1/logout
- /api/v1/authorize
- /api/v1/preauthorize
- /api/v1/mediatoken
- /api/v1/authenticate/freepreview
- /api/v1/authenticate/
- /api/v1/.+/profile-requests/.+
- /api/v1/identities
- /adobe-services/config/
- /reggie/v1/.+/regcode
- /reggie/v1/.+/regcode/.+

### SDK implementation disambiguation

Since clients using the Adobe Pass Authentication provided SDKs are not explicitly interacting with any endpoints, this section will present the known functions, how they behave when encountering a throttle response, and the actions that should be taken.

#### setRequestor

Upon reaching the throttle limit using `setRequestor` function from the SDK, the SDK will return a CFG429 error code through `errorHandler` callback.

#### getAuthorization

Upon reaching the throttle limit using `getAuthorization` function from the SDK, the SDK will return a Z100 error code through `errorHandler` callback.

#### checkPreauthorizedResources

Upon reaching the throttle limit using `checkPreauthorizedResources` function from the SDK, the SDK will return a P100 error code through `errorHandler` callback.

#### getMetadata

Upon reaching the throttle limit using `getMetadata` function from the SDK, the SDK will return an empty response through `setMetadataStatus` callback.

For each specific implementation detail, please refer to the specific SDK documentation.

- [JavaScript SDK API Reference](legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md)
- [Android SDK API Reference](legacy/sdks/android-sdk/android-sdk-api-reference.md)
- [iOS/tvOS API Reference](legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md)

### API response changes and response

When we identify that the limit is breached, we will mark this request with a specific response status (HTTP 429 Too Many Requests), instructing that you have consumed all the tokens assigned to the user device (IP address) for the time interval.

The throttling expires after one second of the first 429 responses. Each application that receives a 429 response must wait for at least 1 second before generating a new request.

All customer applications should appropriately handle the “429 Too Many Requests” response.

Here is a sample 429 response message:

```
HTTP/2 429
date: Tue, 20 Feb 2024 11:21:53 GMT
content-type: text/html
content-length: 166
set-cookie: AWSALB=Btl/GzifUpMhUh+TQK63kU4i+gcJOIvAICVLnHTWt5pkrevNsMSQ5DMwM9KlRkNQ0UlXHIDbQoxDua0oVYYFKC8PDwxQjOuuRzxX2fozM+Jcazl2DSfaR7hU2mt2; Expires=Tue, 27 Feb 2024 11:21:53 GMT; Path=/
set-cookie: AWSALBCORS=Btl/GzifUpMhUh+TQK63kU4i+gcJOIvAICVLnHTWt5pkrevNsMSQ5DMwM9KlRkNQ0UlXHIDbQoxDua0oVYYFKC8PDwxQjOuuRzxX2fozM+Jcazl2DSfaR7hU2mt2; Expires=Tue, 27 Feb 2024 11:21:53 GMT; Path=/; SameSite=None; Secure
server: openresty
access-control-allow-credentials: true
access-control-allow-methods: POST,GET,OPTIONS,DELETE
access-control-allow-headers: ap_11,ap_42,ap_z,ap_19,ap_21,ap_23,authorization,content-type,pass_sfp,AP-Session-Identifier,AP-Device-Identifier,AP-SDK-Identifier,X-Device-Info
access-control-expose-headers: pass_sfp,Authzf-Error-Code,Authzf-Sub-Error-Code,Authzf-Error-Details
p3p: CP="NOI DSP COR CURa ADMa DEVa OUR BUS IND UNI COM NAV STA"

<html>
<head><title>429 Too Many Requests</title></head>
<body>
<center><h1>429 Too Many Requests</h1></center>
<hr><center>openresty</center>
</body>
</html>
```

## Impact and required changes

### Passing X-Forwarded-For header

Customers using a custom implementation (including server-to-server ones) to interact with Pass Authentication API should ensure that they can capture their user IP address and forward it correctly, using X-Forwarded-For header further to Pass Authentication API.

See [here](legacy/rest-api-v1/cookbooks/rest-api-cookbook-servertoserver.md) for more details.

### Reacting to new response code

Customers using a custom implementation (including server-to-server ones) to interact with Pass Authentication API should ensure that any subsequent call made after receiving a 429 Too Many Requests includes a minimum 1-second waiting period. This waiting period ensures an opportunity to change this mechanism and obtain a valid business response.

## Scenario example for throttling

| Time since first request | Response received                 | Explanation                                                                                               |
|--------------------------|-----------------------------------|-----------------------------------------------------------------------------------------------------------|
| Second 0                 | Call receives success status code | 1 calls consumed from the limit                                                                           |
| Second 0.3               | Call receives success status code | 1 calls consumed from the limit and 1 calls marked as burst                                               |
| Second 0.6               | Call receives success status code | 1 calls consumed from the limit and 2 calls marked as burst                                               |
| Second 0.9               | Call receives success status code | 1 calls consumed from the limit and 3 calls marked as burst                                               |
| Second 1.2               | Call receives success status code | 2 calls consumed from the limit and 3 calls marked as burst                                               |
| Second 1.3               | Call receives success status code | 2 calls consumed from the limit and 4 calls marked as burst                                               |
| Second 1.4               | Call receives success status code | 2 calls consumed from the limit and 5 calls marked as burst                                               |
| Second 1.5               | Call receives success status code | 2 calls consumed from the limit and 6 calls marked as burst                                               |
| Second 1.6               | Call receives success status code | 2 calls consumed from the limit and 7 calls marked as burst                                               |
| Second 1.7               | Call receives success status code | 2 calls consumed from the limit and 8 calls marked as burst                                               |
| Second 1.8               | Call receives success status code | 2 calls consumed from the limit and 9 calls marked as burst                                               |
| Second 2.1               | Call receives success status code | 3 calls consumed from the limit and 9 calls marked as burst                                               |
| Second 2.2               | Call receives success status code | 3 calls consumed from the limit and 10 calls marked as burst                                              |
| Second 2.4               | Call receives 429 status code     | 3 calls consumed from the limit and 10 calls marked as burst and 1 calls receives ‘429 Too many requests’ |
| Second 2.6               | Call receives 429 status code     | 3 calls consumed from the limit and 10 calls marked as burst and 2 calls receives ‘429 Too many requests’ |
| Second 2.8               | Call receives 429 status code     | 3 calls consumed from the limit and 10 calls marked as burst and 3 calls receives ‘429 Too many requests’ |
| Second 3.1               | Call receives success status code | 4 calls consumed from the limit and 10 calls marked as burst and 3 calls receives ‘429 Too many requests’ |
