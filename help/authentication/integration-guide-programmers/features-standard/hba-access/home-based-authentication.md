---
title: Home-Based Authentication (HBA)
description: Home-Based Authentication (HBA)
exl-id: abdc7724-4290-404a-8f93-953662cdc2bc
---
# Home-Based Authentication (HBA) {#home-based-authentication}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted. 

Home-Based Authentication (HBA) is a TV Everywhere feature that allows pay-TV subscribers to access TV content online without entering MVPD credentials when connected to their home network, greatly enhancing the authentication experience.

According to the Open Authentication Technology Committee (OATC):

> "In-home automatic authentication is the process by which an MVPD/OVD uses characteristics of the home network (or identifiers automatically accessible between devices on the home network) to authenticate which subscriber account is associated with that home network, eliminating the need for users to manually enter credentials when initiating a TVE session for accessing protected content."

For more information on Home-Based Authentication (HBA) and the relevant industry standards, refer to the following resources:

>[!MORELIKETHIS]
>
> * [Instant Access (HBA) by CTAM](http://www.ctamtve.com/instantaccess)
> * [Home-Based Authentication Use Cases and Requirements by OATC](https://tve.helpdocsonline.com/topic/awsfiles/download_files?ref=https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/Defining%20TVE%20Home-Based%20Authentication%20(HBA)%20%20Use%20Cases%20and%20Requirements%20Recommended%20Practice%20Version%201_0%20FINAL%20DRAFT%20FOR%20BOARD%20APPROVAL.pdf)
> * [Home-Based Authentication Infographic by Adobe](https://tve.helpdocsonline.com/topic/awsfiles/download_files?ref=https://dzf8vqv24eqhg.cloudfront.net/userfiles/258/326/ckfinder/files/AdobeNewsletterHBA.pdf?dc=201604260953-2640)
> * [Authentication with OAuth2 enabled MVPDs](/help/authentication/integration-guide-mvpds/authn-oauth2-protocol.md)
> * [Authentication with SAML enabled MVPDs](/help/authentication/integration-guide-mvpds/authn-usecase.md)
> * [User Metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md)

## HBA benefits {#hba-benefits}

Home-Based Authentication (HBA) is a key feature that removes the sign-in barrier for viewers at home with an active cable subscription. This barrier is a significant challenge for TV Everywhere services, with nearly half of all sign-in attempts resulting in failure.

HBA can greatly improve viewer engagement, providing a seamless and superior user experience for accessing TV Everywhere content.

## HBA support {#hba-support}

>[!IMPORTANT]
>
> If you are interested in leveraging HBA functionality, please reach out to your Adobe Pass Authentication sales representative for more information as certain HBA flows are included in the Premium Workflow package.

HBA is supported by a number of MVPDs that are integrated with Adobe Pass Authentication, but to benefit from HBA, you might need to take some additional steps.

**SAML MVPDs**

For SAML MVPDs, HBA is activated only on the MVPD side.

**OAuth2 MVPDs**

For OAuth2 MVPDs, HBA can be toggled on or off via the [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication) by following the steps from the [TVE Dashboard Integrations User Guide](/help/authentication/user-guide-tve-dashboard/tve-dashboard-integrations.md#most-used-flows).

### MVPDs {#hba-support-mvpds}

**SAML MVPDs**

The following table provides an overview of the SAML enabled MVPDs that support HBA: 

| MVPD         | Basic functionality available? | Sends flag on authentication response? |
|--------------|--------------------------------|----------------------------------------|
| DirecTV      | Yes                            | No                                     |
| Dish         | Yes                            | No                                     |
| Spectrum     | Yes                            | Yes                                    |
| Cox          | Yes                            | No                                     |
| AT&T         | Yes                            | No                                     |
| Verizon      | Yes                            | Yes                                    |
| Cablevision  | Yes                            | No                                     |
| Mediacom     | Yes                            | No                                     |
| Midcontinent | Yes                            | No                                     |
| Massilon     | Yes                            | No                                     |
| AlticeOne    | Yes                            | Yes                                    |

**OAuth2 MVPDs**

The following table provides an overview of the OAuth2 enabled MVPDs that support HBA:

| MVPD    | Basic functionality available? | Sends flag on authentication response? |
|---------|--------------------------------|----------------------------------------|
| Comcast | Yes                            | Yes                                    |

### Adobe Pass Authentication {#hba-support-adobe-pass-authentication}

This section outlines the HBA-enabled experience and details the support provided by Adobe Pass Authentication, highlighting key features such as:

* **HBA Identification:** Capability to indicate to Programmers whether the authentication was HBA or non-HBA (requires MVPD support).
* **Configurable Authentication TTLs:** Ability to set different authentication Time-To-Live (TTL) values for HBA versus non-HBA authentications (requires MVPD support).

The following table provides a high-level overview of the user experience in an HBA and regular (non-HBA) authentication flow:

| Authentication Type | User Experience                                                                                                                                                                                                                 |
|---------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| HBA                 | Users select their MVPD and are automatically authenticated when connected to their home network. Once the authentication expires, users need to re-select their MVPD, after which they will be automatically re-authenticated. |
| Regular (non-HBA)   | Users select their MVPD and are prompted to enter their credentials, regardless of their connection to a home network. Once the authentication expires, users must re-select their MVPD and re-enter their credentials.         |

**SAML MVPDs**

The following table provides an overview of the HBA implementation in case of SAML enabled MVPDs:

| User Actions                                                                                                                                                                             | System Actions                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| The user attempts to play a video.<br/><br/>The MVPD picker is displayed.<br/><br/>The user selects their MVPD and continues to login.                                                   | A background check is conducted where the MVPD applies its rules for user identification. For example, this may involve mapping the user's IP address to the MAC address of distributor-provisioned modems or broadband-connected set-top boxes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| A screen that persists for approximately 3 seconds is displayed.<br/><br/>An interstitial page may inform the user that they are being automatically signed in using their MVPD account. | The application opens the authentication URL in a user agent, initiating an HTTP request to the Adobe Pass Authentication endpoint.<br/><br/>The Adobe Pass Authentication endpoint forwards the request to the MVPD's authentication endpoint via a user agent redirect.<br/><br/>The MVPD is expected to send an authentication decision in the form of a SAML response that includes the HBA flag (`hba_status`) with a value of either "true" or "false".<br/><br/>Adobe Pass Authentication backend makes a request to the MVPD user profile endpoint to expose the `hba_status` flag as part of the [user metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md). |
| The user is authenticated and can now browse entitled TV Everywhere content.                                                                                                             | The application retrieves the user profile and can further proceed with decisions flow to play content.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |

**OAuth2 MVPDs**

The following table provides an overview of the HBA implementation in case of OAuth2 enabled MVPDs:

| User Actions                                                                                                                                                                             | System Actions                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| The user attempts to play a video.<br/><br/>The MVPD picker is displayed.<br/><br/>The user selects their MVPD and continues to login.                                                   | A background check is conducted where the MVPD applies its rules for user identification. For example, this may involve mapping the user's IP address to the MAC address of distributor-provisioned modems or broadband-connected set-top boxes.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| A screen that persists for approximately 3 seconds is displayed.<br/><br/>An interstitial page may inform the user that they are being automatically signed in using their MVPD account. | The application opens the authentication URL in a user agent, initiating an HTTP request to the Adobe Pass Authentication endpoint.<br/><br/>The Adobe Pass Authentication endpoint forwards the request to the MVPD's authentication endpoint via a user agent redirect.<br/><br/>The MVPD authentication endpoint sends an authorization code to the Adobe Pass Authentication endpoint.<br/><br/>Adobe Pass Authentication uses the authorization code to request a refresh token and an access token from the MVPD's token endpoint.<br/><br/>The MVPD is expected to send an authentication decision that includes the HBA flag (`hba_status`) with a value of either "true" or "false" as part of the `id_token`.<br/><br/>Adobe Pass Authentication backend makes a request to the MVPD user profile endpoint to expose the `hba_status` flag as part of the [user metadata](/help/authentication/integration-guide-programmers/features-standard/entitlements/user-metadata.md).<br/><br/>The MVPD sets the refresh token TTL to an MVPD-agreed value and Adobe sets the authentication TTL to a value less or equal to the refresh token's value. |
| The user is authenticated and can now browse entitled TV Everywhere content.                                                                                                             | The application retrieves the user profile and can further proceed with decisions flow to play content.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | 

>[!IMPORTANT]
>
> In the HBA flow for MVPDs using the OAuth 2.0 authentication protocol, the MVPD issues a refresh token with a TTL defined by its business requirements, while Adobe issues an HBA authentication token with a TTL that must not exceed the refresh token's TTL.

## FAQs {#faqs}

1. Why is there a distinction between HBA implementation for SAML and OAuth2 protocols?

   The separation between Home-Based Authentication (HBA) for SAML and OAuth2 protocols exists because these protocols operate differently in terms of authentication mechanisms, configuration, and implementation flexibility. For SAML MVPDs, no action is required from the Programmer to enable HBA, while for OAuth2 MVPDs, HBA can be toggled on or off via the [Adobe Pass TVE Dashboard](https://experience.adobe.com/#/pass/authentication).

1. When HBA is enabled, do users still need to enter their username and password during their initial authentication?

   No, username and password are not required.

1. How can you enforce parental controls?

   Adobe Pass Authentication can disable HBA for integrations with channels that need parental control approval. Also, we are working with OATC on a UX document which recommends how to set up the HBA experience with parental controls. 

1. Do providers supporting HBA use shorter TTL windows for HBA compared to regular authentication?

   The TTL setting is configurable. We recommend setting a shorter TTL for MVPD integrations with HBA to prevent mishandling. 
