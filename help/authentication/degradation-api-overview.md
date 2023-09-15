---
title: Degradation API Overview
description: Degradation API Overview
exl-id: c7d6685b-a235-42eb-9c9c-0ffa1747f614
---
# Degradation API Overview {#degradation-api-overview}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## General Information {#general_info}

>[!NOTE] 
>
>This API is not generally available. Contact your Adobe representative for availability updates.

This feature provides any of the threemain parties in an integration (Programmers, MVPDs, and Adobe) with the capability to temporarily bypass specific MVPD Authentication and Authorization endpoints. Usually it is the Programmer that initates such an action, but regardless of who triggers a degradation event, the action is dependent on previously agreed upon arrangements with the affected MVPDs.  

The main use-case for this feature occurs during live sports or big events. In such high traffic scenarios it is possible for the load on a specific MVPD endpoint to become too high, resulting in very long response times for users. In order to preserve a good user experience during such a scenario, the Programmer may decide to trigger a degradation rule that can temporarily auto-authenticate/auto-authorize users, or disable an MVPD by removing it from the available MVPDs list.

A degradation rule is applied only for a fixed period of time. Although the primary customers for this feature are sports channels and live news channels, any Programmer might want to have access to this feature, as MVPDs services do go down from time to time.

Degradation Notes:

* This feature is designed to be used together with the usage monitoring API, which provides realtime information about the number of authentications and authorizations per MVPD, average authorization latency, and other metrics needed for a complete service overview.
* This feature does not allow bypassing of the Adobe Primetim authentication service. If Adobe Pass authentication is down there is no mechanism within the service that can be used to allow users to see content. The sites or apps could, however, route around Adobe Pass authentication by themselves.
* Adobe will not currently trigger degradation directly-the decision must always reside with a specific Programmer that has agreed to such conditions with MVPDs. In the future, Adobe Pass authentication might be proactive in triggering degradation rules if agreements (SLA protection) can be reached with MVPDs.

<!--
## Related Information {#related}

- [ESM API](/help/authentication/entitlement-service-monitoring-api.md)
- [Server-side Metrics](/help/authentication/understanding-serverside-metrics.md)
-->
