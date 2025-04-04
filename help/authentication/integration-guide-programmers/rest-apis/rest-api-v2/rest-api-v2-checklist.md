---
title: REST API V2 Checklist
description: REST API V2 Checklist
---
# REST API V2 Checklist {#rest-api-v2-checklist}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This document aggregates in one place the mandatory requirements and recommended practices for Programmers implementing client applications that consume Adobe Pass Authentication [REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md).

Following this document must be considered part of your acceptance criteria when implementing the REST API V2 and must be used as a checklist to ensure that all necessary steps have been taken to obtain a successful integration.

## Mandatory Requirements {#mandatory-requirements}

### 1. Registration Phase {#mandatory-requirements-registration-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Requirements</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Registered Application Scoping</i></td>
      <td>Use a registered application with REST API v2 scope.</td>
      <td>Risks triggering HTTP 401 "Unauthorized" error responses, overloading system resources and increasing latency.</td>
   </tr>
    <tr>
      <td style="background-color: #DEEBFF;"><i>Client Credentials Caching</i></td>
      <td>Store the client credentials in persistent storage and reuse them for every access token request.</td>
      <td>Risks authentication loss when the client credentials are regenerated.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Access Tokens Caching</i></td>
      <td>Store the access tokens in persistent storage and reuse them until they expire — do not request a new token for every REST API v2 call.</td>
      <td>Risks overloading system resources, increasing latency, and potentially triggering HTTP 429 "Too Many Requests" error responses.</td>
   </tr>
</table>

### 2. Configuration Phase {#mandatory-requirements-configuration-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Requirements</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Configuration Retrieval</i></td>
      <td>Retrieve the configuration response only when requiring to prompt the user to select their MVPD (TV provider) prior to the Authentication Phase.<br/><br/>There is no need to retrieve the configuration response when:<ul><li>The user is already authenticated.</li><li>The user is offered temporary access.</li><li>The user authentication has expired, but the user can be prompted to confirm they are still a subscriber of the previously selected MVPD.</li></ul></td>
      <td>Risks overloading system resources and increasing latency.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>TV Provider Selection Caching</i></td>
      <td>Store the user's Pay TV provider (MVPD) selection in persistent storage to use it in all subsequent phases:<ul><li>From configuration response store the user selected MVPD "id".</li><li>From configuration response store the user selected MVPD "displayName".</li><li>From configuration response store the user selected MVPD "logoUrl".</li></ul></td>
      <td>Risks overloading system resources and increasing latency.</td>
   </tr>
</table>

### 3. Authentication Phase {#mandatory-requirements-authentication-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Requirements</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Polling Mechanism Starting</i></td>
      <td>Start the polling mechanism under the following conditions:<br/><br/><b><a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md">Authentication performed within the primary (screen) application</a></b><ul><li>The primary (streaming) application should start polling when the user reaches the final destination page, after the browser component loads the URL specified for the "redirectUrl" parameter in the Sessions endpoint request.</li></ul><br/><b><a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md">Authentication performed within a secondary (screen) application</a></b><ul><li>The primary (streaming) application should start polling as soon as the user initiates the authentication process—right after receiving the Sessions endpoint response and displaying the authentication code to the user.</li></ul></td>
      <td>Risks overloading system resources, increasing latency, and potentially triggering HTTP 429 "Too Many Requests" error responses.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Polling Mechanism Stopping</i></td>
      <td>Stop the polling mechanism under the following conditions:<br/><br/><b>Successful authentication</b><ul><li>The user's profile information is successfully retrieved, confirming their authentication status, therefore polling is no longer needed.</li></ul><br/><b>Authentication session and code expiry</b><ul><li>The authentication session and code expire, the user must restart the authentication process, and polling using the previous authentication code should be stopped immediately.</li></ul><br/><b>New authentication code generated</b><ul><li>If the user requests a new authentication code, then the existing session is invalidated, and polling using the previous authentication code should be stopped immediately.</li></ul></td>
      <td>Risks overloading system resources, increasing latency, and potentially triggering HTTP 429 "Too Many Requests" error responses.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Polling Mechanism Configuring</i></td>
      <td>Configure the polling mechanism frequency under the following conditions:<br/><br/><b><a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md">Authentication performed within the primary (screen) application</a></b><ul><li>The primary (streaming) application should poll every 3-5 seconds.</li></ul><br/><b><a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md">Authentication performed within a secondary (screen) application</a></b><ul><li>The primary (streaming) application should poll every 3-5 seconds.</li></ul></td>
      <td>Risks overloading system resources, increasing latency, and potentially triggering HTTP 429 "Too Many Requests" error responses.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Profiles Caching</i></td>
      <td>Store parts of the user's profile information in persistent storage to improve performance and minimize unnecessary REST API v2 calls.<br/><br/>Caching should focus on the following profiles response fields:<br/><br/><b>mvpd</b><ul><li>The client application can use this to keep track of the user's selected TV provider and continue to use it further during Preauthorization or Authorization Phases.</li><li>When the current user profile expires, the client application can use the remembered MVPD selection and just ask the user to confirm.</li></ul><br/><b>attributes</b><ul><li>Used to personalize the user experience based on different user metadata keys (e.g., zip, maxRating, etc.).</li><li>User metadata becomes available after the authentication flow completes, therefore the client application does not need to query a separate endpoint to retrieve the user metadata information, as it is already included in the profile information.</li><li>Certain metadata attributes may be updated during the Authorization Phase, depending on the MVPD (e.g., Charter) and the specific metadata attribute (e.g., householdID). As a result, the client application may need to query the Profiles APIs again after authorization to retrieve the latest user metadata.</li></ul></td>
      <td>Risks overloading system resources, increasing latency, and potentially triggering HTTP 429 "Too Many Requests" error responses.</td>
   </tr>
