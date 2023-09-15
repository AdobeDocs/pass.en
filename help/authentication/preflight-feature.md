---
title: Preflight Feature, How to Enable, Troubleshoot or Determine the Issue
description: Preflight Feature, How to Enable, Troubleshoot or Determine the Issue
exl-id: 9e4ec343-371f-4116-915f-191e5f42cb47
---
# Preflight Feature: How to Enable, Troubleshoot or Determine the Issue {#preflight-feature}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

There has been a change in the way Adobe Pass authentication computes preAuthorizeResources. The PreAuthorization API has a new implementation. This implementation replaces the old solution which comprises making multiple authorization calls only.
The external interface for the PreAuthorization API is unchanged, no updates are required in the Programmer's application.

There are three ways the Preflight resources are computed:

* **Fork and join method to MVPD**: this involves Adobe making multiple authorization calls to the MVPD (the client will still have to make one preflight call though).
* **Channel line-up**: the MVPD exposes the channel line up for the logged in user in the SAML authentication response and Adobe returns the authorized resources based on that. The SAML authN response in the SAML tracer should expose that list.
* **Multi-channel authorization**: the client & Adobe authenication both make a single call to the MVPD for a set of resources.

Regardless of the MVPD, the Client application will make a single call to the Preflight endpoint (checkPreauthorizedResources API), passing a set of resourceIDs. Based on one of the above ways supported by MVPD, Adobe will then return the pre-authorized resourceIDs.

If Preflight is based on the fork & join method, then the Adobe Pass Authentication backend checks a value set for the 'max preauthorization calls' in its configuration. This is configured by Adobe.

The default value for 'max preauthorization calls' config is '5', meaning at max only 5 resources can be sent in Preflight for the fork & join MVPDs. Passing more than 5 resources will result in an exception and a null list will be returned. This is the expected behavior. We can configure this to any value if the MVPD does not support channel lineup or multi channel authorization, but only after consulting them as multiple fork & join authorization calls will increase their load times. 

Consequently, these are things to look for when enabling/troubleshooting Preflight for an MVPD:

* The method that the MVPD supports (fork & join, channel line-up or multi-channel).
* If only fork & join is supported, the Programmer needs to be asked how many resourceIDs it will be sending in the Preflight call.
* The MVPD needs to be consulted and needs to know the impact of making an 'n' number of fork & join authorization calls. Afterwards, the value must be configured in config if it is greater than 5.   
 
**Limitation**

Kindly note that we do not get any resourceID back from the Preflight call for some MVPDs like AT&T & TWC if any one of the resourceIDs is a fake ID or an unrecognized ID in the list of resourceIDs they send in the preflight call even though we have valid & authorized resources in that list too.
