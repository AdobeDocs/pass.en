---
product: adobe primetime
audience: end-user
feature: Authentication
user-guide-title: Adobe Pass Authentication
user-guide-description: Adobe Pass Authentication is an entitlement solution for TV Everywhere, providing a modular framework for determining whether someone who requests access to a resource is entitled to it.
---

# Adobe Pass Authentication Help {#authentication}

+ [Adobe Pass Authentication](home.md)
+ Kickstart {#kickstart}
    + [Technical paper](kickstart/technical-paper.md)
    + [Programmer overview](kickstart/programmer-overview.md)
    + [MVPD overview](kickstart/mvpd-overview.md)
    + [Programmer kickstart guide](kickstart/programmer-kickstart-guide.md)
    + [MVPD kickstart guide](kickstart/mvpd-kickstart-guide.md)
    + [Escalation Procedures](notes-technical/escalation-procedures.md)
    + [Glossary](kickstart/glossary.md)
+ Integration Guide For Programmers {#integration-guide-programmers}
    + REST APIs {#rest-apis}
        + REST API DCR {#rest-api-dcr}
            + [Dynamic client registration overview](integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-overview.md)
            + APIs {#rest-api-dcr-apis}
                + [Retrieve client credentials](integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-client-credentials.md)
                + [Retrieve access token](integration-guide-programmers/rest-apis/rest-api-dcr/apis/dynamic-client-registration-apis-retrieve-access-token.md)
            + Flows {#rest-api-dcr-flows}
                + [Dynamic client registration flow](integration-guide-programmers/rest-apis/rest-api-dcr/flows/dynamic-client-registration-flow.md)
        + REST API V2 {#rest-api-v2}
            + [REST API V2 Overview](integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-overview.md)
            + [REST API V2 Glossary](integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-glossary.md)
            + [REST API V2 FAQs](integration-guide-programmers/rest-apis/rest-api-v2/rest-api-v2-faqs.md)
            + APIs {#rest-api-v2-apis}
                + [REST API V2 APIs Overview](integration-guide-programmers/rest-apis/rest-api-v2/apis/rest-api-v2-apis-overview.md)
                + Configuration {#rest-api-v2-configuration-apis}
                    + [Retrieve configuration for specific service provider](integration-guide-programmers/rest-apis/rest-api-v2/apis/configuration-apis/rest-api-v2-configuration-apis-retrieve-configuration-for-specific-service-provider.md)
                + Sessions {#rest-api-v2-sessions-apis}
                    + [Create authentication session](integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-create-authentication-session.md)
                    + [Resume authentication session](integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-resume-authentication-session.md)
                    + [Retrieve authentication session](integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-retrieve-authentication-session-information-using-code.md)
                    + [Perform authentication in user agent](integration-guide-programmers/rest-apis/rest-api-v2/apis/sessions-apis/rest-api-v2-sessions-apis-perform-authentication-in-user-agent.md)
                + Profiles {#rest-api-v2-profiles-apis}
                    + [Retrieve profiles](integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profiles.md)
                    + [Retrieve profile for specific mvpd](integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-mvpd.md)
                    + [Retrieve profile for specific code](integration-guide-programmers/rest-apis/rest-api-v2/apis/profiles-apis/rest-api-v2-profiles-apis-retrieve-profile-for-specific-code.md)
                + Decisions {#rest-api-v2-decisions-apis}
                    + [Retrieve authorization decisions using specific mvpd](integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-authorization-decisions-using-specific-mvpd.md)
                    + [Retrieve preauthorization decisions using specific mvpd](integration-guide-programmers/rest-apis/rest-api-v2/apis/decisions-apis/rest-api-v2-decisions-apis-retrieve-preauthorization-decisions-using-specific-mvpd.md)
                + Logout {#rest-api-v2-logout-apis}
                    + [Initiate logout for specific mvpd](integration-guide-programmers/rest-apis/rest-api-v2/apis/logout-apis/rest-api-v2-logout-apis-initiate-logout-for-specific-mvpd.md)
                + Partner Single Sign-On {#rest-api-v2-partner-single-sign-on-apis}
                    + [Retrieve partner authentication request](integration-guide-programmers/rest-apis/rest-api-v2/apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-partner-authentication-request.md)
                    + [Retrieve profile using partner authentication response](integration-guide-programmers/rest-apis/rest-api-v2/apis/partner-single-sign-on-apis/rest-api-v2-partner-single-sign-on-apis-retrieve-profile-using-partner-authentication-response.md)
            + Flows {#rest-api-v2-flows}
                + [REST API V2 Flows Overview](integration-guide-programmers/rest-apis/rest-api-v2/flows/rest-api-v2-flows-overview.md)
                + Basic Access Flows {#rest-api-v2-basic-access-flows}
                    + [Basic profiles flow performed within primary application](integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-primary-application-flow.md)
                    + [Basic profiles flow performed within secondary application](integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-profiles-secondary-application-flow.md)
                    + [Basic authentication flow performed within primary application](integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-primary-application-flow.md)
                    + [Basic authentication flow performed within secondary application](integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authentication-secondary-application-flow.md)
                    + [Basic authorization flow performed within primary application](integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-authorization-primary-application-flow.md)
                    + [Basic preauthorization flow performed within primary application](integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-preauthorization-primary-application-flow.md)
                    + [Basic logout flow performed within primary application](integration-guide-programmers/rest-apis/rest-api-v2/flows/basic-access-flows/rest-api-v2-basic-logout-primary-application-flow.md)
                + Degraded Access Flows {#rest-api-v2-degraded-access-flows}
                    + [Degraded access flows](integration-guide-programmers/rest-apis/rest-api-v2/flows/degraded-access-flows/rest-api-v2-access-degraded-flows.md)
                + Temporary Access Flows {#rest-api-v2-temporary-access-flows}
                    + [Temporary access flows](integration-guide-programmers/rest-apis/rest-api-v2/flows/temporary-access-flows/rest-api-v2-access-temporary-flows.md)
                + Single Sign-On Access Flows {#rest-api-v2-single-sign-on-access-flows}
                    + [Single sign-on using partner flows](integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-partner-flows.md)
                    + [Single sign-on using platform identity flows](integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-platform-identity-flows.md)
                    + [Single sign-on using service token flows](integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-service-token-flows.md)
                    + [Single logout flow](integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-logout-flow.md)
            + Cookbooks {#rest-api-v2-cookbooks}
                + [REST API V2 Cookbook (Client-to-Server)](integration-guide-programmers/rest-apis/rest-api-v2/cookbooks/rest-api-v2-cookbook-client-server.md)
                + [REST API V2 Cookbook (Server-to-Server)](integration-guide-programmers/rest-apis/rest-api-v2/cookbooks/rest-api-v2-cookbook-server-server.md)
            + Appendix {#rest-api-v2-appendix}
                + Headers {#rest-api-v2-appendix-headers}
                    + [Header - Authorization](integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-authorization.md)
                    + [Header - AP-Device-Identifier](integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-device-identifier.md)
                    + [Header - X-Device-Info](integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-x-device-info.md)
                    + [Header - AD-Service-Token](integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ad-service-token.md)
                    + [Header - Adobe-Subject-Token](integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-adobe-subject-token.md)
                    + [Header - AP-Partner-Framework-Status](integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-partner-framework-status.md)
                    + [Header - AP-TempPass-Identity](integration-guide-programmers/rest-apis/rest-api-v2/appendix/headers/rest-api-v2-appendix-headers-ap-temppass-identity.md)
    + Standard Features {#standard-features}
        + Entitlements {#entitlements}
            + [Identifying Protected Resource](integration-guide-programmers/features-standard/entitlements/identify-protected-resources.md)
            + [Preflight authorization](integration-guide-programmers/features-standard/entitlements/preflight-authz.md)
            + [How to integrate the Media Token Verifier](integration-guide-programmers/features-standard/entitlements/media-token-verifier-int.md)
            + [User metadata](integration-guide-programmers/features-standard/entitlements/user-metadata-feature.md)
            + [User metadata certificate for encryption](integration-guide-programmers/features-standard/entitlements/user-metadata-certificate.md)
        + Error Reporting {#error-reporting}
            + [Enhanced error codes](integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md)
            + [Error reporting](integration-guide-programmers/features-standard/error-reporting/error-reporting.md)
        + Single Sign-On Access {#sso-access}
            + Partner Single Sign-On {#partner-sso}
                + Apple Single Sign-On {#apple-sso}
                    + [Apple SSO Overview](integration-guide-programmers/features-standard/sso-access/partner-sso/apple-sso/apple-sso-overview.md)
                    + [Apple SSO Cookbook (REST API V2)](integration-guide-programmers/features-standard/sso-access/partner-sso/apple-sso/apple-sso-cookbook-rest-api-v2.md)
                    + [Apple SSO Cookbook (REST API V1)](integration-guide-programmers/features-standard/sso-access/partner-sso/apple-sso/apple-sso-cookbook-rest-api-v1.md)
                    + [Apple SSO Cookbook (iOS/tvOS SDK)](integration-guide-programmers/features-standard/sso-access/partner-sso/apple-sso/apple-sso-cookbook-iostvos-sdk.md)
            + Platform Single Sign-On {#platform-sso}
                + Amazon Single Sign-On {#amazon-sso}
                    + [Amazon SSO Cookbook (REST API V2)](integration-guide-programmers/features-standard/sso-access/platform-sso/amazon-single-sign-on/amazon-sso-cookbook-rest-api-v2.md)
                    + [Amazon SSO Cookbook (REST API V1)](integration-guide-programmers/features-standard/sso-access/platform-sso/amazon-single-sign-on/amazon-sso-cookbook-rest-api-v1.md)
                + Roku Single Sign-On {#roku-sso}
                    + [Roku SSO Overview](integration-guide-programmers/features-standard/sso-access/platform-sso/roku-single-sign-on/roku-sso-overview.md)
            + [Single sign-on support](integration-guide-programmers/features-standard/sso-access/sso-support.md)
            + [SSO via passive authentication](integration-guide-programmers/features-standard/sso-access/sso-passive-authn.md)
        + Home Based Authentication Access {#hba-access}
            + [Home based authentication for TV Everywhere](integration-guide-programmers/features-standard/hba-access/home-based-authn-tve.md)
            + [HBA status for MVPDs](integration-guide-programmers/features-standard/hba-access/hba-status-mvpds.md)
        + Privacy Support {#privacy-support}
            + [Privecy support overview](integration-guide-programmers/features-premium/privacy-support/privacy-supp-overview.md)
            + [How to make a privacy request](integration-guide-programmers/features-premium/privacy-support/make-privacy-req.md)
    + Premium Features {#features-premium}
        + Temporary Access {#temporary-access}
            + [Temp pass](integration-guide-programmers/features-premium/temporary-access/temp-pass.md)
            + [Promotional temp pass](integration-guide-programmers/features-premium/temporary-access/promotional-temp-pass.md)
            + [Reset Temp Pass](integration-guide-programmers/features-premium/temporary-access/reset-temp-pass.md)
        + Degraded Access {#degraded-access}
            + [Degradation API Overview](integration-guide-programmers/features-premium/degraded-access/degradation-api-overview.md) 
        + ESM {#esm}
            + [Entitlement service monitoring overview](integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-overview.md)
            + [Entitlement service monitoring API](integration-guide-programmers/features-premium/esm/entitlement-service-monitoring-api.md)
            + [Server-side metrics](integration-guide-programmers/features-premium/esm/understanding-serverside-metrics.md)
        + Analytics {#analytics}
            + [Integrating Adobe Pass Authentication server side data into Adobe Analytics](integration-guide-programmers/features-premium/analytics/integrate-authn-servr-data-analytics.md)
            + [Using Experience Cloud ID in Adobe Pass Authentication](integration-guide-programmers/features-premium/analytics/exp-cloud-id-authn.md)
    + Legacy {#legacy}
        + (Legacy) REST API V1 {#rest-api-v1}
            + [REST API V1 Overview](integration-guide-programmers/legacy/rest-api-v1/apis/rest-api-overview.md)
            + [REST API V1 Reference](integration-guide-programmers/legacy/rest-api-v1/rest-api-reference.md)
            + (Legacy) APIs {#rest-api-v1-apis}
                + [Registration Code Request](integration-guide-programmers/legacy/rest-api-v1/apis/registration-code-request.md)
                + [Return Registration Record](integration-guide-programmers/legacy/rest-api-v1/apis/return-registration-record.md)
                + [Delete Registration Record](integration-guide-programmers/legacy/rest-api-v1/apis/delete-registration-record.md)
                + [Provide MVPD List](integration-guide-programmers/legacy/rest-api-v1/apis/provide-mvpd-list.md)
                + [Initiate Authentication](integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authentication.md)
                + [Check Authentication Token](integration-guide-programmers/legacy/rest-api-v1/apis/check-authentication-token.md)
                + [Retrieve Authentication Token](integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-authentication-token.md)
                + [Initiate Authorization](integration-guide-programmers/legacy/rest-api-v1/apis/initiate-authorization.md)
                + [Retrieve Authorization Token](integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-authorization-token.md)
                + [Obtain Short Media Token](integration-guide-programmers/legacy/rest-api-v1/apis/obtain-short-media-token.md)
                + [Check Authentication Flow by Second Screen Web App](integration-guide-programmers/legacy/rest-api-v1/apis/check-authentication-flow-by-second-screen-web-app.md)
                + [Retrieve List of Preauthorized Resources](integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-list-of-preauthorized-resources.md)
                + [Retrieve List of Preauthorized Resources by Second Screen Web App](integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md)
                + [Initiate logout](integration-guide-programmers/legacy/rest-api-v1/apis/initiate-logout.md)
                + [User Metadata](integration-guide-programmers/legacy/rest-api-v1/apis/user-metadata.md)
                + [Retrieve profile-request](integration-guide-programmers/legacy/rest-api-v1/apis/retrieve-profilerequest.md)
                + [Token Exchange](integration-guide-programmers/legacy/rest-api-v1/apis/token-exchange.md)
                + [Free Preview for Temp Pass and Promotional Temp Pass](integration-guide-programmers/legacy/rest-api-v1/apis/free-preview-for-temp-pass-and-promotional-temp-pass.md)
            + (Legacy) Cookbooks {#rest-api-v1-cookbooks}
                + [REST API V1 Cookbook (Client-to-Server)](integration-guide-programmers/legacy/rest-api-v1/cookbooks/rest-api-cookbook-clienttoserver.md)
                + [REST API V1 Cookbook (Server-to-Server)](integration-guide-programmers/legacy/rest-api-v1/cookbooks/rest-api-cookbook-servertoserver.md)
        + (Legacy) SDKs {#sdks}
            + (Legacy) JavaScript SDK {#javascript-sdk}
                + [JavaScript SDK Overview](integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-overview.md)
                + [JavaScript SDK Cookbook](integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-cookbook.md)
                + [JavaScript SDK API Reference](integration-guide-programmers/legacy/sdks/javascript-sdk/javascript-sdk-api-reference.md)
                + [JavaScript SDK API Preauthorize](integration-guide-programmers/legacy/sdks/javascript-sdk/preauthorize-api-javascript-sdk.md)
                + (Legacy) Guidelines {#javascript-sdk-guidelines}
                    + [Refresh-less Login and Logout](integration-guide-programmers/legacy/sdks/javascript-sdk/refreshless-login-and-logout.md)
            + (Legacy) iOS/tvOS SDK {#ios-tvos-sdk}
                + [iOS/tvOS SDK Overview](integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-overview.md)
                + [iOS/tvOS SDK Cookbook](integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-cookbook.md)
                + [iOS/tvOS SDK API Reference](integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-api-reference.md)
                + [iOS/tvOS SDK API Preauthorize](integration-guide-programmers/legacy/sdks/ios-tvos-sdk/preauthorize-api-ios-tvos-sdk.md)
                + (Legacy) Guidelines {#ios-tvos-sdk-guidelines}
                    + [iOS/tvOS Application Registration](integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-application-registration.md)
                    + [iOS/tvOS v3.x Migration Guide](integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-v3x-migration-guide.md)
                    + [iOS/tvOS Storage Integrity Checks](integration-guide-programmers/legacy/sdks/ios-tvos-sdk/iostvos-sdk-storage-integrity-checks.md)
            + (Legacy) Android SDK {#android-sdk}
                + [Android SDK Overview](integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-overview.md)
                + [Android SDK Cookbook](integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-cookbook.md)
                + [Android SDK API Reference](integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-api-reference.md)
                + [Android SDK API Preauthorize](integration-guide-programmers/legacy/sdks/android-sdk/preauthorize-api-android-sdk.md)
                + (Legacy) Guidelines {#android-sdk-guidelines}
                    + [Android Application Registration](integration-guide-programmers/legacy/sdks/android-sdk/android-application-registration.md)
                    + [Android SDK with Dynamic Client Registration](integration-guide-programmers/legacy/sdks/android-sdk/android-sdk-with-dynamic-client-registration.md)
            + (Legacy) FireOS SDK {#fireos-sdk}
                + [Amazon FireOS Technical Overview](integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-technical-overview.md)
                + [Amazon FireOS Integration Cookbook](integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-integration-cookbook.md)
                + [Amazon FireOS API Reference](integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-native-client-api-reference.md)
                + [Amazon FireOS Application Registration](integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-fireos-application-registration.md)
                + [FireOS SDK with Dynamic Client Registration](integration-guide-programmers/legacy/sdks/fireos-sdk/fireos-sdk-with-dynamic-client-registration.md)
                + [Amazon FireOS SSO - Programmer kick-off guide](integration-guide-programmers/legacy/sdks/fireos-sdk/amazon-firetv-sso-programmer-kickoff-guide.md)
    + [Programmer integration guide overview](integration-guide-programmers/programmer-integration-guide-overview.md)
    + [Throttling mechanism](integration-guide-programmers/throttling-mechanism.md)
    + [Minimum system requirements](integration-guide-programmers/minimum-system-requirements.md)
    + [Programmer entitlement flow](integration-guide-programmers/entitlement-flow.md)
    + [Programmer use cases](integration-guide-programmers/programmer-use-cases.md)
    + [Passing client information (device, connection, and application)](integration-guide-programmers/passing-client-information-device-connection-and-application.md)
+ Integration Guide For MVPDs {#integration-guide-mvpds}
    + [Integration features](integration-guide-mvpds/mvpd-integr-features.md)
    + [Authentication](integration-guide-mvpds/authn-usecase.md)
    + [Authentication using the OAuth 2.0 Protocol](integration-guide-mvpds/authn-oauth2-protocol.md)
    + [Authorization](integration-guide-mvpds/authz-usecase.md)
    + [Preflight authorization](integration-guide-mvpds/mvpd-preflight-authz.md)
    + [MVPD Logout](integration-guide-mvpds/usecase-mvpd-logout.md)
    + [Content metadata exchange](integration-guide-mvpds/mvpd-content-metadata-exchange.md)
    + [User metadata exchange](integration-guide-mvpds/mvpd-user-metadata-exchng.md)
    + [Proxy MVPD web service](integration-guide-mvpds/proxy-mvpd-webserv.md)
    + [Proxy MVPD SAML integration](integration-guide-mvpds/proxy-mvpd-saml-int.md)
    + [Service provider scoping](integration-guide-mvpds/serv-provider-scoping.md)
    + [MVPD allow IP addresses](integration-guide-mvpds/mvpd-listing-ip-addres.md)
+ User Guide For TVE Dashboard {#user-guide-tve-dashboard}
    + [TVE Dashboard overview](/help/authentication/user-guide-tve-dashboard/tve-dashboard-overview.md)
    + [Environments](/help/authentication/user-guide-tve-dashboard/tve-dashboard-environments.md)
    + [Review and push changes](/help/authentication/user-guide-tve-dashboard/tve-dashboard-review-push-changes.md)
    + [Dashboard](/help/authentication/user-guide-tve-dashboard/tve-dashboard-home.md)
    + [Channels](/help/authentication/user-guide-tve-dashboard/tve-dashboard-channels.md)
    + [Programmers](/help/authentication/user-guide-tve-dashboard/tve-dashboard-programmers.md)
    + [MVPDs](/help/authentication/user-guide-tve-dashboard/tve-dashboard-mvpds.md)
    + [Integrations](/help/authentication/user-guide-tve-dashboard/tve-dashboard-integrations.md)
    + [Reports](/help/authentication/user-guide-tve-dashboard/tve-dashboard-reports.md)
    + [Changes log](/help/authentication/user-guide-tve-dashboard/tve-dashboard-changes-log.md)
    + [TVE Dashboard user guide](user-guide-tve-dashboard/tve-dashboard-user-guide.md)
+ Release Notes {#release-notes}
    + 2024 {#release-notes-2024}
        + [Adobe Pass Authentication 3.0.3 release notes](notes-releases/auth-rn-303.md)
        + [Adobe Pass Authentication 3.0 release notes](notes-releases/auth-rn-300.md)
        + [Adobe Pass Authentication 2.70 release notes](notes-releases/auth-rn-270.md)
        + [Adobe Pass Authentication 2.69 release notes](notes-releases/auth-rn-269.md)
        + [Adobe Pass Authentication JavaScript 4.7.0 Release Notes](notes-releases/authn-rn-javascript-470.md)
        + [Adobe Pass Authentication iOS / tvOS 3.9.2 Release Notes](notes-releases/authn-rn-ios-tvos-392.md)
        + [Adobe Pass Authentication iOS / tvOS 3.8.4 Release Notes](notes-releases/authn-rn-ios-tvos-384.md)
    + 2023 {#release-notes-2023}
        + [Adobe Pass Authentication 2.68 release notes](notes-releases/auth-rn-268.md)
        + [Adobe Pass Authentication 2.67 release notes](notes-releases/auth-rn-267.md)
        + [Adobe Pass Authentication 2.66 release notes](notes-releases/auth-rn-266.md)
        + [Adobe Pass Authentication 2.65.1 release notes](notes-releases/auth-rn-2651.md)
        + [Adobe Pass Authentication 2.65 release notes](notes-releases/auth-rn-265.md)
        + [Adobe Pass Authentication 2.64.1 release notes](notes-releases/auth-rn-2641.md)
        + [Adobe Pass Authentication iOS / tvOS 3.8.3 Release Notes](notes-releases/authn-rn-ios-tvos-383.md)
        + [Adobe Pass Authentication iOS / tvOS 3.8.2 Release Notes](notes-releases/authn-rn-ios-tvos-382.md)
        + [Adobe Pass Authentication iOS / tvOS 3.8.1 Release Notes](notes-releases/authn-rn-ios-tvos-381.md)
        + [Adobe Pass Authentication Android 3.7.3 Release Notes](notes-releases/authn-rn-android-373.md)
    + 2022 {#release-notes-2022}
        + [Adobe Pass Authentication 2.64 release notes](notes-releases/auth-rn-264.md)
        + [Adobe Pass Authentication 2.63 release notes](notes-releases/auth-rn-263.md)
        + [Adobe Pass Authentication 2.62.1 release notes](notes-releases/auth-rn-2621.md)
        + [Adobe Pass Authentication JavaScript 4.6.0 Release Notes](notes-releases/authn-rn-javascript-460.md)
    + 2021 {#release-notes-2021}
        + [Adobe Pass Authentication JavaScript 4.4.0 Release Notes](notes-releases/authn-rn-javascript-440.md)
        + [Adobe Pass Authentication iOS / tvOS 3.7.0 Release Notes](notes-releases/authn-rn-ios-tvos-370.md)
+ Tech Notes {#tech-notes}
    + Environments {#tech-notes-environments}
        + [Understanding the Adobe Environments](notes-technical/understanding-the-adobe-environments.md)
        + [Setting up Your Environment and Testing in Pre-Qual](notes-technical/setting-up-your-environment-and-testing-in-prequal.md)
        + [How to test Authentication and Authorization flows using Adobe API test site](notes-technical/test-authn-authz-flows-using-adobes-api-test-site.md)
    + User Experience {#tech-notes-user-experience}
        + [How to migrate the MVPD login page from iFrame to popup](notes-technical/migr-mvpd-login-iframe-popup.md)
        + [Preflight feature: How to enable, troubleshoot or determine the issue](notes-technical/preflight-feature.md)
        + [Allow MVPDs in the selection dialog](notes-technical/allow-mvpd-selectn-dialog.md)
        + [Prevent MVPDs from appearing the selection dialog](notes-technical/prevent-mvpd-selectn-dialog.md)
    + REST API V1 {#tech-notes-rest-api-v1}
        + [Clientless API Implementation - Error codes / Messages With Probable Reason / Cause](notes-technical/clientless-api-implementation-error-codes-messages-with-probable-reason-cause.md)
        + [Clientless API Flow in the Absence of Device ID](notes-technical/clientless-api-flow-in-the-absence-of-device-id.md)
        + [Clientless: Avoid Using '&'reg_code in /authenticate Request](notes-technical/clientless-avoid-using-reg-code-in-authenticate-request.md)
        + [Enabling Adobe Pass Entitlement Services for a Programer on Xbox 360 and XboxOne Clientless](notes-technical/enabling-primetime-entitlement-services-for-a-programmer-on-xbox-360-and-xboxone-clientless-solution.md)
        + [Clientless device type and metrics](notes-technical/benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)
    + SDKs {#tech-notes-sdks}
        + [Certificates Q&A](notes-technical/certificates-qa.md)
        + [Understanding User IDs](notes-technical/understanding-user-ids.md)
        + JavaScript SDK {#tech-notes-javascript-sdk}
            + [Tracking Prevention Assessment - Apple Safari](notes-technical/tracking-prevention-assessment-apple-safari.md)
            + [Tracking Prevention Assessment - Google Chrome](notes-technical/tracking-prevention-assessment-google-chrome.md)
            + [Cookies Updates - SameSite and Secure flags](notes-technical/cookies-updates-samesite-and-secure-flags.md)
            + [Debugging tips](notes-technical/appendix-b-debugging-tips.md)
        + Android SDK {#tech-notes-android-sdk}
            + [Access Enabler Android SDK Single Sign-On (SSO) on Android 10 apps](notes-technical/access-enabler-android-sdk-single-signon-sso-on-android-10-devices.md)
            + [Adobe Pass Authentication and the Android 6 "Marshmallow" New Permissions Model](notes-technical/adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model.md)
        + iOS/tvOS SDK {#tech-notes-ios-tvos-sdk}
            + [WKWebView support on iOS SDK 3.1+](notes-technical/wkwebview-support-on-ios-sdk-31.md)
            + [SFSafariViewController support on iOS SDK 3.2+](notes-technical/sfsafariviewcontroller-support-on-ios-sdk-32.md)
            + [SSO on iOS when using the Adobe Pass Authentication Access Enabler](notes-technical/sso-on-ios-when-using-the-primetime-authentication-access-enabler.md)
            + [iOS Authentication Error - adobepass.ios.app Cannot Be Found](notes-technical/ios-authentication-error-adobepassiosapp-cannot-be-found.md)
            + [Reset Temp Pass on iOS](notes-technical/reset-temp-pass-on-ios.md)
            + [Debugging the AccessEnabler iOS/tvOS SDK using Console app logs](notes-technical/debugging-the-accessenabler-iostvos-sdk-using-console-app-logs.md)
            + [AccessEnabler iOS/tvOS 3.7.0 Upgrade Path](notes-technical/accessenabler-iostvos-370-upgrade-path.md)
    + Troubleshooting {#tech-notes-troubleshooting}
        + [Using Charles Proxy](notes-technical/using-charles-proxy.md)
        + [Monitoring Adobe Pass Adobe PayTV Pass](notes-technical/monitoring-adobe-pay-tv-pass.md)
