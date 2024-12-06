---
title: Dynamic Client Registration Overview
description: Dynamic Client Registration Overview
exl-id: 9f98dfcd-4375-48c3-beff-259dfb1d3a26
---
# Dynamic Client Registration Overview {#dynamic-client-registration-overview}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

Dynamic client registration represents an authorization mechanism defined by [RFC 7591](https://datatracker.ietf.org/doc/html/rfc7591), and it is based on the OAuth 2.0 authorization framework that is described by [RFC 6749](https://datatracker.ietf.org/doc/html/rfc6749).

Adobe Pass provides a dynamic client registration service that enables access to the following protected APIs:

* Adobe Pass Authentication Management APIs:
  * [Reset Temp Pass API](../../features-premium/temporary-access/reset-temp-pass.md)
  * [Degradation API](../../features-premium/degraded-access/degradation-api-overview.md)
  * [Proxy MVPD API](../../../integration-guide-mvpds/proxy-mvpd-webserv.md)
  * [Entitlement Service Monitoring API](../../features-premium/esm/entitlement-service-monitoring-api.md)
* Adobe Pass Authentication REST APIs:
  * [REST API V1](../../legacy/rest-api-v1/rest-api-reference.md)
  * [REST API V2](../rest-api-v2/apis/rest-api-v2-apis-overview.md)
* Adobe Pass Authentication SDKs:
  * [JavaScript SDK](../../legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md)
  * [iOS/tvOS SDK](../../legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md)
  * [Android SDK](../../legacy/sdks/android-sdk/android-sdk-api-reference.md)
  * [FireOS SDK](../../legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md)

>[!IMPORTANT]
>
> Dynamic client registration authorization mechanism replaces older Adobe Pass Authentication solutions that are subject to be discontinued:
>
> * The signed requestor ID mechanism.
> * The domain listing mechanism.
> * The API key mechanism.

With the adoption of dynamic client registration the main benefits are:

* Enhanced security.
* Unified model across platforms.
* Fine-grained control of your application's lifecycle.

To learn more about how to manage and use dynamic client registration, refer to the following sections.

## Dynamic Client Registration Management {#dynamic-client-registration-management}

The dynamic client registration management process allows client applications running on specific platforms and needing access to specific Adobe Pass Authentication APIs to register through the [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication).

The Adobe Pass TVE Dashboard is a tool for Adobe Pass Authentication customers (Programmers) to manage their configuration and data. This self-service dashboard enables a range of functionalities that are described in the [Adobe Pass TVE Dashboard User Guide](../../../user-guide-tve-dashboard/tve-dashboard-overview.md) documentation.

In case you have access to the [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication), follow the steps in the sections below to create a registered application and download the software statement.

### Manage registered applications {#manage-registered-applications}

>[!IMPORTANT]
>
> In case you do not have access to the Adobe Pass TVE Dashboard, create a ticket through our [Zendesk](https://adobeprimetime.zendesk.com) and ask your Technical Account Manager (TAM) to create a registered application and share the software statement with you.

There are two available ways you can create a registered application:

* **Programmer level**

  The programmer-level registration process allows you to create a registered application linked to all available channels or a selected subset of channels. For more details, refer to the [TVE Dashboard User Guide for Programmers](../../../user-guide-tve-dashboard/tve-dashboard-programmers.md) documentation.


* **Channel level**

  The channel-level registration process allows you to create a registered application linked only to the current selected channel. For more details, refer to the [TVE Dashboard User Guide for Channels](../../../user-guide-tve-dashboard/tve-dashboard-channels.md) documentation.

>[!IMPORTANT]
>
> It is recommended to create registered applications with more specific and limited permissions to enhance security and prevent unauthorized access. Therefore, when creating registered applications, consider using narrower options for the assigned `channels`, `platforms`, and `scopes`.
>
> It is recommended to create a new registered application for each major update of your client application to manage its life cycle and usage. If necessary, create a ticket through our [Zendesk](https://adobeprimetime.zendesk.com) and ask your Technical Account Manager (TAM) to revoke a registered application in order to block the functionality of a specific client application version.

### Manage software statements {#manage-software-statements}

>[!IMPORTANT]
>
> In case you do not have access to the Adobe Pass TVE Dashboard, create a ticket through our [Zendesk](https://adobeprimetime.zendesk.com) and ask your Technical Account Manager (TAM) to create a registered application and share the software statement with you.

Before downloading a software statement, ensure you have a registered application created as described in the [Manage registered applications](#manage-registered-applications) section that meets your client application requirements.

There are two available ways you can download a software statement based on the level where the registered application was created:

* **Programmer level**

  For more details, refer to the [TVE Dashboard User Guide for Programmers](../../../user-guide-tve-dashboard/tve-dashboard-programmers.md) documentation.

* **Channel level**

  For more details, refer to the [TVE Dashboard User Guide for Channels](../../../user-guide-tve-dashboard/tve-dashboard-channels.md) documentation.

The software statement is a JSON Web Token (`JWT`) that contains information about your client application software as a bundle. When presented to the [Retrieve client credentials](apis/dynamic-client-registration-apis-retrieve-client-credentials.md) API, the software statement is digitally signed using JSON Web Signature (`JWS`).

For more detailed explanation on what software statements are and how they work, refer to the [RFC 7591](https://tools.ietf.org/html/rfc7591) documentation.

## Dynamic Client Registration Flow  {#dynamic-client-registration-flow}

In summary, the dynamic client registration authorization mechanism involves several steps:

**Management**

* A client representative must create a registered application as described in the [Manage registered applications](#manage-registered-applications) section.
* A client representative must download and embed a software statement as described in the [Manage software statements](#manage-software-statements) section.

**Flow**

* The client application must obtain the client credentials as described in the [Retrieve client credentials](apis/dynamic-client-registration-apis-retrieve-client-credentials.md) API documentation.
* The client application must obtain the access token as described in the [Retrieve access token](apis/dynamic-client-registration-apis-retrieve-access-token.md) API documentation.

Refer to the [Dynamic Client Registration Flow](flows/dynamic-client-registration-flow.md) documentation to better understand how to access Adobe Pass protected APIs. Furthermore, you can also watch this [webinar](https://my.adobeconnect.com/pzkp8ujrigg1/) recording, which provides more context and includes a demo.
