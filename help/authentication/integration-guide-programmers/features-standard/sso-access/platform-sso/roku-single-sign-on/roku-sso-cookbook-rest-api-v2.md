---
title: Roku SSO Cookbook (REST API V2)
description: Roku SSO Cookbook (REST API V2)
exl-id: 77b154bc-c09f-49d4-b1af-cc33bc6dd22b
---
# Roku SSO Cookbook (REST API V2) {#roku-sso-cookbook-rest-api-v2}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The Adobe Pass Authentication REST API V2 has support for Platform Single Sign-On (SSO) for end users of client applications running on RokuOS.

This document acts as an extension to the existing [REST API V2 Overview](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md) that provides a high-level view and the document that describes how to implement [Single sign-on using platform identity flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-platform-identity-flows.md).

## Roku single sign-on using platform identity flows {#cookbook}

Adobe Pass Authentication collaborates with Roku to improve the login user experience and to facilitate Single Sign-On (SSO) across TV Everywhere applications for TV subscribers.

### Prerequisites {#prerequisites}

Before proceeding with the Roku single sign-on using platform identity flows, ensure that Roku SSO is enabled. Roku SSO is enabled by default unless the Programmer or MVPD request for SSO to be disabled.

Each Programmer can Enable or Disable the Single Sign-On (SSO) on the Roku platform for specific integrations through the [Adobe Pass TVE Dashboard](https://experience.adobe.com/pass/authentication).

### Workflow {#workflow}

**Client-to-Server**

For Programmer applications utilizing a Client-to-Server architecture to integrate REST API V2, Roku SSO functions seamlessly without any modifications.

RokuOS automatically appends two HTTP headers to all requests sent to Adobe Pass Authentication endpoints.

**Server-to-Server**

For Programmer applications utilizing a Server-to-Server architecture to integrate REST API V2, the Programmer must coordinate with the Roku team to configure these headers to be included in all API flows directed to their domain.

To enable cross-application and cross-device SSO, the Roku-provided subscriber ID should be used instead of the device ID when passed by the application.

For more details, refer to the following documentation:

* [Header - X-Roku-Reserved-Roku-Connect-Token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-x-roku-reserved-roku-connect-token.md)
* [Header - AP-Device-Identifier](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-device-identifier.md)

For specific details about the format of the needed headers, please contact your Adobe representative.

### FAQs {#faqs}

* **How will the SSO work?**

  SSO will work across all Programmer applications powered by Adobe Pass Authentication on all Roku devices associated with the same Roku user. Not all MVPDs will allow Roku SSO. 


* **Will there be any change to the authentication TTLs?**

  The first valid authentication token will be used for performing SSO and, in this case, all the other applications that will be authenticated through SSO will use the same TTL until it expires. So, when navigating from one application to another, the second application will share the TTL of the first application that authenticates.


* **Will other Adobe functionality work as before?**

  All Adobe Pass Authentication functionality will work as before.


* **Is there a Programmer opt-in / opt-out process benefiting from SSO on the Roku platform?**

  This will be a configuration change in Adobe's TVE Dashboard. Each Programmer can Enable or Disable SSO on the Roku platform for specific integrations.


* **What are some common issues?**

  Programmers should check that their current implementations based on Adobe's REST API don't impede Roku's platform-SSO.

  See below a list of possible issues and how they should be solved.

| Problem                                          | Possible cause                                                             | Possible solutions                                                                         |
|--------------------------------------------------|----------------------------------------------------------------------------|--------------------------------------------------------------------------------------------|
| No Roku SSO header sent to Adobe                 | Using HTTP instead of HTTPS for calls to Adobe Pass Authentication domains | Use HTTPS                                                                                  |
| MVPD logo not shown / not updated for SSO tokens | UI relies on local storage                                                 | Applications should update UI (and local storage, if needed) after checking authentication |
| Logout triggered on no AuthZ                     | Application design                                                         | Application should be updated to never perform logout behind the scenes                    |
