---
title: Handling authentication requests
description: Handling authentication requests
copied-description: yes
exl-id: c1d46ec0-e053-4824-b3b1-20320e259fbe
---
# Handling authentication requests{#handling-authentication-requests}

The `AuthenticationHandler` class is used to process authentication requests. It is used only for username/password authentication.

When generating the authentication token, the token expiration date must be specified. Custom properties may also be included in the token. If set, those properties will be visible to the server when the authentication token is sent in subsequent requests. See [Handling license requests](../../aaxs-protecting-content/content-implementing-the-license-server/content-handling-license-reqs/content-handling-license-reqs.md) for information on handling custom authentication tokens.

The handler reads an authentication request and parses the request message when `parseRequest()` is called. The server implementation examines the user credentials in the request, and if the credentials are valid, generates an `AuthenticationToken` object by calling `getRequest().generateAuthToken()`. If `AuthenticationRequestMessage.generateAuthToken()` is not called before `close()`, an authentication failure error code is sent.

* The request handler class is `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationHandler` 
* The request message class is `com.adobe.flashaccess.sdk.protocol.authentication.AuthenticationRequestMessage` 
* If both the client and server support protocol version 5, the request URL is "License Server URL in metadata: + "/flashaccess/authn/v4". If protocol version 3 is the maximum supported by either the client or server, Adobe Access clients will send authentication requests to “License Server URL in metadata” + “/flashaccess/authn/v3”. Otherwise, authentication requests are sent to “License Server URL in metadata” + “/flashaccess/authn/v1”
