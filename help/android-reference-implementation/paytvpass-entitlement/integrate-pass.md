---
description: Customize your reference implementation to integrate Adobe Primetime authentication for your production environment.
title: Integrate Primetime authentication
exl-id: ef6dc75d-d00f-481f-a620-4ec402cbebb6
---
# Integrate Primetime authentication {#integrate-primetime-authentication}

Customize your reference implementation to integrate Adobe Primetime authentication for your production environment.

The Reference Implementation integration of the Primetime authentication service works out-of-the-box as a demonstration. However, to use the integration in a production-ready player, you must implement the following customizations: 

1. Enable or disable entitlement flows.

   The `EntitlementManager` must first initialize and obtain an instance of the Primetime authentication SDK to be enabled. If the `EntitlementManager` does not initialize this library, the manager will be disabled.
1. Enable the `EntitlementManger`, from your main application class:

   ```java   
   // initialize the AccessEnabler library, required for Primetime PayTV Pass entitlement workflows 
   EntitlementManager.initializeAccessEnabler(this); // comment out this line to disable entitlement workflows
   ```

1. Use the `ManagerFactory` class to obtain an instance of the `EntitlementManager`.

   You must always use the `ManagerFactory` to get an instance of the `EntitlementManager`, as the `ManagerFactory` maintains a single instance of the EntitlementManager for your application. Never instantiate the `EntitlementManager` or `EntitlementManagerOn` classes by using their constructors.

   ```java
   EntitlementManager entitlementManager =  
   ManagerFactory.getEntitlementManager();
   ```

   The `ManagerFactory` returns an instance of `EntitlementManagerOn`, with the entitlement flows enabled, if you previously called `EntitlementManager.initializeAccessEnabler`. If you do not first call `EntitlementManager.initializeAccessEnabler`, then the `ManagerFactory` will return an instance of `EntitlementManager`, with the entitlement flows disabled. 1. Configure the Requestor ID.

   The Reference Implementation comes pre-configured with the test Requestor ID set to: "REF". You can use this Requestor ID to test your application. When you are ready to use the Requestor ID provided to you by your Primetime authentication representative, update the application's [!DNL res/values/strings.xml] file with your Requestor ID. 

   ```xml
   <!-- Programmer Requestor ID, change to ID provided by your Adobe  
        Primetime pay-TV pass representative --> 
   <string name="adobepass_requestor_id">REF</string> 
    
   <!-- Adobe Primetime pay-TV pass service provider endpoint for production 
        environment --> 
   <string name="adobepass_sp_url_production">sp.auth.adobe.com</string> 
    
   <!-- Adobe Primetime pay-TV pass service provider endpoint for staging  
        environment --> 
   <string name="adobepass_sp_url_staging">sp.auth-staging.adobe.com</string>
   ```

   Additionally, you may need to change the URLs that your application uses to connect to the Primetime authentication services. These include the Primetime authentication staging and production server URLs, and a URL to a Token Verification Service. Check with your Adobe Primetime representative for details. 1. Sign the Requestor ID.

   In order to establish the identity of the Programmer within the Primetime authentication system, the Programmer's Requestor ID is send to the Primetime authentication system. As an added layer of security, the Requestor ID must be signed by the Programmer prior to sending it to Adobe. Adobe recommends that the Programmer setup a service to sign the Requestor ID on a trusted network.

   The Primetime Reference Implementation demonstrates how to sign the Requestor ID, however this is for demonstration purposes only. Adobe strongly recommends that the signing certificate and the signature generator code, under `com.adobe.primetime.reference.crypto`, should not be included within a production application. Instead, you should move it to a trusted networked service. 

1. Configure the Server Environment.

   The Primetime authentication service can run in two separate environments:

   * Staging - The staging environment is used for testing your application. 
   * Production - The production environment is used for live deployments of your application.

   You set the URIs for both the staging and production environments using the application, however you must set which of these is used by the application within the code. In the `com.adobe.primetime.reference.manager.EntitlementManger` class, set the `environmentUri` variable to either `STAGING_URI` or `PRODUCTION_URI` depending on which Primetime authentication service environment you are using.     
  
   >[!NOTE]
   >
   >The provided Requestor ID ("REF") should only be used with the staging environment.

   `com.adobe.primetime.reference.manager.EntitlementManager`:

   ```java    
     // Adobe Primetime authentication service provider endpoint for production environment 
     PRODUCTION_URI = 
         application.getResources().getString(R.string.adobepass_sp_url_production); 
        
     // Adobe Primetime authentication service provider endpoint for staging environment 
     STAGING_URI = 
       application.getResources().getString(R.string.adobepass_sp_url_staging); 
        
     // Set to STAGING_URI when testing against the staging/test environment 
     // Set to PRODUCTION_URI when deploying the application for production use 
     String environmentUri = STAGING_URI; 
        
     // Adobe Primetime authentication service URI used by this application 
     PAYTV_PASS_URI = environmentUri + "/adobe-services"; 
        
     // Token Verification Service URL 
     TVS_URL = "https://" + environmentUri + "/tvs/v1/validate";
   ```

