---
title: Degradation Feature
description: Degradation Feature
exl-id: c7d6685b-a235-42eb-9c9c-0ffa1747f614
---
# Degradation Feature {#degradation-feature}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

In the dynamic world of live sports and major events, ensuring a seamless viewer experience is essential. High traffic during these events can overwhelm Multichannel Video Programming Distributor (MVPD) authentication and authorization endpoints, leading to delays or disruptions.

Adobe Pass Authentication addresses these challenges with its **Degradation Feature**, a solution that enables temporary bypass of specific MVPD authentication and authorization endpoints. This feature is particularly valuable during peak traffic events, where response times may degrade due to a heavy load on MVPD systems.

The **Degradation Feature** can be a vital safeguard for Programmers, ensuring continuity of service. While its primary audience includes live sports and news channels, its utility extends to any Programmer seeking to mitigate the risk of disruptions caused by MVPD endpoints. 

>[!IMPORTANT]
>
> The Degradation API is a premium feature and requires a current license from Adobe.

By applying a degradation rule, Programmers can temporarily enable auto-authentication or auto-authorization, ensuring uninterrupted access to content for the period the degradation is applied. Degradation actions are always initiated by a Programmer based on prearranged agreements with MVPDs. While Adobe does not currently trigger degradation directly, future capabilities may include proactive management if Service Level Agreements (SLAs) are established.

This feature is designed to be used together with a [usage monitoring API](/help/authentication/integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-overview.md) and based on pre-agreements with MVPDs, Adobe Pass Authentication offers a powerful tool to balance user experience, reliability, and operational control during critical moments.

>[!IMPORTANT]
>
> This feature does not permit bypassing the Adobe Pass Authentication service itself. If Adobe Pass Authentication is unavailable, there is no built-in mechanism within this service to facilitate user access. In such cases, sites or applications may choose to implement their own alternative routing solutions to maintain content delivery.

## Degradation API Access {#degradation-api-access}

Before accessing the [Degradation API](#degradation-api), you must complete the required steps in the Dynamic Client Registration (DCR) process. This mandatory process ensures you have the necessary access token to interact with the Degradation API.

For comprehensive instructions, refer to the [Dynamic Client Registration Overview](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md) documentation.

## Degradation API {#degradation-api}

The Degradation API is a RESTful API that allows Programmers to manage degradation rules for specific MVPDs. The API provides the means to activate, remove, as well to retrieve the status for the degradation rules that are active.

To learn more about the Degradation API, refer to the following Zendesk document [Adobe Pass Authentication | Degradation API v3](https://tve.zendesk.com/hc/en-us/articles/33912526308372-Adobe-Pass-Authentication-Degradation-API-v3) and look for the PDF file to download.

## REST API V2 {#rest-api-v2}

Leveraging the Degradation feature requires implementing code updates to modify how your TV Everywhere (TVE) application interacts with the Adobe Pass Authentication [REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md).

For a comprehensive guide on these updates and the associated workflows, refer to the [Degraded Access Flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/degraded-access-flows/rest-api-v2-access-degraded-flows.md) documentation.
