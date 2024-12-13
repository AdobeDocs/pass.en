---
title: Tracking Prevention Assessment Google Chrome
description: Tracking Prevention Assessment Google Chrome
exl-id: f3d552da-2fd7-4ac8-9f82-876625af5d47
---
# (Legacy) Tracking Prevention Assessment - Google Chrome {#tracking-prevention-assessment-google-chrome}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

## Overview

This document aggregates useful resources and assesses the upcoming changes planned by Google Chrome as part of their initiative to phase out  3rd party cookies.

The assessment is performed for TV Everywhere (TVE) applications running on Google Chrome browser and which are using Adobe Pass Access Enabler JavaScript SDK v4 to integrate with the Adobe Pass Authentication backend services.

## Public Resources

See below a list of resources aggregated from Google's developer website and also from their official blog that we recommend our customers to consult:

* [The next step toward phasing out third-party cookies in Chrome](https://blog.google/products/chrome/privacy-sandbox-tracking-protection/)
* [Developer documentation for Privacy Sandbox](https://developers.google.com/privacy-sandbox)
* [Prepare for third-party cookie restrictions](https://developers.google.com/privacy-sandbox/3pcd)
* [Prepare for the third-party cookie phaseout](https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout)
* [Preparing for the end of third-party cookies](https://developers.google.com/privacy-sandbox/blog/cookie-countdown-2023oct)
* [Third-party cookies restricted by default for 1% of Chrome users](https://developers.google.com/privacy-sandbox/blog/cookie-countdown-2024jan)

## Timeline

As a brief summary Google Chrome started testing [Tracking Protection](https://privacysandbox.com/), a new feature that limits cross-site tracking affecting all 3rd party cookies.

Initially, this started at the beginning of 2024 affecting about 1% of their users and their (tentative) plan is to extend this for up to 100% of users starting from the third quarter of 2024. 

## Assessment

Google published a document aggregating their recommended playbook to prepare for the third-party cookies phase out at the following link: https://developers.google.com/privacy-sandbox/3pcd/prepare/prepare-for-phaseout.

We adhered to this playbook for the assessment of TV Everywhere (TVE) applications running on Google Chrome browser and which are using Adobe Pass Access Enabler JavaScript SDK v4 to integrate with the Adobe Pass Authentication backend services.

### Conclusions

Based on our testing, simulating the upcoming updates of Google Chrome, the primary TVE business flows **will continue to function as expected**.

However, it is crucial to recognize Google's broader strategy, which involves not only discontinuing third-party cookies but also partitioning third-party storage.

Consequently, Chrome users will experience disruptions with Single Sign-On (SSO), Single Logout (SLO) and passive authentication features, necessitating separate login / logout actions for each TVE application they use (aligning with the current experience on Safari).

## Call for self assessment

We urge our clients to proactively conduct similar evaluations to pinpoint potential issues well in advance and to familiarize themselves with the revised Google Chrome user experience.

This evaluation should encompass both first-party services and third-party services, especially concerning the Adobe Pass Access Enabler JavaScript SDK v4 integration.

In case you encounter any difficulties related to TVE business flows, including authentication, pre-authorization, authorization, user metadata, or logout, we invite you to file a report through a Zendesk ticket with our customer care team.

For assistance in developing your self-assessment plan please refer to below sections.

### Audit use of cookies

Starting with Chrome 118, the [DevTools Issues](https://developer.chrome.com/docs/devtools/issues/) tab highlights potentially affected cookies with the following message: `Cookie sent in cross-site context will be blocked in future Chrome versions`.

Cookies marked for third-party usage can be identified by their `SameSite=None` attribute value.

Follow this link to read more: https://developers.google.com/privacy-sandbox/3pcd/prepare/audit-cookies

### Test for breakage

In order to test for breakage either launch Chrome using the `--test-third-party-cookie-phaseout` command-line flag or from Chrome 118 enable `#test-third-party-cookie-phaseout` in `chrome://flags/`. 

This will set up Google Chrome to block third-party cookies and ensure that future functionality is active in order to best simulate the state after the phase out.

It is worth taking a deep dive in the technical specifications for the following Chrome flags:

* `#test-third-party-cookie-phaseout`
* `#third-party-storage-partitioning`

Follow this link to read more: https://developers.google.com/privacy-sandbox/3pcd/prepare/test-for-breakage

## Other browsers

### Firefox

Firefox had a roll-out of their mechanism called: `Enhanced Tracking Protection` a couple of years ago.

See below some useful resources from Firefox:

* https://support.mozilla.org/en-US/kb/enhanced-tracking-protection-firefox-desktop
* https://support.mozilla.org/en-US/kb/enhanced-tracking-protection-firefox-android

### Safari

Safari had a roll-out of their mechanism called: `Intelligent Tracking Prevention` a couple of years ago.

See below some useful resources from Safari:

* https://webkit.org/blog/9521/intelligent-tracking-prevention-2-3/
* https://webkit.org/blog/8828/intelligent-tracking-prevention-2-2/
* https://webkit.org/blog/8311/intelligent-tracking-prevention-2-0/
* https://webkit.org/blog/8142/intelligent-tracking-prevention-1-1/
* https://webkit.org/blog/7675/intelligent-tracking-prevention/

See below some useful resources from Adobe Pass:

* [Tracking Prevention Assessment - Apple Safari](tracking-prevention-assessment-apple-safari.md)
