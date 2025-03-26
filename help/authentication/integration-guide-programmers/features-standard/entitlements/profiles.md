---
title: Profiles
description: Profiles
---
# Profiles {#profiles}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

Profiles are created by Adobe Pass Authentication [REST API V2](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md) when a user successfully authenticates with their Pay TV provider (MVPD).

Profiles type vary based on the authentication method used:

* **Regular**

  Created through basic authentication.

* **Apple SSO**

  Created via single sign-on (SSO) using Apple's Video Subscriber Account framework.

* **Platform SSO**

  Created via single sign-on (SSO) using a platform identity.

* **Service Token SSO**

  Created via single sign-on (SSO) using a service token.

Profiles store key data that enables client applications to:

* Determine the user's authentication status.
* Identify the authentication method used.
* Identify the identity provider.
* Access [user metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md).

Profiles are securely stored in Adobe Pass Authentication’s backend and are linked to the requesting application, device, and service provider identifier. They remain valid for a limited timeframe, as defined by the [Authentication Time-to-Live (TTL)](#authentication-ttl-management).

## Authentication Time-to-Live (TTL) Management {#authentication-ttl-management}

Authentication Time-to-Live (TTL) defines how long a user remains authenticated before needing to re-authenticate. This timeframe is limited and must be agreed upon with MVPD representatives. TTL values can vary based on:

* Platform category (e.g., desktop, mobile, TV connected devices)
* Specific platform (e.g., iOS, Android, tvOS, Roku, FireTV)

The authentication (authN) TTL can be viewed and changed through the Adobe Pass [TVE Dashboard](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md#tve-dashboard) by one of your organization administrators or by an Adobe Pass Authentication representative acting on your behalf.

For more details, refer to the [TVE Dashboard Integrations User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-integrations.md#most-used-flows) documentation.

## REST API V2 {#rest-api-v2}

The profiles can be retrieved using the following APIs:

* [Retrieve profiles](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)
* [Retrieve profile for specific mvpd](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md)
* [Retrieve profile for specific code](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md)

Refer to the **Response** and **Samples** sections of the above APIs to understand the structure of the profiles.

For more details about how and when to integrate the above APIs, refer to the following documents:

* [Basic profiles flow performed within primary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)
* [Basic profiles flow performed within secondary application](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)

>[!MORELIKETHIS]
>
> [Authentication Phase FAQs](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md#authentication-phase-faqs-general)
