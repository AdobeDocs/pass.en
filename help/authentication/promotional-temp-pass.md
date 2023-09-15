---
title: Promotional Temp Pass
description: Promotional Temp Pass
exl-id: 705c1ba9-0430-4e3b-add1-d9e4da3f82d1
---
# Promotional Temp Pass {#promotional-temp-pass}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Feature summary {#feature-summary}

Promotional Temp Pass allows Programmers to offer temporary access to their protected content for users who don't have account credentials with an MVPD.

Promotional Temp Pass is designed to be used for running promotional campaigns where a user, after providing valid identification information (for example, e-mail address) to the Programmer, will be able to consume a **predefined number of different VOD titles for a predefined period of time**.

>[!IMPORTANT]
>
>Adobe doesn't store any Personally Identifiable Information (PII). Therefore, the Programmer must set a hash over the unique user provided information on the Adobe Pass authentication APIs.

Promotional Temp Pass is built on top of the [Temp Pass](/help/authentication/temp-pass.md) feature, meaning it includes all the Temp Pass functionality. 

Once the maximum predefined number of VOD titles or the predefined period of time are exceeded, that user will not be able to access content on the same device or by using the same user identifier information (for example, e-mail address) until the authorization tokens are cleared from the Adobe Pass authentication server.

>[!NOTE]
>
>Temp Pass is part of the Premium Workflow package. Please contact your Adobe Pass sales rep if interested in using this functionality.

## Temp Pass and Promotional Temp Pass comparison {#tp-ptp-comparison}

|              Temp Pass             |                                   Promotional Temp Pass                                  |
|----------------------------------|----------------------------------------------------------------------------------------|
| Access to content <ul><li>time-based</li></ul>       | Access to content <ul><li>time-based</li><li>based on number of resources</li></ul>                                |
| Access security based on <ul><li>device ID</li></ul> | Security based on <ul><li>device ID</li><li>hash over provided user identifier information (for example, e-mail)</li></ul> |
| Client Error API available         | Client Error API available                                                               |
| Resetting / Purging available      | Resetting / Purging available                                                            |

## Feature details {#feature-details}

This feature enables users to access promotional content from a specific device (phone and tablet) after having provided unique information, such as the e-mail address, in the Programmer's application.

The Programmer will provide a hash over the user's PII on the authentication and authorization APIs. This hash will be used together with the device Id in generating a unique key to identify the user and device.   

Based on device Id and the information the user provided and following the logic below, Adobe Pass authentication will determine if the user is in a new trial or in an existing one:

* new hash over user-provided information (for example, e-mail), new device Id => new trial
* existing hash over user-provided information (for example, e-mail), new device Id  => existing trial (with existing hash over user provided information (for example, e-mail)) 
* new hash over user-provided information (for example, e-mail), existing device Id => existing trial (with existing device Id)
* existing hash over user-provided information (for example, e-mail), existing device Id => existing trial 

>[!NOTE]
>Validation and hashing of the user-provided information is handled by the Programmer, not by Adobe. 

**The Promotional Temp Pass feature can be configured based on the following properties:**

* User-provided information key (for example, e-mail)
* Number of resources which the user is entitled to consume
* TTL - the time frame in which the user is entitled to consume the configured number of resources

### User metadata {#user-metadata}

To facilitate the implementation of the Programmer's application, the following **user metadata information is exposed** on the Promotional Temp Pass, with corresponding keys (to activate the keys, contact tve-support@adobe.com):

* **remaining_resources**: the number of remaining resources which the current user is entitled to consume
* **used_assets**: the list of resources that the current user has already consumed
* **expiration_date**: the current user's expiration date 

### How viewing time is computed? {#compute-viewing-time}

The amount of time that a Temp Pass remains valid does not correlate to the amount of time a user spends viewing content on the Programmer's application. Upon the initial user request for authorization via Promotional Temp Pass, an expiration time is computed by adding the initial current request time to the TTL (duration time frame) specified by the Programmer. 

### Authentication and authorization {#authn-authz}

For Promotional Temp Pass flows, authentication and authorization do not communicate with an actual MVPD, **so all authorization requests will succeed** as long as all these conditions are met:

* authorization tokens are valid for specified resources
* number of **used_assets** is lower than the limit set by the Programmer
* **expiration_date** value is after current date. 

### Preflight behavior {#preflight-beh}

When a preflight or preauthorization request is made for a Promotional Temp Pass MVPD, the corresponding Preflight response returned will contain the entire list of resources from the Preflight Request as preflight successful.

The logic behind this is: the Promotional Temp Pass authorization conditions are based on time and resource number limit rather than on specific resources. More specifically, as long as the time constraint is met and as long as the resource limit is not exceeded, the called resources will be authorized. 

### SSO {#sso}

SSO is not enabled for instances of Promotional Temp Pass, which is configured with "Authentication Per Requestor" enabled. This means that when the user switches from application A to another application B which are both integrated with the same Promotional Temp Pass, the user will not be automatically signed in. 

### Logout {#logout}

