---
title: How to test Authentication and Authorization flows using Adobe's API test site
description: How to test Authentication and Authorization flows using Adobe's API test site
exl-id: 04af4aed-35e4-44cb-98ce-7643165a8869
---
# (Legacy) How to test Authentication and Authorization flows using Adobe's API Test site {#How-to-test-auth-flows}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

>[!IMPORTANT]
>
> Make sure you stay informed about the latest Adobe Pass Authentication product announcements and decommissioning timelines aggregated in the [Product Announcements](/help/authentication/product-announcements.md) page.

In order to test the AuthN and AuthZ flows, we have prepared an **API test site** which is at your disposal. Our support team will be happy to supply you with credentials. You can contact us at **support@tve.zendesk.com**.


## Part I {#part-I}

For testing against the RELEASE environment, skip directly to Part II.  In order to test in the pre-qualification environment, see [Setting up Your Environment and Testing in Pre-Qual](/help/authentication/notes-technical/environments/setting-up-your-environment-and-testing-in-prequal.md).

## Part II

After completing Part I, carry out the following steps:


1.  Open webpage: [Staging API test](https://sp.auth-staging.adobe.com/apitest/api.html).
1.  Load access enabler from the following URL:
    * [Access enabler javascript for staging](https://entitlement.auth-staging.adobe.com/entitlement/js/AccessEnabler.js). 
    * OR 
    * [Access enabler javascript for production](https://entitlement.auth.adobe.com/entitlement/js/AccessEnabler.js).
    * THEN click on the "**Load Access Enabler**" button.
1.  Now set the requestor id value to "**requestorID**" and click on the "setRequestor" button.
1.  After that press on the "getAuthentication" button and wait for the display picker to show up.
1.  Select the "**MVPD**" from the picker.
1.  Enter your credentials on the "**MVPD**" login page.
1.  After being redirected back, redo steps 1 to 3
1.  After redoing step 3 on the "setAuthenticationStatus" you should see the value "1". If the authentication did not work, the MVPD dialog box will be shown.
1.  To test authorization, in the resource input field enter "**requestorID**" and click on the "getAuthorization" button.
1.  As a result, in the "setToken"-\>"resource id" textbox the resource will be shown and in "setToken"-\>"token" textbox the shortAuthorizationToken will be shown meaning that authZ was successful.
1.  Now you can click on the "logout" button to delete the tokens.