</table>

### 4. (Optional) Preauthorization Phase {#mandatory-requirements-preauthorization-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Requirements</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Preauthorization Decisions Retrieval</i></td>
      <td>Use preauthorization decisions for content filtering and never for playback decisions.</td>
      <td>Risks breaching contractual agreements between Programmer, MVPDs and Adobe.<br/><br/>Risks bypassing our monitoring and alerting systems.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Preauthorization Decisions Retrieval Retry</i></td>
      <td>Handle the <a href="/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md">enhanced error codes</a> appropriately and utilize the action field to determine the necessary remediation steps.<br/><br/>Only a limited number of enhanced error codes warrant a retry, while most require alternative resolutions as specified in the action field.<br/><br/>Ensure that any retry mechanism implemented for retrieving preauthorization decisions does not result in an endless loop and that it limits retries to a reasonable number (i.e., 2-3).</td>
      <td>Risks overloading system resources, increasing latency, and potentially triggering HTTP 429 "Too Many Requests" error responses.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Preauthorization Decisions Caching</i></td>
      <td>Cache successful permit decisions in memory to improve performance and minimize unnecessary REST API v2 calls, as subscription updates while the application is running are infrequent.</td>
      <td>Risks overloading system resources, increasing latency, and potentially triggering HTTP 429 "Too Many Requests" error responses.</td>
   </tr>
</table>

### 5. Authorization Phase {#mandatory-requirements-authorization-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Requirements</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Authorization Decisions Retrieval</i></td>
      <td>Obtain authorization decisions before playback — regardless if a preauthorization decision exists.<br/><br/>Allow streams to continue uninterrupted even if the media token expires during playback and request a new authorization decision containing a (fresh) media token when the user makes their next playback request, regardless it is for the same or a different resource.<br/><br/>Live streams running for extended periods of time may choose to request a new authorization decision following video operations such as pausing content, initiating commercial breaks, or modifying asset-level configurations when the MRSS undergoes changes.</td>
      <td>Risks breaching contractual agreements between Programmer, MVPDs and Adobe.<br/><br/>Risks bypassing our monitoring and alerting systems.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Authorization Decisions Retrieval Retry</i></td>
      <td>Handle the <a href="/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md">enhanced error codes</a> appropriately and utilize the action field to determine the necessary remediation steps.<br/><br/>Only a limited number of enhanced error codes warrant a retry, while most require alternative resolutions as specified in the action field.<br/><br/>Ensure that any retry mechanism implemented for retrieving authorization decisions does not result in an endless loop and that it limits retries to a reasonable number (i.e., 2-3).</td>
      <td>Risks overloading system resources, increasing latency, and potentially triggering HTTP 429 "Too Many Requests" error responses.</td>
   </tr>
