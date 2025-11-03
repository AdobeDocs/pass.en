---
title: TempPass Feature
description: TempPass Feature
exl-id: 1df14090-8e71-4e3e-82d8-f441d07c6f64
---
# TempPass Feature {#temp-pass-feature}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

TempPass is a versatile feature that empowers Programmers to offer temporary access to their protected content for users without valid MVPD account credentials. It serves as an effective tool for engaging viewers, whether through basic access scenarios or targeted promotional campaigns.

TempPass is a powerful solution for Programmers to:

* **Engage Viewers:** Offer a taste of premium content to attract new subscribers.
* **Drive Promotions:** Run targeted campaigns to increase content exposure and build brand loyalty.
* **Retain Control:** Manage access periods, enforce limits, and reset access as needed to align with business goals.

TempPass feature is delivered by introducing a pseudo-MVPD (named further "Temp Pass") within the Adobe Pass Authentication server configuration as an integration with the participating Programmer. TempPass feature is available in two configurations:

* [Basic TempPass](#basic-temp-pass) for time-based access.
* [Promotional TempPass](#promotional-temp-pass) for flexible campaign-driven access.

>[!IMPORTANT]
>
> The TempPass feature is a premium feature and requires a current license from Adobe.

The following table provides a brief comparison of the Basic and Promotional TempPass features:

| **Feature**                   | **Basic TempPass**           | **Promotional TempPass**                                                                        |
|-------------------------------|------------------------------|-------------------------------------------------------------------------------------------------|
| **Access to Content**         | <ul><li>Time-based</li></ul> | <ul><li>Time-based</li><li>Limited to a maximum number of resources</li></ul>                   |
| **Access Security Based On**  | <ul><li>Device ID</li></ul>  | <ul><li>Device ID</li><li>Hash of provided user identifier information (e.g., e-mail)</li></ul> |
| **Enhanced Error Codes**      | Available                    | Available                                                                                       |
| **TempPass Reset Capability** | Available                    | Available                                                                                       |

>[!IMPORTANT]
> 
> Adobe Pass Authentication does not include a built-in mechanism to automatically halt the ongoing stream once the allotted time (X minutes) has elapsed. It is the responsibility of Programmers to enforce access restrictions once the TempPass expires during an ongoing stream.

Whether you’re providing a sneak peek of your content library or promoting a marquee event, TempPass equips you with the tools to expand your audience while maintaining control over access.

## Basic TempPass {#basic-temp-pass}

The basic TempPass feature allows Programmers to provide time-limited access to content, catering to various scenarios:

* **Short Previews:** Offer brief previews, such as a 10-minute daily access period, to attract potential subscribers.
* **Event-Based Access:** Enable longer access for major events, such as a 4-hour session.
* **Combination Access:** Mix and match durations, such as an initial extended viewing period followed by shorter daily previews over several days.

Certain events may require phased free access to content, such as an initial extended free access period (e.g., 4 hours), followed by shorter daily free access intervals (e.g., 10 minutes each day). To implement this scenario, Programmers must coordinate with their Adobe representative to configure two TempPass MVPDs tailored to their needs.

For example, to provide an initial 4-hour free session followed by daily 10-minute free sessions, Adobe can configure for the Programmer:

* **TempPass1**: Configured with a Time-To-Live (TTL) of 4 hours to cover the initial free access period.
* **TempPass2**: Configured with a Time-To-Live (TTL) of 10 minutes for the subsequent daily free access intervals.

To ensure proper functionality for daily access, TempPass2 must be reset for all devices at 00:00 hours each day.

### Feature details {#basic-temp-pass-feature-details}

**Configuration parameters:**

* **TTL (Time-To-Live):** Programmers can specify the duration of access. This clock-based TTL expires regardless of actual viewing time.

**User identification:**

The basic TempPass feature uses the device identifier as a user identification parameter.

The following table helps you understand how user identification parameters influence the user trial experience:

| Device Identifier | Result         |
|-------------------|----------------|
| New               | New trial      |
| Existing          | Existing trial |

**View time computation:**

The TTL represents the duration from the initial authorization request time to the expiration time, independent of the actual time spent viewing content. Each future request checks the current server time against the stored expiration time to authorize access.

**Authentication:**

Authentication is not required for Basic TempPass, allowing you to proceed directly to the authorization step.

**Authorization:**

As there is no interaction with an actual MVPD, the Basic "Temp Pass" MVPD will authorize any resource given the TempPass is valid. In case of a successful authorization, the Media Token Verifier library remains applicable for verifying the media token and ensuring resource validation before initiating content playback.

The authorization decision is based on the user identification parameters and the configured TTL. To obtain a successful authorization for a resource, the following conditions must be met by a valid request:

* **Unconsumed duration:** The expiration time is computed by adding the initial authorization request time (saved in our databases) to the configured TTL. The current server time is compared against this expiration time to determine if the TempPass is still valid.

In case of a user exceeding the configured TTL, they will no longer be able to view content on the same device unless their TempPass is reset.

**Preauthorization:**

When a preauthorization request is made for a Basic "Temp Pass" MVPD, the response will return the entire list of resources from the request as successfully preauthorized. This behavior reflects the authorization logic, given the authorization conditions are based on time limits, rather than specific resources. As long as the time constraint is valid, the requested resources will be authorized.

**Logout:**

Logout is not required for Basic TempPass, allowing you to switch directly to the authentication step using an actual user MVPD.

**Tracking data and analytics:**

During the basic TempPass flow, tracking data uses a hashed version of the device identifier, with the MVPD identifier set to "Temp Pass". Programmers should differentiate TempPass metrics from standard MVPD metrics in their analytics implementations.

## Promotional TempPass {#promotional-temp-pass}

The promotional TempPass feature expands the capabilities of the basic TempPass, designed specifically for running promotional campaigns. This feature lets Programmers engage users by allowing access to a predefined number of VOD titles for a specified time period after collecting valid user identification, such as an email address.

Promotional TempPass includes all the functionality of the basic TempPass, with added flexibility for:

* Defining the maximum number of VOD titles accessible during the promotional period.
* Setting the time period during which the promotional access is valid.

Once a user exceeds the predefined access limits (number of VOD titles or duration), they will no longer be able to view content on the same device or with the same user identifier unless their TempPass is reset.

### Feature details {#promotional-temp-pass-feature-details}

**Configuration parameters:**

* **User Information Key:** The key used to communicate the user-provided identifier, such as an email address (i.e., key is e-mail).
* **Number of Resources:** Defines how many VOD titles a user can access.
* **TTL (Time-To-Live):** The duration during which the user can consume the allowed resources.

**User identification:**

The Promotional TempPass feature uses the hash of the user-provided identifier on top of the device identifier as user identification parameters.

>[!IMPORTANT]
>
> The validation and hashing of user-provided identifier are managed by the Programmer, not Adobe. Adobe does not store any Personally Identifiable Information (PII). As such, the Programmer is responsible for generating and submitting a hash of the unique user-provided identifier when interacting with the Adobe Pass Authentication APIs.

Adobe recommends using the **SHA-2** family or its specific **SHA-256**, **SHA-512** functions on data before it is sent to Adobe. For example, **SHA-256** over **"user@domain.com"** is **"f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7"**.

The following table helps you understand how user identification parameters influence the user trial experience:

| User-Provided Identifier Hash | Device Identifier | Result                                                  |
|-------------------------------|-------------------|---------------------------------------------------------|
| New                           | New               | New trial                                               |
| Existing                      | New               | Existing trial (based on user-provided identifier hash) |
| New                           | Existing          | Existing trial (based on device identifier)             |
| Existing                      | Existing          | Existing trial                                          |

**View time computation:**

The TTL represents the duration from the initial authorization request time to the expiration time, independent of the actual time spent viewing content. Each future request checks the current server time against the stored expiration time to authorize access.

**Authentication:**

Authentication is not required for Promotional TempPass, allowing you to proceed directly to the authorization step.

To support the implementation of the Programmer's application, Promotional TempPass exposes the following user metadata information, accessible through corresponding keys:

* **`remaining_resources`**: Indicates the number of resources the user is still entitled to consume.
* **`used_assets`**: Provides a list of resources the user has already consumed.
* **`expiration_date`**: Displays the expiration date of the user's Promotional Temp Pass.

**Authorization:**

As there is no interaction with an actual MVPD, the Promotional "Temp Pass" MVPD will authorize any resource given the TempPass is valid. In case of a successful authorization, the Media Token Verifier library remains applicable for verifying the media token and ensuring resource validation before initiating content playback. 

The authorization decision is based on user identification parameters, and the configured number of resources and TTL. To obtain a successful authorization for a resource, the following conditions must be met by a valid request:

* **Unconsumed duration:** The expiration time is computed by adding the initial authorization request time (saved in our databases) to the configured TTL. The current server time is compared against this expiration time to determine if the TempPass is still valid.
* **Unconsumed resources:** The number of resources consumed is tracked (saved in our databases). The number of resources consumed is compared against the configured number of resources to determine if the TempPass is still valid.

In case of a user exceeding the configured TTL or number of resources, they will no longer be able to view content on the same device or with the same user-provided identifier unless their TempPass is reset.

**Preauthorization:**

When a preauthorization request is made for a Promotional "Temp Pass" MVPD, the response will return the entire list of resources from the request as successfully preauthorized. This behavior reflects the authorization logic, given the authorization conditions are based on time limits and the total number of resources accessed, rather than specific resources. As long as the time constraint is valid and the resource limit has not been exceeded, the requested resources will be authorized.

**Logout:**

Logout is not required for Promotional TempPass, allowing you to switch directly to the authentication step using an actual user MVPD.

**Tracking data and analytics:**

During the promotional TempPass flow, tracking data uses a hashed version of the device identifier, with the MVPD identifier set to "Temp Pass". Programmers should differentiate TempPass metrics from standard MVPD metrics in their analytics implementations.

## Reset TempPass API Access {#reset-tempass-api-access}

Before accessing the Reset TempPass API, you must complete the required steps in the Dynamic Client Registration (DCR) process. This mandatory process ensures you have the necessary access token to interact with the Reset TempPass API.

For comprehensive instructions, refer to the [Dynamic Client Registration Overview](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md) documentation.

## Reset TempPass API - DELETE /reset-tempass/v3/reset {#reset-tempass-v3-reset}

In order to reset a specific TempPass for a device or all devices, Adobe Pass Authentication provides Programmers with an API that works for both Basic and Promotional TempPass.

### Request {#reset-tempass-v3-reset-request}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">HTTP</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">host</td>
      <td>mgmt.auth.adobe.com</td>
      <td></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">path</td>
      <td>/reset-tempass/v3/reset</td>
      <td></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">method</td>
      <td>DELETE</td>
      <td></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Query Parameters</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">requestor_id</td>
      <td>The internal unique identifier associated with the Service Provider during onboarding process.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">mvpd_id</td>
      <td>The internal unique identifier associated with the TempPass during onboarding process.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">device_id</td>
      <td>
            The device identifier for which this reset operation is valid.
            <br/><br/>
            If no value is provided, the reset operation applies to all devices.
      </td>
      <td>optional</td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Authorization</td>
      <td>The generation of the bearer token payload is described in the <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md">Retrieve access token</a> documentation.</td>
      <td><i>required</i></td>
   </tr>
</table>

### Response {#reset-tempass-v3-reset-response}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Code</th>
      <th style="background-color: #EFF2F7;">Text</th>
      <th style="background-color: #EFF2F7;">Description</th>
   </tr>
   <tr>
      <td>204</td>
      <td>No Content</td>
      <td>
        The reset was successful.
      </td>
   </tr>
   <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        The request is invalid, the client needs to correct the request and try again.
      </td>
   </tr>
   <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        The access token is invalid, the client needs to obtain a new access token and try again. For more details refer to the <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md">Dynamic Client Registration Overview</a> documentation.
      </td>
   </tr>
   <tr>
      <td>403</td>
      <td>Forbidden</td>
      <td>
        The access token is invalid, the client needs to obtain new client credentials and a new access token and try again. For more details refer to the <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md">Dynamic Client Registration Overview</a> documentation.
      </td>
   </tr>
</table>

### Samples {#reset-tempass-v3-reset-samples}

#### Reset TempPass for a specific device {#reset-tempass-v3-reset-specific-device}

```curl

$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v3/reset?requestor_id=REF30&mvpd_id=TempPass&device_id=ba23d141-d715-561c-94f4-e9e4c966b1eb"

```

#### Reset TempPass for all devices {#reset-tempass-v3-reset-all-devices}

```curl

$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v3/reset?requestor_id=REF30&mvpd_id=TempPass&device_id=all"

```

## Reset TempPass API - DELETE /reset-tempass/v3/reset/generic {#reset-tempass-v3-reset-generic}

In order to reset a specific TempPass for a generic key (user-provided identifier hash) or all keys, Adobe Pass Authentication provides Programmers with an API that works for Promotional TempPass.

### Request {#reset-tempass-v3-reset-generic-request}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">HTTP</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">host</td>
      <td>mgmt.auth.adobe.com</td>
      <td></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">path</td>
      <td>/reset-tempass/v3/reset/generic</td>
      <td></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">method</td>
      <td>DELETE</td>
      <td></td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Query Parameters</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">requestor_id</td>
      <td>The internal unique identifier associated with the Service Provider during onboarding process.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">mvpd_id</td>
      <td>The internal unique identifier associated with the TempPass during onboarding process.</td>
      <td><i>required</i></td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">key</td>
      <td>
            The user-provided identifier hash for which this reset operation is valid.
            <br/><br/>
            If no value is provided, the reset operation applies to all users.
      </td>
      <td>optional</td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;">Headers</th>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;"></th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;">Authorization</td>
      <td>The generation of the bearer token payload is described in the <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md">Retrieve access token</a> documentation.</td>
      <td><i>required</i></td>
   </tr>
</table>

### Response {#reset-tempass-v3-reset-generic-response}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Code</th>
      <th style="background-color: #EFF2F7;">Text</th>
      <th style="background-color: #EFF2F7;">Description</th>
   </tr>
   <tr>
      <td>204</td>
      <td>No Content</td>
      <td>
        The reset was successful.
      </td>
   </tr>
   <tr>
      <td>400</td>
      <td>Bad Request</td>
      <td>
        The request is invalid, the client needs to correct the request and try again.
      </td>
   </tr>
   <tr>
      <td>401</td>
      <td>Unauthorized</td>
      <td>
        The access token is invalid, the client needs to obtain a new access token and try again. For more details refer to the <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md">Dynamic Client Registration Overview</a> documentation.
      </td>
   </tr>
   <tr>
      <td>403</td>
      <td>Forbidden</td>
      <td>
        The access token is invalid, the client needs to obtain new client credentials and a new access token and try again. For more details refer to the <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md">Dynamic Client Registration Overview</a> documentation.
      </td>
   </tr>
</table>

### Samples {#reset-tempass-v3-reset-generic-samples}

#### Reset TempPass for a specific key {#reset-tempass-v3-reset-specific-key}

```curl

$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v3/reset/generic?requestor_id=REF30&mvpd_id=TempPass&key=f7ee5ec7312165148b69fcca1d29075b14b8aef0b5048a332b18b88d09069fb7"

```

#### Reset TempPass for all keys {#reset-tempass-v3-reset-all-keys}

```curl

$ curl -H "Authorization: Bearer <access_token_here>" -X DELETE -v "https://mgmt.auth.adobe.com/reset-tempass/v3/reset/generic?requestor_id=REF30&mvpd_id=TempPass&key=all"

```

## REST API V2 {#rest-api-v2}

Leveraging the TempPass feature requires implementing code updates to modify how your TV Everywhere (TVE) application interacts with the Adobe Pass Authentication [REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md).

For a comprehensive guide on these updates and the associated workflows, refer to the [Temporary Access Flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/temporary-access-flows/rest-api-v2-access-temporary-flows.md) documentation.