All the tokens on a device are deleted on logout. Therefore, switching from the Promotional Temp Pass to a regular user-selected MVPD should not rely on this implementation. The recommendation is to use the `setSelectedProvider(null)` function in order to clear the application state and then restart the authentication flow, which has a better user experience. 

### Promotional Temp Pass flow diagram {#promo-tempass-flowdia}

![Promotional Temp Pass flow diagram](assets/promo-temp-pass-flow.png)

*Figure: Promotional Temp Pass flow*

## Implement Promotional Temp Pass {#impl-promo-tempass}

Promotional Temp Pass requires the following client-side functionalities:

* **User identifier information, for example e-mail address propagation** (sending the user's e-mail address on the authentication and authorization flows). The e-mail is required by Adobe Pass authentication to bind the authentication and authorization tokens (similar to the case of the `device_ID`, required on all the calls).
* **Force authentication** - allowing the Programmer to force an authentication flow when the user is already authenticated. This functionality is required in order to force a user metadata refresh (the user metadata key **used_assets** contains the number of available resources) every time the app is started. Because the user can login on multiple devices, the user metadata present on the device during app startup is unreliable, and we need to update it in order to reflect the current state for that specific user (identified by e-mail address).
 

>[!IMPORTANT]
>Force authentication is possible only on iOS and Android.
>Adobe Pass authentication does not have a built-in mechanism to stop the free streaming after the X minutes have passed. Adobe Pass authentication will cease issuing **authorization** and **short media** tokens once the user consumes the Y free resources. It is up to Programmers to restrict the access once the Promotional Temp Pass expires.

## Security {#security}

>[!IMPORTANT]
>Adobe doesn't store any Personally Identifiable Information (PII). Therefore, the Programmer must set a hash over the unique user provided information on the Adobe Pass authentication APIs. 

**Hashing of user identifier information**

Adobe recommends using the **SHA-2** family or its specific **SHA-256**, **SHA-512** functions on data before it is sent to Adobe.

For example, **SHA-256** over **"user@domain.com"** is **"f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7"**.

## Reset or purge Promotional Temp Pass {#reset-promo-tempass}

Certain business rules require a regular purging of Promotional Temp Pass. In order to do so, Adobe Pass authentication provides Programmers with a *public* web API, described below:

| `DELETE https://mgmt.auth.adobe.com/reset-tempass/v2/reset` |
|----|
| <ul><li>Protocol: **https**</li><li>Host:<ul><li>Release: **mgmt.auth.adobe.com**</li><li>Prequal: **mgmt-prequal.auth.adobe.com**</li></ul></li><li>Path: **/reset-tempass/v2/reset**</li><li>Query parameters: **device_id=all&requestor_id=THE_REQUESTOR_ID&mvpd_id=THE_TEMPASS_MVPD_ID**</li><li>headers: ApiKey: **1232293681726481**</li> <li>Response:<ul><li>Success: **HTTP 204**</li><li>Failure: **HTTP 400** for incorrect requests, **HTTP 401** if ApiKey not specified, **HTTP 403** if ApiKey is invalid</li></ul></li></ul> |

On top of the requirements to purge Temp Pass, the Promotional Temp Pass uses the hash over user identifier information sent as **generic_data** on authentication and authorization for purging. 

The hash will be sent, not the entire JSON:

```cURL
$ curl -X DELETE -H "Authorization:Bearer H4j7cF3GtJX81BrsgDa10GwSizVz" "https://mgmt.auth.adobe.com/reset-tempass/v2.1/reset/generic?key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7&requestor_id=REF&mvpd_id=FlexibleTempPass"

```

### Supported clients {#supported-clients}

| Adobe Pass authentication Clients | Promotional Temp Pass | Reset Tool | Supports Dedicated Response Code / Client Error |
|:--------------------------------------:|:---------------------:|:----------:|:-----------------------------------------------:|
| JS Access Enabler                      | YES                   | YES        | YES (starting with v 3.0.0)                     |
| Native Client iOS                      | YES                   | YES        | YES (starting with v 1.10)                      |
| Native Client Android                  | YES                   | YES        | YES                                             |
| Clientless API                         | YES                   | YES        | NO                                              |


## Limitations {#limitations}

This section describes the limitations that apply to the current implementation of Promotional Temp Pass.

### Clientless {#lim-clientless}

**Smart devices without a Unique Device ID** 

Not all smart device apps are able to provide a Unique Device ID. In the absence of one, Adobe Pass authentication can use the UUID generated by the Adobe Registration Code Service as the Unique Device ID. This means that when user signs out, the authentication and authorization tokens will be deleted. Once the user will attempt to authenticate again, this time with different user information (for example, e-mail) the user will be able to authorize again. Adobe recommends adding an UI flow that will not allow a user to "fool" the system and add logic to determine whether it is a new user requesting a trial or an existing trial. 

**Resetting / purging Temp Pass**

Reset Temp Pass for Clientless is not available in the specific cases of Xbox360 and Xbox One, because these platforms require additional device ID parsing, not possible in the Reset Temp Pass tool.

<!--
>[!RELATEDINFORMATION]
>
>* [Preflight Authorization](/help/authentication/preflight-authz.md)
-->