</table>

### 6. Logout Phase {#mandatory-requirements-logout-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Requirements</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Logout Support</i></td>
      <td>Implement the logout API to allow users to manually sign out, terminating their authenticated profile and follow the REST API v2 action name specified for each removed profile:<ul><li>For MVPDs supporting a logout endpoint the client application requires to navigate to the provided "url" in a user-agent.</li><li>For "appleSSO" type profiles, the client application requires to guide the user to also log out from the partner level (Apple’s system settings).</li></ul></td>
      <td>Risks client application malfunction due to missing support on client application side.</td>
   </tr>
</table>

### 7. Parameters and Headers {#mandatory-requirements-parameters-headers}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Requirements</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Send Authorization Header</i></td>
      <td>Send the <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-authorization.md">Authorization</a> header for every REST API v2 request.</td>
      <td>Risks triggering HTTP 401 "Unauthorized" error responses, overloading system resources and increasing latency.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Send AP-Device-Identifier Header</i></td>
      <td>Send the <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-device-identifier.md">AP-Device-Identifier</a> header for every REST API v2 request.<br/><br/>Even when the request originates from a server on behalf of a device, the AP-Device-Identifier header value must reflect the actual streaming device identifier.</td>
      <td>Risks triggering HTTP 400 "Bad Request" error responses, overloading system resources and increasing latency.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Send X-Device-Info Header</i></td>
      <td>Send the <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-x-device-info.md">X-Device-Info</a> header for every REST API v2 request.<br/><br/>Even when the request originates from a server on behalf of a device, the X-Device-Info header value must reflect the actual streaming device information.</td>
      <td>Risks being classified as originating from an unknown platform and treated as insecure, becoming subject to more restrictive rules, such as shorter authentication TTLs.<br/><br/>Additionally, some fields, such as the streaming device connectionIp and connectionPort, are mandatory for features like Spectrum’s Home Base Authentication.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Stable Device Identifier</i></td>
      <td>Compute and store a stable device identifier that does not change across updates or reboots for the <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-device-identifier.md">AP-Device-Identifier</a> header.<br/><br/>For platforms without a hardware identifier, generate a unique identifier from application attributes and persist it.</td>
      <td>Risks authentication loss when the device identifier changes.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Follow APIs References</i></td>
      <td>Ensure you are sending only REST API v2 expected parameters and headers.</td>
      <td>Risks triggering HTTP 400 "Bad Request" error responses, overloading system resources and increasing latency.</td>
   </tr>
</table>

### 8. Error Handling {#mandatory-requirements-error-handling}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Requirements</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Enhanced Error Code Handling Support</i></td>
      <td>Handle the <a href="/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md">enhanced error codes</a> appropriately and utilize the action field to determine the necessary remediation steps.<br/><br/>Only a limited number of enhanced error codes warrant a retry, while most require alternative resolutions as specified in the action field.<br/><br/>Most enhanced error codes listed in the <a href="/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md#enhanced-error-codes-lists-rest-api-v2">Enhanced Error Codes - REST API V2</a> documentation can be prevented entirely if correctly handled during development phase before launching the application.</td>
      <td>Risks overloading system resources, increasing latency, and potentially triggering HTTP 429 "Too Many Requests" error responses.<br/><br/>Risks client application malfunction due to missing handling of the enhanced error codes — causing unclear error messages, improper user guidance, or incorrect fallback behavior.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>HTTP Error Handling Support</i></td>
      <td>Differentiate between handling HTTP error responses (e.g., 400, 401, 403, 404, 405, 500) and success responses (e.g., 200, 201) that contain enhanced error codes payloads, as discussed above.<br/><br/>Only a limited number of HTTP error codes warrant a retry, while most require alternative resolutions.<br/><br/>Most HTTP error responses can be prevented entirely if correctly handled during development phase before launching the application.</td>
      <td>Risks overloading system resources, increasing latency, and potentially triggering HTTP 429 "Too Many Requests" error responses.<br/><br/>Risks client application malfunction due to missing handling of the enhanced error codes — causing unclear error messages, improper user guidance, or incorrect fallback behavior.</td>
   </tr>
