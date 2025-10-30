---
title: REST API V2 Cookbook (Server-to-Server)
description: REST API V2 Cookbook (Server-to-Server)
exl-id: 3160c03c-849d-4d39-95e5-9a9cbb46174d
---
# REST API V2 Cookbook (Server-to-Server) {#rest-api-v2-cookbook-server-to-server}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> REST API V2 implementation is bounded by the [Throttling mechanism](/help/authentication/integration-guide-programmers/throttling-mechanism.md) documentation.

The document is intended for developers who are integrating [Adobe Pass Authentication REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md) into their streaming applications having a Server-to-Server (S2S) architecture.

## Prerequisites {#prerequisites}

For terms and definitions, refer to the [REST API V2 Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md) documentation.

For mandatory requirements and recommended practices, refer to the [REST API V2 Checklist](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-checklist.md) documentation.

For frequently asked questions, refer to the [REST API V2 FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md) documentation.

### Components {#components}

Before getting started, ensure you have an understanding of the following components and terms used in the workflow:

| Type                      | Component               | Description                                                                                                                                                  |
|---------------------------|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Adobe Infrastructure      | Adobe Pass Service      | Integrates with the MVPD IdP and AuthZ Service to provide authentication and authorization decisions.                                                        |
| Programmer Infrastructure | Programmer Service      | Connects the Streaming Device with Adobe Pass Service to obtain authenticated profiles and authorization decisions.                                          |
| MVPD Infrastructure       | MVPD IdP Service        | MVPD endpoint responsible for credential-based authentication, validating the user's identity.                                                               |
|                           | MVPD AuthZ Service      | MVPD endpoint that determines authorization decisions based on user subscriptions, parental controls, and other entitlement rules.                           |
| Streaming Device          | Streaming App           | The Programmer’s application that runs on the user’s streaming device and plays authenticated video content.                                                 |
|                           | (Optional) AuthN Module | If the Streaming Device has a user-agent (e.g., browser), the AuthN Module handles user authentication on the MVPD IdP.                                      |
| (Optional) AuthN Device   | AuthN App               | If the Streaming Device lacks a user-agent (e.g., browser), the AuthN Application is a Programmer web app accessed from a separate device via a web browser. |

### Requirements {#requirements}

In Server-to-Server (S2S) implementations, the Streaming App and the Programmer Service must establish a protocol that enables the Programmer Service to:

* Communicate with Adobe Pass Service on behalf of the Streaming App.

* Collect and pass a unique device identifier for the Streaming Device as required by the [AP-Device-Identifier](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-device-identifier.md) header.

* Collect and pass accurate Streaming Device information, including the source port and device-specific details, as required by the [X-Device-Info](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-x-device-info.md) header.

* Collect and pass the Streaming Device IP address as required by the X-Forwarded-For header.

* Securely store parameters such as device ID, client ID, and client secret in either the Streaming App or the Programmer Service.

* Format and send data in compliance with MVPDs and integrated apps, including device IP, source port, device-specific information, MRSS, and optional identifiers such as ECID.

* Maintain and securely manage certificates shared with Adobe for encrypted user metadata transmission.

* Respect authentication profile and authorization decision validity when caching, ensuring authentication and authorization states are invalidated when notified.

* Return authorization decisions and relevant instructions to the Streaming App.

### Environments {#environments}

Before going into the workflow, ensure you maintain at least two environments: Production and Staging.

**Production**

The production environment must be highly available and scaled appropriately to handle large or unexpected traffic spikes, such as those caused by live sports events or breaking news.

* The Adobe Pass Service operates across multiple geographically dispersed data centers throughout the US to optimize performance and minimize latency.

    * The Programmer Service should adopt a similar infrastructure strategy, ensuring low-latency response times from Adobe Pass.

* The Programmer must provide the public IP range of its production environment.

  * These IPs will be added to an allowlist within the Adobe Pass Infrastructure.

* The Programmer Service must limit DNS caching to a maximum of 30 seconds to allow for dynamic rerouting in case Adobe needs to redirect traffic due to a data center becoming unavailable.

