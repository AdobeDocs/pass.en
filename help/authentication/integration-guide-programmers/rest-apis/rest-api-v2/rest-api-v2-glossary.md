---
title: REST API V2 Glossary
description: REST API V2 Glossary
exl-id: 8b3bd2de-1ff8-4c57-b18d-27ecdf2b0de2
---
# REST API V2 Glossary {#rest-api-v2-glossary}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This document provides definitions for terms used when integrating the Adobe Pass Authentication REST API V2.

>[!MORELIKETHIS]
>
> * [Dynamic Client Registration (DCR) Glossary](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-glossary.md)

## Glossary Terms {#glossary-terms}

### A {#a}

#### Authentication {#authentication}

The authentication is a process that allows a user to prove their identity to a [Programmer](#programmer), to gain access to protected content ([resource](#resource)), after validating the user subscription with the [MVPD](#mvpd).

#### Authentication Code {#code}

The authentication code is an Adobe Pass Authentication concept that stores a unique value generated when a user initiates the [authentication](#authentication) process, and uniquely identifies a user's [authentication session](#session) until the authentication process is complete.

The authentication code can be used by both a [Primary (Programmer) Application](#primary-application) or a [Secondary (Programmer) Application](#secondary-application) to complete the [authentication](#authentication) process, retrieve information about the [authentication session](#session), or to access the user [profile](#profile).

Synonymous with former term used registration code.

#### Authentication Session {#session}

The authentication session is an Adobe Pass Authentication concept that stores information about the user's authentication process started (or continued) from a [Programmer](#programmer) application, and is uniquely identified by an [authentication code](#code).

The authentication session can also indicate the [Programmer](#programmer) application to proceed with the [authorization](#authorization) process as the next phase of the [entitlement](#entitlement) flow in case the user is already authenticated.

#### Authorization {#authorization}

The authorization is a process that allows a user to access protected content ([resource](#resource)) from a [Programmer](#programmer) catalog based on the owned [MVPD](#mvpd) subscription, after validating the user rights with the [MVPD](#mvpd).

### C {#c}

#### Configuration {#configuration}

The configuration is an Adobe Pass Authentication concept that stores information about the [Programmer](#programmer) and [MVPD](#mvpd) integration settings and can be used during the [authentication](#authentication) process when asking the user to select their [TV Provider](#tv-provider) from a list of active integrations.

### D {#d}

#### Decision {#decision}

The decision is an Adobe Pass Authentication concept that stores information about the [MVPD](#mvpd) [authorization](#authorization) or [preauthorization](#preauthorization) process enquiry to allow or deny user access to a [Programmer](#programmer) protected content.

#### Degradation {#degradation}

The degradation is an Adobe Pass Authentication feature that allows a user to access protected content even when its [MVPD](#mvpd) experiences a service disruption.

For more information, refer to the [Degradation Feature](/help/authentication/integration-guide-programmers/features-premium/degraded-access/degradation-feature.md) documentation.

#### Device ID {#device-id}

The device ID is a unique identifier bound to the user's device and must be provided by the [Programmer](#programmer) application on all phases of the [entitlement](#entitlement) flow.

### E {#e}

#### Entitlement {#entitlement}

The entitlement is an Adobe Pass Authentication concept that incorporates the available flows and features that help a user go through different phases, to access protected content, ranging from [authentication](#authentication), [preauthorization](#preauthorization), [authorization](#authorization), and finally [logout](#logout).

#### Enhanced Error Code {#enhanced-error-code}

The enhanced error code is an Adobe Pass Authentication concept that provides additional information about the error that occurred while processing a request.

For more information, refer to the [Enhanced Error Codes](/help/authentication/integration-guide-programmers/features-standard/error-reporting/enhanced-error-codes.md) documentation.

### H {#h}

#### HBA {#hba}

The Home-Based Authentication (HBA) is the process whereby a consumer is automatically granted access to [TV Everywhere (TVE)](#tve) content on select devices that are connected to their home network, which is part of the location within the subscription contract.

### I {#i}

#### Identity Provider {#identity-provider}

The identity provider is a company that provides identity services to consumers across cable, satellite, or internet-based services in the context of [TV Everywhere (TVE)](#tve).

Synonymous with [MVPD](#mvpd) and [TV Provider](#tv-provider).

### L {#l}

#### Logout {#logout}

The logout is a process that allows a user to terminate their authenticated [profile](#profile) within Adobe Pass Authentication and update the [Programmer](#programmer) application to reflect the user's status.

### M {#m}

#### Media Token {#media-token}

The media token is a token generated by Adobe Pass Authentication as a result of an authorization [decision](#decision) meant to provide access to protected content.

The media token is passed to the [Programmer](#programmer), which then validates it to ensure the security of access for that [resource](#resource).

Synonymous with former term used short authorization token.

#### Media Token Verifier {#media-token-verifier}

The Media Token Verifier is a library distributed by Adobe Pass Authentication that is responsible for verifying the authenticity of a [media token](#media-token).

For more information, refer to the [Media Token Verifier](/help/authentication/integration-guide-programmers/features-standard/entitlements/media-tokens.md#media-token-verifier) documentation.

#### MVPD {#mvpd}

The multichannel video programming distributor (MVPD) is a company that provides television services to consumers across cable, satellite, or internet-based services.

The MVPD is identified by a unique value defined during the onboarding process between the MVPD and Adobe.

Synonymous with [TV Provider](#tv-provider) and [Identity Provider](#identity-provider).

### P {#p}

#### Partner {#partner}

The partner is a company that provides a service or framework to a [Programmer](#programmer) to enable a single sign-on user experience.

The partner is identified by a unique value (e.g., "apple") that is defined during the onboarding process between the partner and Adobe.

#### Preauthorization {#preauthorization}

The preauthorization is a process that allows a user to preview a subset of [resources](#resource) from a [Programmer](#programmer) catalog they would be entitled to access, after validating the user rights with the [MVPD](#mvpd).

Synonymous with [Preflight](#preflight).

#### Preflight {#preflight}

The preflight is a process that allows a user to preview a subset of [resources](#resource) from a [Programmer](#programmer) catalog they would be entitled to access, after validating the user rights with the [MVPD](#mvpd).

Synonymous with [Preauthorization](#preauthorization).

#### Primary (Programmer) Application {#primary-application}

The primary application refers to a [Programmer](#programmer) application that initiates [authentication](#authentication), but which may not be capable of completing the process by using a [user agent](#user-agent) to navigate to the [MVPD](#mvpd) login page.

#### Profile {#profile}

The profile is an Adobe Pass Authentication concept that stores information about the user's authentication start date and end date, the [user's metadata](#user-metadata) along with other fields that indicate the method of obtaining the authentication (e.g., "regular", "degraded", "temporary", "single sign-on", etc.).  

Synonymous with the former term used authentication token.

#### Programmer {#programmer}

The Programmer is a company that provides content to consumers through owned channels (brands) across various platforms.

The Programmer groups multiple owned channels (brands) as [service providers](#service-provider) in its integration with Adobe Pass Authentication.

#### Proxy MVPD {#proxy-mvpd}

The proxy MVPD is a company that provides identity services for other MVPDs and directly integrates with Adobe Pass Authentication.

#### Proxied MVPD {#proxied-mvpd}

The proxied MVPD is a company that does not have a direct integration with Adobe Pass Authentication, but gets integrated through a [proxy MVPD](#proxy-mvpd).

#### Platform Identity {#platform-identity}

The platform identity is a unique platform identifier payload generated by a service or framework (library) bound to the user's device and is provided to the [Programmer](#programmer) to enable a single sign-on user experience.

For more information, refer to the [Single sign-on using platform identity flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-platform-identity-flows.md) documentation.

### R {#r}

#### Resource {#resource}

The resource is a protected content that a user is trying to access from a [Programmer](#programmer) catalog.

The resource is identified by a unique value agreed upon between the Programmer and MVPDs.

For more information, refer to the [Protected Resources](/help/authentication/integration-guide-programmers/features-standard/entitlements/protected-resources.md#identifiers) documentation.

### S {#s}

#### SAML {#saml}

The Security Assertion Markup Language (SAML) is an open standard for exchanging authentication and authorization data between parties, in particular, between an [identity provider](#identity-provider) and a [service provider](#sp).

#### Secondary (Programmer) Application {#secondary-application}

The secondary application refers to a [Programmer](#programmer) application that is capable of completing the [authentication](#authentication) process by using a [user agent](#user-agent) to navigate to the [MVPD](#mvpd) login page.

The secondary application may run on the same device as the primary application or on a different (secondary) device, in which case the sign-in experience is referred to as a 'second screen authentication' user experience.

#### Service Token {#service-token}

The service token is a unique user identifier generated by a service or framework (library) bound to the user and is provided to the [Programmer](#programmer) to enable a single sign-on user experience.

For more information, refer to the [Single sign-on using service token flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-service-token-flows.md) documentation.

#### Service Provider {#service-provider}

The service provider is a channel (brand) that is owned by a [Programmer](#programmer).

The service provider is identified by a unique value defined during the onboarding process between the Programmer and Adobe.

Synonymous with the former term used requestor ID.

#### SLO {#slo}

The single logout (SLO) is a process that allows a user to log out from all the applications that were part of the [single sign-on (SSO)](#sso).

#### SP {#sp}

The service provider (SP) refers to the role played by Adobe Pass Authentication on behalf of a [Programmer](#programmer) in an integration with an [MVPD](#mvpd).

#### SSO {#sso}

The single sign-on (SSO) is a process that allows a user to authenticate once and gain access to multiple [Programmer](#programmer) applications without the need to authenticate for each of them.

### T {#t}

#### TempPass Basic {#temp-pass-basic}

The basic TempPass is an Adobe Pass Authentication feature that allows a user to access protected content for a limited time without the need to authenticate with an [MVPD](#mvpd).

For more information, refer to the [Basic TempPass](/help/authentication/integration-guide-programmers/features-premium/temporary-access/temp-pass-feature.md#basic-temp-pass) documentation.

#### TempPass Promotional {#temp-pass-promotional}

The promotional TempPass is an Adobe Pass Authentication feature that allows a user to access protected content for a maximum number of resources and a limited time without the need to authenticate with an [MVPD](#mvpd).

For more information, refer to the [Promotional TempPass](/help/authentication/integration-guide-programmers/features-premium/temporary-access/temp-pass-feature.md#promotional-temp-pass) documentation.

#### TTL {#ttl}

The time to live (TTL) is a value that indicates the amount of time that an underlying entity is valid for.

The TTL can be mentioned for an [access token](/help/authentication/integration-guide-programmers/rest-apis/rest-api-dcr/dynamic-client-registration-glossary.md#access-token), a [profile](#profile), an authorization [decision](#decision), or a [media token](#media-token).

#### TVE {#tve}

The TV Everywhere (TVE) is an industry niche that allows consumers to access their favorite TV shows, movies, and other content on multiple devices, such as smartphones, tablets, laptops, and many more.

#### TVE Dashboard {#tve-dashboard}

The TV Everywhere (TVE) Dashboard is an Adobe Pass Authentication tool provided to [Programmers](#programmer) to manage their configuration and data.

For more information, refer to the [TVE Dashboard User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-overview.md) documentation.

#### TV Provider {#tv-provider}

The TV provider is a company that provides television services to consumers across cable, satellite, or internet-based services.

The TV provider is identified by a unique value defined during the onboarding process between the TV provider and Adobe.

Synonymous with [MVPD](#mvpd) and [Identity Provider](#identity-provider).

### U {#u}

#### User Agent {#user-agent}

The user agent refers to a browser or similar component (platform-specific) capable of navigating the web and rendering the [MVPD](#mvpd) login page. 

#### User ID {#user-id}

The user ID is a unique identifier bound to the user and originates from the [MVPD](#mvpd) authentication process.

#### User Metadata {#user-metadata}

The user metadata refers to user-specific attributes (e.g., zip codes, parental ratings, user IDs, etc.) that are maintained by the [MVPD](#mvpd) and provided by Adobe Pass Authentication as part of a [profile](#profile).

For more information, refer to the [User Metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md) documentation.

### V {#v}

#### VSA {#vsa}

The Video Subscriber Account (VSA) is an Apple developed framework provided to the [Programmer](#programmer) to enable a single sign-on user experience.

For more information, refer to the [Video Subscriber Account Framework](https://developer.apple.com/documentation/videosubscriberaccount) and [Single sign-on using partner flows](/help/authentication/integration-guide-programmers/rest-apis/rest-api-v2/flows/single-sign-on-access-flows/rest-api-v2-single-sign-on-partner-flows.md) documentation.
