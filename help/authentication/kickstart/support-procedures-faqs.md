---
title: Support procedures FAQs
description: Support procedures FAQs
exl-id: 1d754e5a-d5fa-4411-8932-2a36294da6eb
---
# Support procedures FAQs {#support-procedures-faqs}

>[!IMPORTANT]
>
> The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

This document outlines the frequently asked questions (FAQ) on support procedures for major incidents (SEVERITY 1 level) affecting Adobe Pass Authentication and its partners.

## FAQs {#faqs}

### What is a SEVERITY 1 level incident? {#support-procedures-faqs-1}

A SEVERITY 1 level incident is a live situation in the production environment that prevents the completion of authentication or authorization flows for one channel and one MVPD, impacting a large number of subscribers.

Examples of SEVERITY 1 Incidents

* During the authentication process, the user is not redirected to the login page after the user selects the MVPD in any supported browser.

* During the authentication process, the user is stuck on an Adobe error page without the ability to re-initiate the authentication flow.

* The partner receives numerous reports that users cannot authenticate or authorize with a specific MVPD.

* The production Access Enabler hosted at https://entitlement.auth.adobe.com/entitlement/v4/AccessEnabler.js is unavailable.

### What is a non-SEVERITY 1 level incident?

Adobe will support investigations for these issues, but they are not considered SEVERITY 1 level incidents:

* One or a few subscribers cannot authenticate and remain on the MVPD login page.

* One or a few subscribers are authenticated but cannot play videos.

* Some or all subscribers encounter a JavaScript error on the Programmer site.

### How are SEVERITY 1 level incidents handled?

A SEVERITY 1 level incident can be initiated by either Adobe or an Adobe Pass Authentication partner. The steps for each are outlined below.

**Partner-initiated flow**

1. The partner identifies a Severity 1 level incident requiring Adobe's immediate attention.

1. The partner sends an email to **tve-support@adobe.com** including **URGENT - INCIDENT** in the subject line and adding the following information:
    * Title
    * Description and steps to reproduce
    * OS / Browser
    * SDK & Version
    * Devices affected
    * % users affected
    * HTTP Trace or Device logs demonstrating the issue
    * (optional) Any available screenshots or video captures demonstrating the issue

1. If Adobe does not respond to the ticket within a period, the partner can call the following number: **1-657-312-4623**.

>[!IMPORTANT]
>
> If you do not include "URGENT-INCIDENT" in the ticket's title, it will not be picked up by our notification system.

**Adobe-initiated flow**

For an Adobe Pass Authentication issue:

1. Adobe identifies an internal issue and opens a ticket in our tracking system.

1. Adobe notifies the partner's program manager and technical contact, specifying the ticket number and the estimated impact of the issue.

1. Adobe works towards resolving the incident and keeps all impacted partners informed.

For a partner issue (Programmer/MVPD):

1. Adobe identifies an issue related to the integration with an MVPD or on one of the Programmer's sites.

1. Adobe notifies the impacted partner following the support procedures in place with that partner and opens a ticket with the partner's support organization.

1. If, during the impact analysis, Adobe identifies that the issue falls under one of the pre-agreed decisions on incident scenarios, it will act accordingly without waiting for the partner’s input.

1. Adobe will wait for updates from the partner and a notification when the service has been restored.

### What are pre-agreed decisions on incident scenarios?

Certain situations with default actions that will be performed if the scenario occurs:

|    | Scenario                                                                                               | Description                                                                                                                                                                                                                                                          | Actions                                                                                                                                                                                                                                 |
|----|--------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| S1 | Adobe identifies an issue with an MVPD's integration during normal production operations.              | During normal production operations, Adobe identifies a problem with one of the MVPDs which makes the performing of the authentication/authorization flows impossible to (e.g. expired certificates, expired SAML responses, ports closed, changed parameters, etc.) | Adobe will notify the impacted MVPD and Programmers.  </br></br> Adobe will deactivate this MVPD for all affected Programmers. </br></br> Adobe will open a ticket with the MVPD following the agreed support  procedure with that MVPD |
| S2 | Adobe activates a new MVPD for a Programmer, and the Programmer allow the MVPD before the launch date. | Adobe is activating a new MVPD for a Programmer's site, and the site is displaying the new MVPD in the picker already, even if it wasn't supposed to.                                                                                                                | Adobe will notify the Programmer about the new MVPD appearing in the picker before the scheduled date. </br></br>  Programmer will take action to remove it from the picker if necessary.                                               |
| S3 | Adobe activates a new MVPD for a Programmer even if the MVPD is not ready to go in production          | Adobe is activating a new MVPD for a Programmer, but the MVPD has not yet deployed the support for the integration so the authentication/authorization flows cannot be performed                                                                                     | Adobe will do the deployment only if asked by the programmer </br></br> The programmer will be responsible for ensuring the permit of the MVPD once all the tests were performed.                                                       |