**Staging**

The staging environment can be minimal but should mirror production by including all critical system components and business logic.

* It must allow for testing releases before deployment to production.

* It should remain operationally similar to production, enabling realistic testing.

* Ideally, the staging environment should be connected to Adobe Pass testing environments to:

  * Allow Programmers to test against Adobe’s Infrastructure.

  * Enable Adobe to assist with testing and troubleshooting when necessary.

## Workflow {#workflow}

Perform the below steps as shown in the following diagram.

![REST API V2 Cookbook (Server-to-Server)](/help/authentication/assets/rest-api-v2/cookbooks/rest-api-v2-cookbook-server-to-server-diagram.png)

*REST API V2 Cookbook (Server-to-Server)*

## A. Registration Phase {#registration-phase}

The purpose of the Registration Phase is to register the streaming application against Adobe Pass Authentication through the Dynamic Client Registration (DCR) process.

The Dynamic Client Registration (DCR) process requires the streaming application to obtain a pair of client credentials and retrieve an access token as the end goal of the Registration Phase.

The Registration Phase is mandatory, but the streaming application can skip this phase if it has a cached pair of client credentials and an access token that are still valid.

+++Related Articles

APIs:

* [Retrieve client credentials](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-client-credentials.md)
* [Retrieve access token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md)

Flows:

* [Dynamic Client Registration Flow](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/flows/dynamic-client-registration-flow.md)

FAQs:

* [Registration Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-faqs.md)

+++

### Step 1: Register your application {#step-1-register-your-application}

* Retrieve client credentials: The Programmer Service retrieves client credentials by calling the [**/o/client/register**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-client-credentials.md) endpoint.

    * The Programmer Service or Programmer App must store the client credentials and use them indefinitely when needing to retrieve an access token.


* Retrieve access token: The Programmer Service retrieves access token by calling the [**/o/client/token**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md) endpoint.

    * The Programmer Service or Programmer App must store and use the access token until it expires, then discard it and obtain a new one.

## B. Authentication Phase {#authentication-phase}

The purpose of the Authentication Phase is to provide the streaming application the capability to verify the user's identity and obtain user metadata information.

The Authentication Phase acts as a prerequisite step for the Preauthorization Phase or Authorization Phase when the streaming application needs to play content.

+++Related Articles

APIs

* [Create authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md)
* [Resume authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md)
* [Retrieve authentication session](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md)
* [Perform authentication in user agent](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)
* [Retrieve profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)
* [Retrieve profile for specific mvpd](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md)
* [Retrieve profile for specific code](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md)

Flows

* [Basic authentication flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)
* [Basic authentication flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)
* [Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)
* [Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)

FAQs

* [Authentication Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authentication-phase-faqs-general)

+++

### Step 2: Check for existing authenticated profiles {#step-2-check-for-existing-authenticated-profiles}

* **Retrieve profiles:** The Programmer Service checks on behalf of the Streaming App for existing profiles by calling the [**/api/v2/{serviceProvider}/profiles**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md) endpoint.


