---
title: MVPD Direct Integration Plan
description: MVPD Direct Integration Plan
exl-id: 6423cc9a-a45a-4cde-b562-4cb72c98e505
---
# MVPD kickstart guide: MVPD direct integration plan {#mvpd-dir-int-plan}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

## Introduction {#mvpd-kickstart-intro}

Welcome to Adobe Pass Authentication for TV Everywhere.  We look forward to working with you.

>[!NOTE]
>
>This is the Kickstart Guide for Multichannel Video Programming Distributors (MVPDs). If you are a Programmer (content provider), see the [Programmers' Kickstart Guide](/help/authentication/kickstart/programmer-kickstart-guide.md).  

Support is available at all times through the Adobe Pass Authentication ticket system on Zendesk. This is also where you can find samples, documentation, and video tutorials for our processes. In order to use [Zendesk](https://adobeprimetime.zendesk.com/), you will have to register and create an account at https://tve.zendesk.com/home. There is no limit to the amount of users you can register and who can see or post comments on a filed ticket. All support questions should be addressed to: tve-support at adobe.com
 
**Team contacts**:

**Support** - For all questions, incidents, or feature requests **tve-support@adobe.com**.

## 1. Kick-off Meetings {#kickoff-meetings}

The scope for these meetings is the start of technical discussions between Adobe and the MVPD. At this point of the process, documentation needs to be shared from both sides. As a follow up, Adobe needs to open a ticket in our ticketing system (https://tve.zendesk.com/) to track the status of the integration. 

## 2. Features {#features}

Adobe will set up a weekly status call to discuss and track the overall schedule, steps, timeline, and implementation details of the integration. In this phase, Adobe does a review of the MVPD's specifications. The result of this should be a spec page that details all of the features needed by the MVPD. The MVPD will send Adobe a specification document, detailing the MVPD's authentication / authorization implementation.
 
Items to clarify, see [MVPD Integration Features](/help/authentication/integration-guide-mvpds/mvpd-integr-features.md).
 
There are several settings that will need to be described in detail at this point:

* **MVPD's logo URL** - This is a file with the following dimensions: 112 x 33 pixels. The logo is displayed by Programmers on their sites when the user clicks on the "Sign in" button to select their Pay TV provider. 
* **TTL (time-to-live) Values** - The TTL typically is set by the MVPD during the authentication/authorization process. However Adobe can override those TTL values and provide different values depending on what is agreed upon by both the Programmer and the MVPD. 
* **Display name** - This is displayed by Programmers on their sites when the user clicks on the "Sign in" button to select their Pay TV provider. 
* **Test credentials** - Both profiles (staging and production) should have a list of test credentials.

>[!IMPORTANT]
>
>Each time a user will initiate an entitlement flow he will be associated with a single, opaque, unique user ID.  The user ID is used to identify the user of a Programmer's app, but originates from the MVPD.

>[!CAUTION]
>
>An important notice for each MVPD: the user ID should NOT contain any PII (Personally Identifiable Information), information that can be used on its own or with other information to identify, contact, or locate the user.

## 2. Metadata exchange {#metadata-ex}

The two sides need to exchange the metadata for all environments involved (production, staging, etc.).

*   **Adobe** 
    * For the staging environment Adobe's SP metadata can be retrieved from: [Authentication staging sp metadata](https://sp.auth-staging.adobe.com/sp/metadata)
    * For the production environment Adobe's SP metadata can be retrieved from: [Authentication production sp metadata](https://sp.auth.adobe.com/sp/metadata)

*   **MVPD**
    * To add metadata (staging/production).

## 4. Allow IP list {#allow-ip-list}

The following IPs should be whitelisted in the MVPD's firewall. Please contact Adobe for the list of IPs. 

*   Adobe Pass Authentication requires that firewalls be opened on ports 80 and 443, for allowing access to restricted resources. 

*   The MVPD needs to add a list of IP addresses for authentication and authorization servers (if this is the case).

## 5. Development {#deve}

The duration of the development phase will be determined after reviewing the specifications, and taking into consideration the items the two sides sign off on. Adobe needs to write custom code for the authorization part. 

>[!NOTE]
>
>Note that authorization is performed per resource. The authorization transaction is typically performed with an ID string, passed from the Programmer's site, representing the channel for which the user is requesting authorization. This Resource ID is established between the Programmer and MVPD and can be as granular as necessary.

## 6. Adobe environments {#adobe-env}

Adobe provides different environments for different stages of the development process:

* **Prequalification** (PRE-QUAL): The PRE-QUAL environment contains the next release candidate. Adobe initially integrates new partners in this environment, before upgrading the integration to the Release environment. Partners have two weeks to test on the PRE‐QUAL environment and must explicitly request any changes to the PRE-QUAL configuration (contact your Adobe representative for details on the change request process). Bug fixes trigger new deployments in this environment.
* **Release** (RELEASE): Adobe's current production build is deployed to a live environment here. 

For more information on how to use Adobe's environments, see [Understanding the Adobe Environments](/help/authentication/notes-technical/understanding-the-adobe-environments.md)

## 7. Staging deployment {#stag-env}

Based on the metadata received from the MVPD, Adobe will create and configure a new MVPD in the Adobe Pass Authentication system. This will be deployed in Adobe's prequal staging environment, and will be configured with our test Programmer (TestDistributors). 
 
The MVPD needs to do the same deployment in their QA/staging/test environment.

## 8. Test and troubleshoot {#tes-troubleshoot}

In this phase, Adobe and the MVPD test and troubleshoot the integration. To help test the integration, the Adobe Pass Authentication team can use Adobe's API test site. To know more about using Adobe's API test site see [Test authentication and authorization flows using Adobe API test site](/help/authentication/notes-technical/test-authn-authz-flows-using-adobes-api-test-site.md). 

When testing and troubleshooting has concluded successfully, the integration is enabled in Adobe's release staging environment. At this point, Adobe can integrate the MVPD with an actual programmer. 

## 9. Production deployment {#prod-dep}

*   The MVPD needs to deploy first in the production profile, in order to test the connectivity. 

*   Adobe deploys in prequal production. 

*   All parties can now test in the production profile. 

*   If everything is ok at this point, Adobe can move the integration to the release production environment ("live"), which is available to all users.

## 10. Escalation procedures {#esc-proc}

Once the integration is live in production it is critical to provide the best customer experience. To ensure the best response in the case of a server down issue, MVPDs must provide escalation procedure documentation for issues brought to Adobe's attention. 

In turn, Adobe supplies MVPDs with the most current Adobe Pass Authentication escalation process.


<!--- [!RELATEDINFORMATION]
>
>* [Programmer Kickstart Guide](/help/authentication/programmer-kickstart-guide.md)
>* [MVPD Integration Guide](/help/authentication/mvpd-integr-features.md)
-->
