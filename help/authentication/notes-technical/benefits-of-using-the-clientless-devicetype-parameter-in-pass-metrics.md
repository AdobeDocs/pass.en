---
title: Benefits of using the Clientless deviceType parameter in Adobe Pass Authentication metrics
description: Benefits of using the Clientless deviceType parameter in Adobe Pass Authentication metrics
exl-id: a5004887-d5fa-468e-971b-10806519175b
---
# Benefits of using the Clientless deviceType parameter in Adobe Pass Authentication metrics {#benefits-of-using-the-clientless-devicetype-parameter-in-primetime-authentication-metrics}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

</br>

## Context

Although optional, the parameter `deviceType` from the Clientless API, when present, is used in Adobe Pass Authentication metrics that are being exposed through [Entitlement Service Monitoring](/help/authentication/integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-overview.md).

Considering that the connection between the `deviceType` parameter and its **benefits** on Adobe Pass Authentication metrics wasn't initially stated, the scope of this tech note is to add more information about them.

## Explanation

The `deviceType` parameter was present in the Clientless API since the first version, but its implications on Adobe Pass Authentication metrics were added in a more recent release.



>[!IMPORTANT]
>
>If the parameter `deviceType` is set correctly then it has the following **benefit** in Entitlement Service Monitoring: it offers metrics that are [broken down per device type](/help/authentication/integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-overview.md#clientless_device_type) when using Clientless, so that different types of analysis can be performed for e.g. Roku, AppleTV, Xbox etc.


For more information on the Entitlement Service Monitoring API, please refer to the [drill-down tree,](/help/authentication/integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-api.md#drill-down_tree) which illustrates the [dimensions](/help/authentication/integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-overview.md#esm_dimensions) (resources) available in ESM 2.0.

>[!NOTE]
>
>Content of this tech note was also added to the [Clientless API](#clientless_device_type).




## Implementation

To fully benefit from the Adobe Pass Authentication metrics, there are 2 types of [Clientless APIs](#web_srvs_summary) that are currently being used and that need to have the correct `deviceType` set:

1.  APIs that have `regcode` as a required parameter and will use the `deviceType` parameter which was set when creating the `regcode`, with the following API call:
      - [\<REGGIE\_FQDN\>/reggie/v1/{requestorId}/regcode](#reg_serv)

1.  APIs that have the `deviceType` as an optional parameter:
      - [\<SP\_FQDN\>/api/v1/checkauthn](#check_authn_token)
      - [<span class="s1">\<SP\_FQDN\>/api/v1/tokens/authn</span>](#retrieve_authn_token)
      - [\<SP\_FQDN\>/api/v1/authorize](#init_authz)
      - [\<SP\_FQDN\>/api/v1/tokens/authz](#retrieve_authz_token)
      - [\<SP\_FQDN\>/api/v1/tokens/media](#short_media)
      - [\<SP\_FQDN\>/api/v1/mediatoken](#short_media)
      - [\<SP\_FQDN\>/api/v1/preauthorize](#PreAuthZ_Resources)
      - [\<SP\_FQDN\>/api/v1/logout](#init_logout)

Our recommendation is to use the `deviceType` parameter and pass the correct Clientless device type for all APIs.
