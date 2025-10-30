---
title: REST API V2 Cookbook (Client-to-Server)
description: REST API V2 Cookbook (Client-to-Server)
exl-id: 6a5a89d2-ea54-4f9c-9505-e575ced4301c
---
# REST API V2 Cookbook (Client-to-Server) {#rest-api-v2-cookbook-client-to-server}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

The document is intended for developers who are integrating [Adobe Pass Authentication REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md) into their streaming applications having a Client-to-Server (C2S) architecture.

## Prerequisites {#prerequisites}

For terms and definitions, refer to the [REST API V2 Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md) documentation.

For mandatory requirements and recommended practices, refer to the [REST API V2 Checklist](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-checklist.md) documentation.

For frequently asked questions, refer to the [REST API V2 FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md) documentation.

## A. Registration Phase {#registration-phase}

The purpose of the Registration Phase is to register the streaming application against Adobe Pass Authentication through the Dynamic Client Registration (DCR) process.

The Dynamic Client Registration (DCR) process requires the streaming application to obtain a pair of client credentials and retrieve an access token as the end goal of the Registration Phase.

The Registration Phase is mandatory, but the streaming application can skip this phase if it has a cached pair of client credentials and an access token that are still valid.

+++Related Articles

**APIs:**

* [Retrieve client credentials](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-client-credentials.md)
* [Retrieve access token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md)

**Flows:**

* [Dynamic Client Registration Flow](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/flows/dynamic-client-registration-flow.md)

**FAQs:**

* [Registration Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-faqs.md)

+++

### Step 1: Register your application {#step-1-register-your-application}

* **Retrieve client credentials:** The streaming application retrieves client credentials by calling the [**/o/client/register**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-client-credentials.md) endpoint.

  * The streaming application must store the client credentials and use them indefinitely when needing to retrieve an access token.


* **Retrieve access token:** The streaming application retrieves access token by calling the [**/o/client/token**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md) endpoint.

  * The streaming application must store and use the access token until it expires, then discard it and obtain a new one.

## B. Authentication Phase {#authentication-phase}

The purpose of the Authentication Phase is to provide the streaming application the capability to verify the user's identity and obtain user metadata information.

The Authentication Phase acts as a prerequisite step for the Preauthorization Phase or Authorization Phase when the streaming application needs to play content.

+++Related Articles

**APIs**

* [Create authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md)
* [Resume authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md)
* [Retrieve authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md)
* [Perform authentication in user agent](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)
* [Retrieve profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)
* [Retrieve profile for specific mvpd](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md)
* [Retrieve profile for specific code](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md)

**Flows**

* [Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)
* [Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)
* [Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)
* [Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)

**FAQs**

* [Authentication Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authentication-phase-faqs-general)

+++

### Step 2: Check for existing authenticated profiles {#step-2-check-for-existing-authenticated-profiles}

* **Retrieve profiles:** The streaming application checks for existing profiles by calling the [**/api/v2/{serviceProvider}/profiles**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) endpoint.