1. Customize the MVPD Selection Grid.

   The content provider selection page displays a table of the top nine MVPDs the user may select from. The application pulls the top nine MVPDs from an ordered list within the application that match the available MVPDs integrated with the Programmer in the Primetime authentication system. The ordered list of the primary MVPDs is keyed on the MVPD ID within the Primetime authentication system, not the MVPD display name. It is important to verify that the MVPD IDs in the primary MVPDs list match the MVPD IDs integrated with the Programmer's account, as in some cases the IDs may be different across integrations. Below is the ordered list of primary MVPDs that is found in the class `com.adobe.primetime.reference.ui.entitlement.MvpdPickerFragment`. 

   ```java
   /* Array of MVPDs to display in a Grid of icons 
   When displaying a grid, only the MVPDs which intersect this array and the 
   ArrayList of all MVPDs are displayed. 
   The array contents are ordered by display preference as only a maximum of 
   MAX_DISPLAY_ICONS are displayed. 
   */ 
   private static final String[] PRIMARY_MVPDS = { 
   "Comcast_SSO",                         // Comcast XFINITY 
   "DTV",                                 // DirectTV 
   "Dish",                                // Dish 
   "TWC",                                 // Time Warner Cable 
   "Cox",                                 // Cox 
   "Charter_Direct",                      // Charter 
   "Verizon",                             // Verizon FiOS 
   "Cablevision",                         // Cablevision Optimum 
   "ATT",                                 // AT&T U-verse 
   "Brighthouse",                         // Brighthouse 
   "Suddenlink",                          // Suddenlink 
   "Mediacom",                            // Mediacom 
   "CableOne",                            // CableOne 
   "WOW",                                 // WOW! 
   "RCN",                                 // RCN 
   "auth_atlanticbb_net",                 // Atlantic Broadband 
   "auth_armstrongmywire_com",            // Armstrong 
   "knology_auth-gateway_net",            // KNOLOGY 
   "serviceelectric_auth-gateway_net",    // Service Electric Cablevision 
   "msauth_midco_net",                    // Midcontinent Communications 
   "auth_metrocast_net",                  // MetroCast 
   "www_websso_mybrctv_com",              // Blue Ridge Communications 
   };
   ```

   The following table provides an example of how the ordered list of primary MVPDs is used. The first column lists the MVPDs integrated with the Programmer. The second column is the (shortened) ordered list of MVPDs. The third column is the result list used to display the top six MVPDs to the user.

   This example uses the top six MVPDs instead of the actual nine just to keep the example simple. Notice how the result list contains the intersection of the first two lists and has the same ordering as the second list. Also, notice that AT&T U-verse is not in the final list, as only the first matching six MVPDs are taken. 

|Available MVPDs|Primary MVPDs|Displayed 6 MVPDs|
|--- |--- |--- |
|<ol><li>Comcast XFINITY</li><li>TWC</li><li>Mediacom</li><li>RCN</li><li>Dish</li><li>AT&T U-verse</li><li>CableOne</li><li>Brighthouse</li><li>Atlantic Broadband</li><li>WOW!</li><li>MetroCast</li><li>DirectTV </li><li>Cox</li><li>Cablevision Optimum</li></ol>|<ol><li>Comcast XFINITY</li><li>DirectTV</li><li>Dish</li><li> TWC</li><li>Cox</li><li>Charter</li><li>Verizon FiOS</li><li>Cablevision Optimum</li><li>AT&T U-verse</li></ol>|<ol><li>Comcast XFINITY</li><li>DirectTV</li><li>Dish</li><li>TWC</li><li>Cox</li><li>Cablevision Optimum</li></ol>|