</table>

### 9. Testing {#mandatory-requirements-testing}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Requirements</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Lifecycle Testing</i></td>
      <td>Develop and test the application using the official Adobe Pass Authentication non-production environments:<ul><li>Prequal-Production</li><li>Release-Staging</li></ul><br/>Perform thorough quality assurance (QA) in these environments before launching to Release-Production.<br/><br/>Client applications must not proceed to Release-Production without first completing end-to-end validation in non-production environments.</td>
      <td>Risks launching with critical and major defects.<br/><br/>Lacking a short and efficient debugging path can hinder Adobe Support and Engineering from intervening quickly.</td>
   </tr>
</table>

## Recommended Practices {#recommended-practices}

### 1. Registration Phase {#recommended-practices-registration-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Practices</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Access Tokens Validation</i></td>
      <td>Proactively check access token validity and refresh it when expired.<br/><br/>Ensure that any retry mechanism for handling HTTP 401 "Unauthorized" errors first refreshes the access token before retrying the original request.</td>
      <td>Risks triggering HTTP 401 "Unauthorized" error responses, overloading system resources and increasing latency.</td>
   </tr>
</table>

### 2. Configuration Phase {#recommended-practices-configuration-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Practices</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Configuration Caching</i></td>
      <td>Store the configuration response in memory or persistent storage for a short period of time (e.g. 3-5 minutes) to improve performance and minimize unnecessary REST API v2 calls.</td>
      <td>Risks overloading system resources and increasing latency.</td>
   </tr>
</table>

### 3. Authentication Phase {#recommended-practices-authentication-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Practices</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Authentication Code Validation (2nd screen authentication)</i></td>
      <td>Validate authentication code submitted through user input on the secondary (2nd) application (screen) before calling /api/v2/authenticate API under the following conditions:<br/><br/><b><a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md#perform-authentication-within-secondary-application-with-preselected-mvpd">Authentication performed within secondary (screen) application with preselected mvpd</a></b><ul><li>Make use of <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md">Resume authentication session</a> - POST /api/v2/{serviceProvider}/sessions/{code}</li></ul><br/><b><a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md#perform-authentication-within-secondary-application-without-preselected-mvpd">Authentication performed within secondary (screen) application without preselected mvpd</a></b><ul><li>Make use of <a href="/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md">Retrieve authentication session</a> - GET /api/v2/{serviceProvider}/sessions/{code}</li></ul><br/>The client application would receive an error if the provided authentication code was typed wrong or in case the authentication session would be expired.</td>
      <td>Risks various error responses and work flow issues during authentication.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Multiple Profiles Support</i></td>
      <td>Ensure client application can handle multiple profiles by either prompting the user to select a profile or applying custom logic, such as automatically selecting the profile with the longest validity period.</td>
      <td>Risks client application malfunction due to missing support on client application side.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>(Optional) Non-Basic Flows Support</i></td>
      <td>Support non-basic flows in case the client application business requires:<ul><li>Degraded access flows (premium feature)</li><li>Temporary access flows (premium feature)</li><li>Single sign-on access flows (standard feature)</li></ul></td>
      <td>Risks creating a less than ideal user experience.</td>
   </tr>
</table>

### 4. (Optional) Preauthorization Phase {#recommended-practices-preauthorization-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Practices</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>User Experience</i></td>
      <td>Display clear user feedback if a preauthorization decision is denied, using messaging provided by MVPDs or Adobe via enhanced error codes.</td>
      <td>Risks creating a less than ideal user experience.</td>
   </tr>
</table>

### 5. Authorization Phase {#recommended-practices-authorization-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Practices</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Media Tokens Validation</i></td>
      <td>Validate media tokens using the <a href="/help/authentication/integration-guide-programmers/features-standard/entitlements/media-tokens.md#media-token-verifier">Media Token Verifier</a> library.</td>
      <td>Risks fraud schemes such as stream ripping.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>User Experience</i></td>
      <td>Display clear user feedback if an authorization decision is denied, using messaging provided by MVPDs or Adobe via enhanced error codes.</td>
      <td>Risks creating a less than ideal user experience.</td>
   </tr>
