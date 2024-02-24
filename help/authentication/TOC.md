---
product: adobe primetime
audience: end-user
feature: Authentication
user-guide-title: Adobe Pass Authentication
user-guide-description: Adobe Pass Authentication is an entitlement solution for TV Everywhere, providing a modular framework for determining whether someone who requests access to a resource is entitled to it.
---

# Adobe Pass Authentication Help {#authentication}

+ [Adobe Pass Authentication overview](home.md)
+ Adobe Pass Authentication concepts {#authentication-concepts}
    + [Technical paper](technical-paper.md)
    + [Overview for programmers](programmer-overview.md)
    + [MVPD overview](mvpd-overview.md)
+ Kickstart guides {#kickstart-guides}
    + [Programmer kickstart guide](programmer-kickstart-guide.md)
    + [MVPD kickstart guide](mvpd-kickstart-guide.md)
+ Programmer integration guide {#programmer-integration-guide}
    + [Programmer integration guide overview](programmer-integration-guide-overview.md)
    + [The programmer entitlement flow](entitlement-flow.md)
    + [Programmer use cases](programmer-use-cases.md)
    + [Passing client information (device, connection, and application)](passing-client-information-device-connection-and-application.md)
    + REST API {#restapi}
        + [REST API Overview](rest-api-overview.md)
        + [REST API Cookbook (Server-to-Server)](rest-api-cookbook-servertoserver.md)
        + [REST API Cookbook (Client-to-Server)](rest-api-cookbook-clienttoserver.md)
        + Rest API Reference {#rest-api-reference}
            + [REST API Reference](rest-api-reference.md)
            + [Registration Code Request](registration-code-request.md)
            + [Return Registration Record](return-registration-record.md)
            + [Delete Registration Record](delete-registration-record.md)
            + [Provide MVPD List](provide-mvpd-list.md)
            + [Initiate Authentication](initiate-authentication.md)
            + [Check Authentication Token](check-authentication-token.md)
            + [Retrieve Authentication Token](retrieve-authentication-token.md)
            + [Initiate Authorization](initiate-authorization.md)
            + [Retrieve Authorization Token](retrieve-authorization-token.md)
            + [Obtain Short Media Token](obtain-short-media-token.md)
            + [Check Authentication Flow by Second Screen Web App](check-authentication-flow-by-second-screen-web-app.md)
            + [Retrieve List of Preauthorized Resources](retrieve-list-of-preauthorized-resources.md)
            + [Retrieve List of Preauthorized Resources by Second Screen Web App](retrieve-list-of-preauthorized-resources-by-second-screen-web-app.md)
            + [Initiate logout](initiate-logout.md)
            + [User Metadata](user-metadata.md)
            + [Retrieve profile-request](retrieve-profilerequest.md)
            + [Token Exchange](token-exchange.md)
            + [Free Preview for Temp Pass and Promotional Temp Pass](free-preview-for-temp-pass-and-promotional-temp-pass.md)
    + AccessEnabler SDK {#accessenabler-sdk}
      + JavaScript SDK {#javascriptsdk}        
        + [JavaScript SDK Overview](javascript-sdk-overview.md)
        + [JavaScript SDK Cookbook](javascript-sdk-cookbook.md)
        + [JavaScript SDK API Reference](javascript-sdk-api-reference.md)
        + Guidelines {#js-sdk-guidelines}
            + [Refresh-less Login and Logout](refreshless-login-and-logout.md)
        + JavaScript API {#js-api}
            + [Preauthorize](js-preauthorize.md)
      + iOS/tvOS SDK {#ios-sdk}
          + [iOS/tvOS SDK Overview](iostvos-sdk-overview.md)
          + [iOS/tvOS SDK Cookbook](iostvos-sdk-cookbook.md)
          + [iOS/tvOS SDK API Reference](iostvos-sdk-api-reference.md)          
          + Guidelines {#ios-tvos-sdk-guidelines}
            + [iOS/tvOS Application Registration](iostvos-application-registration.md)
            + Migration guidelines {#migration-guidelines}  
              + [iOS/tvOS v3.x Migration Guide](iostvos-v3x-migration-guide.md)
          + iOS/tvOS API {#ios-tvos-api}
            + [Preauthorize](preauthorize.md)    
      + Android SDK {#androidsdk}
        + [Android SDK Overview](android-sdk-overview.md)
        + [Android SDK Cookbook](android-sdk-cookbook.md)
        + [Android SDK API Reference](android-sdk-api-reference.md)
        + Guidelines {#androidguidelines}
          + [Android Application Registration](android-application-registration.md)
          + [Android SDK with Dynamic Client Registration](android-sdk-with-dynamic-client-registration.md)
        + Android API{#androidapi}
          + [Preauthorize](preauthorize-android.md)
      + Amazon FireOS SDK {#fireossdk}
        + [Amazon FireOS SSO - Programmer kick-off guide](amazon-firetv-sso-programmer-kickoff-guide.md)
        + [Amazon FireOS SSO using Clientless API Cookbook](amazon-fireos-sso-using-clientless-api-cookbook.md)
        + [Amazon FireOS Technical Overview](amazon-fireos-technical-overview.md)
        + [Amazon FireOS Integration Cookbook](amazon-fireos-integration-cookbook.md)
        + [Amazon FireOS API Reference](amazon-fireos-native-client-api-reference.md)
        + [Amazon FireOS Application Registration](amazon-fireos-application-registration.md)
        + [FireOS SDK with Dynamic Client Registration](fireos-sdk-with-dynamic-client-registration.md)
    + Platform SSO {#platform-sso}
      + Apple SSO {#apple-sso}
        + [Apple SSO Overview](apple-sso-overview.md)
        + [Apple SSO Cookbook (REST API)](apple-sso-cookbook-rest-api.md)
        + [Apple SSO Cookbook (iOS/tvOS SDK)](apple-sso-cookbook-iostvos-sdk.md)
      + Roku SSO {#roku-sso}
        + [Roku SSO](roku-sso-overview.md)    
    + Content Metadata {#content-metadata}
      + [Identifying Protected Resource](identify-protected-resources.md)
    + Content server integration {#content-serv-int}
      + [How to integrate the Media Token Verifier](media-token-verifier-int.md)
    + Appendices {#appendices}
        + [Debugging tips](appendix-b-debugging-tips.md)
+ MVPD integration guide {#mvpd-int-guide}
  + [Integration features](mvpd-integr-features.md)
  + [Authentication](authn-usecase.md)
  + [Authentication using the OAuth 2.0 Protocol](authn-oauth2-protocol.md)
  + [Authorization](authz-usecase.md)
  + [Preflight authorization](mvpd-preflight-authz.md)
  + [MVPD Logout](usecase-mvpd-logout.md)
  + [Content metadata exchange](mvpd-content-metadata-exchange.md)
  + [User metadata exchange](mvpd-user-metadata-exchng.md)
  + [Proxy MVPD web service](proxy-mvpd-webserv.md)
  + [Proxy MVPD SAML integration](proxy-mvpd-saml-int.md)
  + [Service provider scoping](serv-provider-scoping.md)
  + [MVPD allow IP addresses](mvpd-listing-ip-addres.md)
+ Adobe Pass Authentication features {#auth-features}
  + Adobe Analytics integration {#analytics-int}
    + [Integrating Adobe Pass Authentication server side data into Adobe Analytics](integrate-authn-servr-data-analytics.md)
    + [Using Experience Cloud ID in Adobe Pass Authentication](exp-cloud-id-authn.md)
  + Entitlement service monitoring {#entitlement-service-monitoring}
    + [Entitlement service monitoring overview](entitlement-service-monitoring-overview.md)
    + [Entitlement service monitoring API](entitlement-service-monitoring-api.md)
    + [Server-side metrics](understanding-serverside-metrics.md)
  + Temp pass {#temp-pass}
    + [Temp pass](temp-pass.md)
    + [Promotional temp pass](promotional-temp-pass.md)
    + [Reset Temp Pass](reset-temp-pass.md)    
  + Single sign-On {#sso}
    + [Single sign-on support](sso-support.md)
    + [SSO via passive authentication](sso-passive-authn.md)
  + Home based authentication {#home-based-auth}
    + [Home based authentication for TV Everywhere](home-based-authn-tve.md)
    + [HBA status for MVPDs](hba-status-mvpds.md)
  + User metadata {#user-metadat}
    + [User metadata](user-metadata-feature.md)
  + [Preflight authorization](preflight-authz.md)
  + Error reporting {#error-reportn}
    + [Error reporting](error-reporting.md)
    + [Enhanced error codes](enhanced-error-codes.md)
  + Client registration {#client-regn}
    + [Dynamic Client Registration](dynamic-client-registration.md)
    + [Dynamic Client Registration API](dynamic-client-registration-api.md)
    + [Dynamic Client Registration Management](dynamic-client-registration-management.md)
  + Degradation service {#degrn-service}
    + [Degradation API Overview](degradation-api-overview.md)
  + Privacy readiness {#privacy-readiness}
    + [Privecy support overview](privacy-supp-overview.md)
    + [How to make a privacy request](make-privacy-req.md)
+ Tips and troubleshooting {#tips-troubleshoot}
  + [Allow MVPDs in the selection dialog](allow-mvpd-selectn-dialog.md)
  + [Prevent MVPDs from appearing the selection dialog](prevent-mvpd-selectn-dialog.md)
+ Support {#support}
  + [Escalation Procedures](escalation-procedures.md)
  + [Monitoring Adobe Pass Adobe PayTV Pass](monitoring-adobe-pay-tv-pass.md)
  + [Minimum System Requirements](minimum-system-requirements.md)
+ Release notes {#release-notes}
  + [Adobe Pass Authentication 2.68 release notes](auth-rn-268.md)
  + [Adobe Pass Authentication 2.67 release notes](auth-rn-267.md)
  + [Adobe Pass Authentication 2.66 release notes](auth-rn-266.md)
  + [Adobe Pass Authentication 2.65.1 release notes](auth-rn-2651.md)
  + [Adobe Pass Authentication 2.65 release notes](auth-rn-265.md)
  + [Adobe Pass Authentication 2.64.1 release notes](auth-rn-2641.md)
  + [Adobe Pass Authentication 2.64 release notes](auth-rn-264.md)
  + [Adobe Pass Authentication 2.63 release notes](auth-rn-263.md)
  + [Adobe Pass Authentication 2.62.1 release notes](auth-rn-2621.md)
  + iOS/tvOS SDK Release Notes  {#release-notes-ios}
    + [Adobe Pass Authentication iOS / tvOS 3.8.2 Release Notes](authn-rn-ios-tvos-382.md)
    + [Adobe Pass Authentication iOS / tvOS 3.8.1 Release Notes](authn-rn-ios-tvos-381.md)
    + [Adobe Pass Authentication iOS / tvOS 3.7.0 Release Notes](authn-rn-ios-tvos-370.md)
  + Android SDK Release Notes {#release-notes-android}
    + [Adobe Pass Authentication Android 3.7.3 Release Notes](authn-rn-android-373.md)
+ Tech Notes {#tech-notes}
  + Adobe Pass Authentication SDKs {#primetime-authentication-sdks}
    + [Certificates Q&A](certificates-qa.md)
    + JavaScript SDK {#javascript}
      + [JS SDK limitations for Safari browser](js-sdk-limitations-for-safari-browser.md)
      + [Cookies Updates - SameSite and Secure flags](cookies-updates--samesite-and-secure-flags.md)
    + Android SDK {#android}
      + [Access Enabler Android SDK Single Sign-On (SSO) on Android 10 apps](access-enabler-android-sdk-single-signon-sso-on-android-10-devices.md)
      + [Adobe Pass Authentication and the Android 6 "Marshmallow" New Permissions Model](adobe-primetime-authentication-and-the-android-6-marshmallow-new-permissions-model.md)
    + iOS/tvOS SDK {#iostvos}
      + [WKWebView support on iOS SDK 3.1+](wkwebview-support-on-ios-sdk-31.md)
      + [SFSafariViewController support on iOS SDK 3.2+](sfsafariviewcontroller-support-on-ios-sdk-32.md)
      + [SSO on iOS when using the Adobe Pass Authentication Access Enabler](sso-on-ios-when-using-the-primetime-authentication-access-enabler.md)
      + [iOS Authentication Error - adobepass.ios.app Cannot Be Found](ios-authentication-error-adobepassiosapp-cannot-be-found.md)
      + [Reset Temp Pass on iOS](reset-temp-pass-on-ios.md)
      + [Debugging the AccessEnabler iOS/tvOS SDK using Console app logs](debugging-the-accessenabler-iostvos-sdk-using-console-app-logs.md)
      + [AccessEnabler iOS/tvOS 3.7.0 Upgrade Path](accessenabler-iostvos-370-upgrade-path.md)            
  + Pass Authentication Environments {#primetime-authentication-environments}
    + [Understanding the Adobe Environments](understanding-the-adobe-environments.md)
    + [Setting up Your Environment and Testing in Pre-Qual](setting-up-your-environment-and-testing-in-prequal.md)
    + [How to test Authentication and Authorization flows using Adobe API test site](test-authn-authz-flows-using-adobes-api-test-site.md)
  + Clientless API {#clientless-api}
    + [Clientless API Implementation - Error codes / Messages With Probable Reason / Cause](clientless-api-implementation-error-codes--messages-with-probable-reason--cause.md)
    + [Clientless API Flow in the Absence of Device ID](clientless-api-flow-in-the-absence-of-device-id.md)
    + [Clientless: Avoid Using '&'reg_code in /authenticate Request](clientless-avoid-using-reg-code-in-authenticate-request.md)
    + [Enabling Adobe Pass Entitlement Services for a Programer on Xbox 360 and XboxOne Clientless](enabling-primetime-entitlement-services-for-a-programmer-on-xbox-360-and-xboxone-clientless-solution.md)
    + [Clientless device type and metrics](benefits-of-using-the-clientless-devicetype-parameter-in-pass-metrics.md)
  + User experience {#user-exp}
    + [How to migrate the MVPD login page from iFrame to popup](migr-mvpd-login-iframe-popup.md)
    + [Preflight feature: How to enable, troubleshoot or determine the issue](preflight-feature.md)
  + Tools and Utilities {#tools-and-utilities}
    + [Using Charles Proxy](using-charles-proxy.md)
  + Concepts {#concepts}
    + [Understanding User IDs](understanding-user-ids.md) 
+ [TVE Dashboard user guide](tve-dashboard-user-guide.md)
+ [New TVE Dashboard user guide] {#user-guide}
  + [TVE Dashboard overview](/help/authentication/tve-dashboard-overview.md)
  + [Work with Environments](/help/authentication/work-with-environments.md)
+ [Glossary](glossary.md)
