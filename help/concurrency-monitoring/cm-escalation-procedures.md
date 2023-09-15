---
title: Concurrency Monitoring escalation procedures
description: Concurrency Monitoring escalation procedures
---

# Concurrency Monitoring escalation procedures {#esc-procedures}

>[!NOTE]
>
>Call the hotline: +1-205-693-9813 and send an email to `tve-support@adobe.com` including "URGENT - INCIDENT" in the subject line.


## Introduction {#cm-escalation-intro}

This document describes the support procedures for major incidents (**SEVERITY 1** level) affecting Adobe Pass authentication, Adobe Pass Concurrency Monitoring and its partners.
 
## Definition of Escalation Severity 1 Level {#defn-escl-sevrityone-level}

A **SEVERITY 1** level incident is a **LIVE** situation, **happening in the production environment**, that does not allow the completion of the authentication and / or authorization flows for one channel and one MVPD, affecting a large number of subscribers of the MVPD performing the flow.

## Examples of Severity 1 incidents {#exampl-sevone-incident}

* The production Access Enabler hosted at <http://entitlement.auth.adobe.com/entitlement/AccessEnabler.js> is not available.

* For a specific MVPD, Adobe no longer redirects / displays the login page, after the user selects the MVPD (in any of the supported browsers).

* The partner receives a large number of reports that the users cannot authenticate/authorize with a specific MVPD.

* During the authentication process, the user is stuck on an Adobe error page without the possibility to re-initiate the authentication / authorization flow.


## Examples of what is *NOT* a Severity 1 incident {#exampl-not-sev1}

*For issues of these types, Adobe will provide support for investigations but they are not Severity 1 incidents:*

* One or a few subscriber(s) are not able to perform the flow due to a Flash version issue (missing Flash, Flash blockers, wrong Flash version).
* One or a few subscriber(s) are not able to authenticate and remain on the MVPD login page.
* One or a few subscriber(s) are authenticated but not able to play videos.
* One/few/all subscribers encounter a JavaScript error on the Programmer site.

## Severity 1 Escalation Flows {#sevone-escalation-flows}

Severity 1 incidents may be initiated by either Adobe or an Adobe Pass authentication partner. The steps for each are presented below.

### Partner-initiated Flow {#partner-initiated-flow}

1. The partner identifies a Severity 1 incident (as described above) requiring Adobe's immediate attention.

1. The partner sends an email to tve-support@adobe.com including "URGENT - INCIDENT" in the subject line and adding the following information:

    * Title
    * Description and steps to reproduce
    * OS
    * Browser
    * Flash Version
    * (optional) Any available screenshots or video captures demonstrating the issue

1. If Adobe does not respond to the ticket within 30 minutes, the partner calls the number below:

    * **1-205-693-9813**

   
**If you do not include "URGENT-INCIDENT" in the ticket's title it will not be picked up by our notification system.**
 
### Adobe initiated flow {#adobe-initiated-flow}

**...for an Adobe Pass authentication issue**
    
1. Adobe identifies an internal issue and opens a ticket with our tracking system. 

1. Adobe notifies the partner's program manager and technical contact, specifying the ticket number and the estimated impact of the issue. 

1. Adobe works towards the resolution of the incident and keeps all impacted partners informed.
 

**...for a partner issue (Programmer/MVPD)**

1.  Adobe identifies an issue related to the integration with an MVPD or on one of the Programmer's sites.

1. Adobe notifies the impacted partner **following the support procedures in place with that partner** and opens a ticket with the partner's support organization.

1. If, during the impact analysis, Adobe identifies that the issue belongs to one of the pre-agreed decisions on incident scenarios (see section "Pre-agreed decisions on incident scenarios" below), it will act accordingly without waiting for the partner1. 's input.

1. Adobe will wait for updates from the partner and a notification from the partner when the service has been restored.

### Pre-agreed Decisions on Incident Scenarios {#pre-agreed-decisions}

There are some situations in which a default action will be performed in the case of that scenario's occurence:

|    |                                                   Scenario                                                  |                                                                                                                               Description                                                                                                                              |                                                                                                      Actions                                                                                                     |
|:---:|:---|:---|:---|
| S1 | Adobe identifies an issue with an MVPD's integration during normal production operations.                   | During normal production operations, Adobe identifies a problem with one of the MVPDs which makes the performing of the authentication/authorization flows impossible to (e.g. expired certificates, expired SAML responses, ports closed, changed parameters, etc.)   | Adobe will notify the impacted MVPD and Programmers. Adobe will deactivate this MVPD for all affected Programmers. Adobe will open a ticket with the MVPD following the agreed support  procedure with that MVPD |
| S2 | Adobe activates a new MVPD for a Programmer, and the Programmer whitelists the MVPD before the launch date. | Adobe is activating a new MVPD for a Programmer's site, and the site is displaying the new MVPD in the picker already, even if it wasn't supposed to.                                                                                                                  | Adobe will notify the Programmer about the new MVPD appearing in the picker before the scheduled date. Programmer will take action to remove it from the picker if necessary.                                    |
| S3 | Adobe activates a new MVPD for a Programmer even if the MVPD is not ready to go in production               | Adobe is activating a new MVPD for a Programmer, but the MVPD has not yet deployed the support for the integration so the authentication/authorization flows cannot be performed                                                                                       | Adobe will do the deployment only if asked by the programmer The programmer will be responsible for ensuring the whitelisting of the MVPD once all the tests were performed.                                     |

### Response Expectations For Severity 1 Incidents {#response-expectations}

* Initial Response: 30 Minutes (24/7)
* Action Plan: 1 Hour (24/7)
* Resolution: ASAP (24/7)