</table>

### 6. Logout Phase {#recommended-practices-logout-phase}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Practices</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>User Experience</i></td>
      <td>Avoid automatically (programmatically) calling the logout API in scenarios like denied preauthorization or authorization, as the logout API should only be invoked in response to a direct user request.</td>
      <td>Risks confusing the user that the authentication is failing.</td>
   </tr>
</table>

### 7. Parameters and Headers {#recommended-practices-parameters-headers}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Practices</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Reuse Code</i></td>
      <td>Reuse code from REST API v1 for computing the device identifier and device information with minor adjustments, but ensure you are sending only REST API v2 expected parameters and headers.<br/><br/>Reuse code from REST API v1 for calling the DCR API to retrieve an access token.</td>
      <td>-</td>
   </tr>
</table>

### 8. Testing {#recommended-practices-testing}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Practices</th>
      <th style="background-color: #EFF2F7;">Risks</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Test Coverage</i></td>
      <td>Ensure the following basic flows are tested across devices and platforms:<br/><br/><b>Authentication flows</b><ul><li>Primary application (screen) authentication scenario</li><li>Secondary application (screen) authentication scenario</li></ul><br/><b>(Optional) Preauthorization flows</b><ul><li>Test permit decisions scenario</li><li>Test deny decisions scenario</li></ul><br/><b>Authorization flows</b><ul><li>Test permit decisions scenario</li><li>Test deny decisions scenario</li></ul><br/><b>Logout flows</b><br/><br/>Additionally, test other access flows, if applicable:<br/><br/><ul><li>Degraded access flows (premium feature)</li><li>Temporary access flows (premium feature)</li><li>Single sign-on access flows (standard feature)</li></ul><br/>Cover top MVPD integrations (covering the most widely used providers).</td>
      <td>Risks unforeseen failures in production, especially across less frequently tested platforms or rare flows like negative scenarios.</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Test Tools</i></td>
      <td>Use the <a href="https://developer.adobe.com/adobe-pass/">Adobe Developer</a> website.</td>
      <td>-</td>
   </tr>
</table>

## Summary {#summary}

<table style="table-layout:auto">
   <tr>
      <th style="background-color: #EFF2F7;">Phase</th>
      <th style="background-color: #EFF2F7;">Mandatory</th>
      <th style="background-color: #EFF2F7;">(Strongly) Recommended</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Registration</i></td>
      <td>Cache client credentials<br/><br/>Cache access tokens</td>
      <td>Validate and refresh access tokens</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Configuration</i></td>
      <td>Minimize configuration response retrievals</td>
      <td>Cache configuration response</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Authentication</i></td>
      <td>Polling mechanism fine tuning<br/><br/>Cache parts of profiles</td>
      <td>Support multiple profiles<br/><br/>Support Degradation Feature (if business requirement)<br/><br/>Support TempPass Feature (if business requirement)<br/><br/>Support Single Sign-On Feature (if business requirement)</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Preauthorization</i></td>
      <td>Cache permit preauthorization decisions<br/><br/>Retry mechanism fine tuning</td>
      <td>Enhance user experience using error codes for denied preauthorization decisions</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Authorization</i></td>
      <td>Retrieve authorization decision when user requests for playback<br/><br/>Retry mechanism fine tuning</td>
      <td>Enhance user experience using error codes for denied authorization decisions<br/><br/>Media token validation</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Logout</i></td>
      <td>Implement the logout API to allow users to manually sign out</td>
      <td>Avoid automatically calling the logout API</td>
   </tr>
   <tr>
      <th style="background-color: #EFF2F7;"></th>
      <th style="background-color: #EFF2F7;">Mandatory</th>
      <th style="background-color: #EFF2F7;">(Strongly) Recommended</th>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Parameters & Headers</i></td>
      <td>Follow mandatory headers specifications</td>
      <td>Reuse code from REST API v1</td>
   </tr>
   <tr>
      <td style="background-color: #DEEBFF;"><i>Error Handling</i></td>
      <td>Implement enhanced error handling<br/><br/>Implement HTTP error handling</td>
      <td>-</td>
   </tr>
</table>
