---
title: Setting up Your Environment and Testing in Pre-Qual
description: Setting up Your Environment and Testing in Pre-Qual
exl-id: f822c0a1-045a-401f-a44f-742ed25bfcdc
---
# Setting up Your Environment and Testing in Pre-Qual{#setting-up-your-environment-and-testing-in-prequal}

>[!NOTE]
>
>The content on this page is provided for information purposes only. Usage of this API requires a current license from Adobe. No unauthorized use is permitted.

The purpose of this tech note is to help our partners set up their environment and start testing a new build deployed on the Adobe pre-qualification environment.

Since there are two build flavors: ***production*** and ***staging***, in this document we will focus on the production setup with the mention that all steps are the same for staging, only the URLs are different.

Steps 1 and 2 are setting up the test environment on one of the testing machines, step 3 is a verification of the basic flow and steps 4 & 5 are presenting some testing guidelines.

>[!IMPORTANT] 
>
> It is very important to execute steps 1 and 2 each time you want to change your testing environment (switching from staging to production profile or the other way around)
 

## STEP 1. Resolving Pass domain to an IP {#resolving-pass-domain-to-an-ip}

* To find a load balancer IP which can be used for spoofing, run the following command:

* **On Windows**

  ```cmd
  C:\>nslookup sp-prequal.auth.adobe.com
  ...
  Addresses:  52.13.71.11
              54.184.208.150
  ```

```Choose any IP from **addresses** section (e.g. `52.13.71.11)```

* **On Linux/Mac**

```sh
    $ dig sp-prequal.auth.adobe.com
    
    ;; ANSWER SECTION:
    ...
    ............ 60 IN A      52.13.71.11
    ............ 60 IN A      54.184.208.150
```    

```Choose any IP from **A records (**e.g `52.13.71.11)```

>[!NOTE] 
>
>Domains excluded from answer as they are not relevant and could differ from user to user.

>[!IMPORTANT] 
>
> These IP addresses may change in the future and they might not be the same for users in different geographical regions.


## STEP 2.  Spoofing the pre-qualification environment to be production {#spoofing-the-prequalification-environment}

* Edit the *c:\\windows\\System32\\drivers\\etc\\hosts* file (in Windows) or */etc/hosts* file (on Macintosh/Linux/Android) and add the following:
  
* Spoof production profile    
    * 52.13.71.11 entitlement.auth.adobe.com sp.auth.adobe.com api.auth.adobe.com

**Spoofing on Android:** In order to spoof on Android, you have to use an Android emulator.

* Once the spoofing is in place, you can simply use the regular URLs for the production and staging profiles: (that is, `http://sp.auth-staging.adobe.com` and `http://entitlement.auth-staging.adobe.com` and you will actually hit the *pre-qualification environment/ production* of the* new build.


## STEP 3.  Verify you are pointing to the right environment {#Verify-you-are-pointing-to-the-right-environment}

**This is an easy step:** 

* load [entitlement prequal environment](https://entitlement-prequal.auth.adobe.com/environment.html) and [entitlement](https://entitlement.auth.adobe.com/environment.html). They should return the same response.  


## STEP 4.  Perform a simple authentication/authorization flow using the programmer's website {#peform-a-simple-auth-flow}

* This step requires the programmer's website address and some valid MVPD credentials (a user that it is authenticated and authorized).

## STEP 5.  Perform scenario testing using the programmer's websites {#perform-scenario-testing-using-programmer-website}

* After completing the environment setup and ensuring that the basic authentication-authorization flow is working you can proceed with the testing of more complex scenarios.


## STEP 6.  Perform testing using the API test site {#perform-testing-using-api-testing-site}

* If you want to go deeper into testing Adobe Pass Authentication, we recommend you use the [API test site](http://entitlement-prequal.auth.adobe.com/apitest/api.html).

You can find more details on API test site at [How to test Authentication and Authorization flows using Adobe's API test site](/help/authentication/integration-guide-programmers/legacy/notes-technical/test-authn-authz-flows-using-adobes-api-test-site.md).