* **Scenario 1:** There are existing profiles, the streaming application may proceed to the [Preauthorization Phase](#preauthorization-phase) or [Authorization Phase](#authorization-phase).


* **Scenario 2:** There are no existing profiles, the streaming application may proceed to the next step to [Authenticate the user](#step-3-authenticate-the-user).


* **Scenario 3:** There are no existing profiles, the streaming application may proceed to provide the user with temporary access through the [TempPass](/help/premium-workflow/temporary-access/temp-pass-feature.md) feature.

  * This scenario is outside the scope of this document, refer to the [Temporary Access Flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/temporary-access-flows/rest-api-v2-access-temporary-flows.md) documentation for more information.

### Step 3: Authenticate the user {#step-3-authenticate-the-user}

* **Retrieve configuration:** The streaming application retrieves the list of available MVPDs by calling the [**/api/v2/{serviceProvider}/configuration**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md) endpoint.

  * The streaming application can implement a custom filtering mechanism to refine the list of MVPDs from the configuration response, displaying only the intended providers while hiding others (e.g., MVPDs under development, test MVPDs, TempPass). This ensures that users are presented with a curated selection when choosing their TV provider.


* **Create authentication session:** The streaming application initiates an authentication session by calling the [**/api/v2/{serviceProvider}/sessions**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint.


* **Scenario 1:** The streaming application can open a browser or webview, therefore it must load the authentication `url`.

  * The user submits their username and password within the MVPD login page. Upon successful authentication the final redirect displays a success page.


* **Scenario 2:** The streaming application cannot open a browser, therefore it must display the authentication `code`. A separate web application is required to prompt the user to enter the `code`, construct the authentication `url` and open: [**/api/v2/authenticate/{serviceProvider}/{code}**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md).

  * The user submits their username and password within the MVPD login page. Upon successful authentication the final redirect displays a success page.

### Step 4: Check for authenticated profiles {#step-4-check-for-authenticated-profiles}

* **Retrieve profile for specific code:** The streaming application must implement a polling mechanism using the `code` to check if the profile was successfully generated and saved by calling the [**/api/v2/{serviceProvider}/profiles/code/{code}**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) endpoint.

  * The streaming application must **start the polling** mechanism under the following conditions:

    * **Authentication performed within the primary (screen) application:** The primary (streaming) application should start polling when the user reaches the final destination page, after the browser component loads the URL specified for the `redirectUrl` parameter in the [Sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint request.

    * **Authentication performed within a secondary (screen) application:** The primary (streaming) application should start polling as soon as the user initiates the authentication process—right after receiving the [Sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint response and displaying the authentication code to the user.

  * The streaming application must **stop the polling** mechanism under the following conditions:

    * **Successful authentication:** The user's profile information is successfully retrieved, confirming their authentication status. At this point, polling is no longer needed.

    * **Authentication session and code expiry:** The authentication session and code expire, as indicated by the `notAfter` timestamp (e.g., 30 minutes) in the [Sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint response. If this happens, the user must restart the authentication process, and polling using the previous authentication code should be stopped immediately.

    * **New authentication code generated:** If the user requests a new authentication code on the primary (screen) device, the existing session is no longer valid, and polling using the previous authentication code should be stopped immediately.

  * The streaming application must **configure the polling** mechanism frequency under the following conditions:

    * **Authentication performed within the primary (screen) application:** The primary (streaming) application should poll every 3-5 seconds or more.

    * **Authentication performed within a secondary (screen) application:** The primary (streaming) application should poll every 3-5 seconds or more.

  * The streaming application should cache parts of the user's profile information in a persistent storage to avoid unnecessary requests and improve the user experience.

## C. (Optional) Preauthorization Phase {#preauthorization-phase}

The purpose of the Preauthorization Phase is to provide the streaming application the capability to present a subset of resources from its catalog that the user would be entitled to access.

The Preauthorization Phase can enhance the user experience when the user opens the streaming application for the first time or navigates to a new section.

The Preauthorization Phase is not mandatory, the streaming application can skip this phase if it wants to present a catalog of resources without filtering them first based on the user's entitlement.

+++Related Articles

**APIs**

* [Retrieve preauthorization decisions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md)

**Flows**

* [Basic preauthorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)

**FAQs**

* [Preauthorization Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#preauthorization-phase-faqs-general)

+++

### Step 5: Check for preauthorized resources {#step-5-check-for-preauthorized-resources}

* **Retrieve preauthorization decisions:** The streaming application retrieves preauthorization decisions for a list of resources by calling the [**/api/v2/{serviceProvider}/decisions/preauthorize/{mvpd}**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) endpoint.

  * The streaming application is not required to store preauthorization decisions in persistent storage. However, it is recommended to cache permit decisions in memory to improve the user experience. This helps avoid unnecessary calls for resources that have already been preauthorized, reducing latency and improving performance.

  * The streaming application can determine the reason for a denied preauthorization decision by inspecting the [error code and message](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md) included in the response from the Decisions Preauthorize endpoint. These details provide insight into the specific reason the preauthorization request was denied, helping to inform the user experience or trigger any necessary handling in the application. Ensure that any retry mechanism implemented for retrieving preauthorization decisions does not result in an endless loop if the preauthorization decision is denied. Consider limiting retries to a reasonable number and handling denials gracefully by surfacing clear feedback to the user.

  * The streaming application can obtain a preauthorization decision for a limited number of resources in a single API request, usually up to 5, due to conditions imposed by MVPDs. This maximum number of resources can be viewed and changed after agreeing with MVPDs through the Adobe Pass [TVE Dashboard](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#tve-dashboard) by one of your organization administrators or by an Adobe Pass Authentication representative acting on your behalf.


## D. Authorization Phase {#authorization-phase}

The purpose of the Authorization Phase is to provide the streaming application the capability to play resources the user requests after validating their rights with the MVPD.

The Authorization Phase is mandatory, the streaming application cannot skip this phase if it wants to play resources the user requests, as it requires verifying with the MVPD that the user is entitled before releasing the stream.

+++Related Articles

**APIs**

* [Retrieve authorization decisions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md)

**Flows**

* [Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)

**FAQs**

* [Authorization Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authorization-phase-faqs-general)

+++

### Step 6: Check for authorized resources {#step-6-check-for-authorized-resources}

* **Retrieve authorization decision:** The streaming application retrieves authorization decision for a specific resource by calling the [**/api/v2/{serviceProvider}/decision/authorize/{mvpd}**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) endpoint.

  * The streaming application is not required to store authorization decisions in persistent storage.

  * The streaming application can determine the reason for a denied authorization decision by inspecting the [error code and message](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md) included in the response from the Decisions Authorize endpoint. These details provide insight into the specific reason the authorization request was denied, helping to inform the user experience or trigger any necessary handling in the application. Ensure that any retry mechanism implemented for retrieving authorization decisions does not result in an endless loop if the authorization decision is denied. Consider limiting retries to a reasonable number and handling denials gracefully by surfacing clear feedback to the user.

  * The streaming application is not required to refresh an expired media token while the stream is actively playing. If the media token expires during playback, the stream should be allowed to continue uninterrupted. However, the client must request a new authorization decision — and obtain a new media token — the next time the user attempts to play a resource.

  * The streaming application can obtain an authorization decision for a limited number of resources in a single API request, usually up to 1, due to conditions imposed by MVPDs.

## E. Logout Phase {#logout-phase}

The purpose of the Logout Phase is to provide the streaming application the capability to terminate the user's authenticated profile within Adobe Pass Authentication upon user request.

The Logout Phase is mandatory, the streaming application must provide the user with the capability to log out.

+++Related Articles

**APIs**

* [Initiate logout for specific mvpd](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md)

**Flows**

* [Basic logout flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-logout-primary-application-flow.md)

**FAQs**

* [Logout Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#logout-phase-faqs-general)

+++

### Step 7: Logout {#step-7-logout}

* **Initiate Adobe Pass logout:** The streaming application initiates the logout flow by calling the [**/api/v2/{serviceProvider}/logout/{mvpd}**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) endpoint.

  * The streaming application must follow the instructions provided in the `actionName` and `actionType` attributes of the Logout endpoint response to ensure the logout process is completed correctly.

    * If the `actionType` attribute in the response is set to "interactive":

      * **Scenario 1:** The streaming application can open a browser or webview, therefore it must load the logout `url`.  

      * **Scenario 2:** The streaming application cannot open a browser, therefore the logout process can be stopped as the MVPD session was not persisted in a streaming device browser cache.