* **Scenario 1:** There are existing profiles, the Programmer Service may proceed to the [Preauthorization Phase](#preauthorization-phase) or [Authorization Phase](#authorization-phase).


* **Scenario 2:** There are no existing profiles, the Programmer Service may proceed to the next step to [Authenticate the user](#step-3-authenticate-the-user).


* **Scenario 3:** There are no existing profiles, the Programmer Service may proceed to provide the user with temporary access through the [TempPass](/help/premium-workflow/temporary-access/temp-pass-feature.md) feature.

  * This scenario is outside the scope of this document, refer to the [Temporary Access Flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/temporary-access-flows/rest-api-v2-access-temporary-flows.md) documentation for more information.
  
### Step 3: Authenticate the user {#step-3-authenticate-the-user}

* **Retrieve configuration:** The Programmer Service retrieves the list of available MVPDs by calling the [**/api/v2/{serviceProvider}/configuration**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md) endpoint.

  * The Programmer Service can implement a custom filtering mechanism to refine the list of MVPDs from the configuration response, such that the Streaming App displays only the intended providers while hiding others (e.g., MVPDs under development, test MVPDs, TempPass). This ensures that users are presented with a curated selection when choosing their TV provider.


* **Create authentication session:** The Programmer Service initiates an authentication session by calling the [**/api/v2/{serviceProvider}/sessions**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint.

  * The Programmer Service must return the `code` and `url` to the Streaming App.


* **Scenario 1:** The Streaming App can open a browser or webview, therefore it must load the authentication `url`.

  * The user submits their username and password within the MVPD login page. Upon successful authentication the final redirect displays a success page.


* **Scenario 2:** The Streaming App cannot open a browser, therefore it must display the authentication `code`. A separate web application is required to prompt the user to enter the `code`, construct the authentication `url` and open: [**/api/v2/authenticate/{serviceProvider}/{code}**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md).

  * The user submits their username and password within the MVPD login page. Upon successful authentication the final redirect displays a success page.

### Step 4: Check for authenticated profiles {#step-4-check-for-authenticated-profiles}

* **Retrieve profile for specific code:** The Programmer Service must implement a polling mechanism using the `code` to check if the profile was successfully generated and saved by calling the [**/api/v2/{serviceProvider}/profiles/code/{code}**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md) endpoint.

  * The Programmer Service must **start the polling** mechanism under the following conditions:

    * **Authentication performed within the primary (screen) application:** The Programmer Service should start polling when the user reaches the final destination page, after the browser component loads the URL specified for the `redirectUrl` parameter in the [Sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint request.

    * **Authentication performed within a secondary (screen) application:** The Programmer Service application should start polling as soon as the user initiates the authentication process—right after receiving the [Sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint response and displaying the authentication code to the user.

  * The Programmer Service must **stop the polling** mechanism under the following conditions:

    * **Successful authentication:** The user's profile information is successfully retrieved, confirming their authentication status. At this point, polling is no longer needed.

    * **Authentication session and code expiry:** The authentication session and code expire, as indicated by the `notAfter` timestamp (e.g., 30 minutes) in the [Sessions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md) endpoint response. If this happens, the user must restart the authentication process, and polling using the previous authentication code should be stopped immediately.

    * **New authentication code generated:** If the user requests a new authentication code on the primary (screen) device, the existing session is no longer valid, and polling using the previous authentication code should be stopped immediately.

  * The Programmer Service must **configure the polling** mechanism frequency under the following conditions:

    * **Authentication performed within the primary (screen) application:** The Programmer Service should poll every 3-5 seconds or more.

    * **Authentication performed within a secondary (screen) application:** The Programmer Service should poll every 3-5 seconds or more.

  * The Programmer Service should cache parts of the user's profile information in a persistent storage to avoid unnecessary requests and improve the user experience.

## C. (Optional) Preauthorization Phase {#preauthorization-phase}

The purpose of the Preauthorization Phase is to provide the streaming application the capability to present a subset of resources from its catalog that the user would be entitled to access.

The Preauthorization Phase can enhance the user experience when the user opens the streaming application for the first time or navigates to a new section.

The Preauthorization Phase is not mandatory, the streaming application can skip this phase if it wants to present a catalog of resources without filtering them first based on the user's entitlement.

+++Related Articles

APIs

* [Retrieve preauthorization decisions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md)

Flows

* [Basic preauthorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)

FAQs

* [Preauthorization Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#preauthorization-phase-faqs-general)

+++

### Step 5: Check for preauthorized resources {#step-5-check-for-preauthorized-resources}

* **Retrieve preauthorization decisions:** The Programmer Service retrieves preauthorization decisions for a list of resources by calling the [**/api/v2/{serviceProvider}/decisions/preauthorize/{mvpd}**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md) endpoint.

  * The Programmer Service must pass the list of permit and deny preauthorization decisions to the Streaming App.

  * The Programmer Service is not required to store preauthorization decisions in persistent storage. However, it is recommended to cache permit decisions in memory to improve the user experience. This helps avoid unnecessary calls for resources that have already been preauthorized, reducing latency and improving performance.

  * The Programmer Service can determine the reason for a denied preauthorization decision by inspecting the [error code and message](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md) included in the response from the Decisions Preauthorize endpoint. These details provide insight into the specific reason the preauthorization request was denied, helping to inform the user experience or trigger any necessary handling in the application. Ensure that any retry mechanism implemented for retrieving preauthorization decisions does not result in an endless loop if the preauthorization decision is denied. Consider limiting retries to a reasonable number and handling denials gracefully by surfacing clear feedback to the user.

  * The Programmer Service can obtain a preauthorization decision for a limited number of resources in a single API request, usually up to 5, due to conditions imposed by MVPDs. This maximum number of resources can be viewed and changed after agreeing with MVPDs through the Adobe Pass [TVE Dashboard](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#tve-dashboard) by one of your organization administrators or by an Adobe Pass Authentication representative acting on your behalf.

## D. Authorization phase {#authorization-phase}

The purpose of the Authorization Phase is to provide the streaming application the capability to play resources the user requests after validating their rights with the MVPD.

The Authorization Phase is mandatory, the streaming application cannot skip this phase if it wants to play resources the user requests, as it requires verifying with the MVPD that the user is entitled before releasing the stream.

+++Related Articles

APIs

* [Retrieve authorization decisions](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md)

Flows

* [Basic authorization flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)

FAQs

* [Authorization Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authorization-phase-faqs-general)

+++

### Step 6: Check for authorized resources {#step-6-check-for-authorized-resources}

* **Retrieve authorization decision:** The Programmer Service retrieves authorization decision for a specific resource passed by the Streaming App by calling the [**/api/v2/{serviceProvider}/decision/authorize/{mvpd}**](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md) endpoint.

  * The Programmer Service is not required to store authorization decisions in persistent storage.

  * The Programmer Service can determine the reason for a denied authorization decision by inspecting the [error code and message](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md) included in the response from the Decisions Authorize endpoint. These details provide insight into the specific reason the authorization request was denied, helping to inform the user experience or trigger any necessary handling in the Streaming App. Ensure that any retry mechanism implemented for retrieving authorization decisions does not result in an endless loop if the authorization decision is denied. Consider limiting retries to a reasonable number and handling denials gracefully by surfacing clear feedback to the user.

  * The Programmer Service may evaluate other business rules and return an appropriate authorization decision to the Streaming App.

  * The Programmer Service is not required to refresh an expired media token while the stream is actively playing. If the media token expires during playback, the stream should be allowed to continue uninterrupted. However, the client must request a new authorization decision — and obtain a new media token — the next time the user attempts to play a resource.

  * The Programmer Service can obtain an authorization decision for a limited number of resources in a single API request, usually up to 1, due to conditions imposed by MVPDs.

## E. Logout phase {#logout-phase}

The purpose of the Logout Phase is to provide the streaming application the capability to terminate the user's authenticated profile within Adobe Pass Authentication upon user request.

The Logout Phase is mandatory, the streaming application must provide the user with the capability to log out.

+++Related Articles

APIs

* [Initiate logout for specific mvpd](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md)

Flows

* [Basic logout flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-logout-primary-application-flow.md)

FAQs

* [Logout Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#logout-phase-faqs-general)

+++

### Step 7: Logout {#step-7-logout}

* Initiate Adobe Pass logout: The Programmer Service initiates the logout flow as requested by the Streaming App by calling the [/api/v2/{serviceProvider}/logout/{mvpd}](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md) endpoint.

    * The Programmer Service may clean up any information it stores about the authenticated user.

    * The Programmer Service must follow the instructions provided in the `actionName` and `actionType` attributes of the Logout endpoint response to ensure the logout process is completed correctly.

        * If the `actionType` attribute in the response is set to "interactive", the Programmer Service must return the `url` attribute value to the Streaming App.

            * **Scenario 1:** The Streaming App can open a browser or webview, therefore it must load the logout `url`.  

            * **Scenario 2:** The Streaming App cannot open a browser, therefore the logout process can be stopped as the MVPD session was not persisted in a Streaming Device browser cache.
