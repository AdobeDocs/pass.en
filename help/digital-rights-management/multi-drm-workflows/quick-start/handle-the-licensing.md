---
description: Licensing is the primary mechanism by which users are allowed or denied the ability to play a piece of protected video content. A legitimate (entitled) user can be issued a license (a key) to decrypt and play a specific piece of their content provider's encrypted content.
title: Licensing
exl-id: 60aa3e77-f821-41b3-ba0e-1a2c05b2bb1a
---
# Licensing{#licensing}

Licensing is the primary mechanism by which users are allowed or denied the ability to play a piece of protected video content. A legitimate (entitled) user can be issued a license (a key) to decrypt and play a specific piece of their content provider's encrypted content.

Before your app or web page on an end-user's device can play DRM-protected content, it must acquire a token from an entitlement or storefront server that you, the customer, operate. Adobe provides a sample reference server for this purpose: [Reference Server: Sample ExpressPlay Entitlement Server (SEES)](../../multi-drm-workflows/feature-topics/sees-reference-server.md).

Your entitlement or storefront server will request a license token from the relevant ExpressPlay Server, only after checking with your own back end systems to determine if the specific user is entitled to watch the requested content. The response returned from the license token request is either a ready-to-use URL for the license server, or the response contains the URL in a JSON structure, depending upon the DRM solution you are working with. 

>[!NOTE]
>
>The license token request cannot be made from the client itself:
>1. The entitlements must be checked in a trusted environment; and 
>1. The customer authenticator must be kept secret. 

1. Make the license token request.

   For a quick-start scenario, in which you merely want to make sure that the various components involved are working together, you may want to use something like [!DNL curl] to make your license token request, (as opposed to initially getting an app up and running and testing calls from there). For example:

   * Widevine:     

   ```    
   curl "https://wv-gen.test.expressplay.com/hms/wv/token?customerAuthenticator= 
   <Customer Authenticator> 
   &kid 
   <indexterm>
   CEKSID 
     <indexterm>
     as query parameter kid 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEKSID> 
      &contentKey 
    <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    Widevine 
    </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>WidevineToken 
   ```

   Sample Widevine test token:     

   ```    
   https://wv.test.expressplay.com/widevine/RightsManager.asmx?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ 
      
   ```    

   Note that the Widevine response is a "ready-to-use" URL string. 
    
    * PlayReady:     

   ```    
   curl "https://pr-gen.test.expressplay.com/hms/pr/token?customerAuthenticator= 
   <Customer Authenticator> 
      &kid 
   <indexterm>
   CEKSID 
   <indexterm>
   as query parameter kid 
   <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<Key ID> 
      &contentKey 
   <indexterm>
    CEK 
    <indexterm>
    as query parameter contentKey 
    <indexterm>
    PlayReady 
   </indexterm> 
   </indexterm> 
   </indexterm>=<CEK> 
      &<Any additional licensing attributes desired>" >>playreadyToken
   ```    

   Sample PlayReady test token:     

   ```    
   {"licenseAcquisitionUrl":"https://pr.test.expressplay.com/playready/RightsManager.asmx", 
   "token":"AQAAAxBbWv4AAABgV8_GaWjU80mObLQdfwEdy1lenXmcqvx5VLyqixigtwXLthzjPxq9QDT-TYbudNrMSOpUAy 
   G_2Qt8RdTGJ2_Q_xtRfnj7H6C-yt6By40IhNaSQ0nNYUsY1_MtCrHXIltlVhN2Ekr_RNyTNvCjYs0V5TqzOPY"} 
      
   ```

   Note that the PlayReady response is a JSON object, with separate URL and token elements. 
    
   * FairPlay:     

   ```    
   curl "https://fp-gen.test.expressplay.com/hms/fp/token?customerAuthenticator= 
    <Customer Authenticator> 
    &kid 
    <indexterm>
      CEKSID 
    <indexterm>
      as query parameter kid 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<Key ID> 
          &contentKey 
    <indexterm>
      CEK 
    <indexterm>
      as query parameter contentKey 
      <indexterm>
        FairPlay 
      </indexterm> 
    </indexterm> 
    </indexterm>=<CEK> 
    &iv=<IV ID> 
    &<Any additional licensing attributes desired>"
   ```

      Sample FairPlay test token:

      ```    
      https://{expressplay_test_domain_license_url}/?ExpressPlayToken= 
      AQAAAJJ2Y0MAAABQbyvnJ6KgEg_w-2yZmU-MsjTEZ3f7UkhUcFhDFAvdonzBk 
      RGQU-xe1G-DMbel5-BVH_PozovdWhKZx0_SXRokfh9-FERmBl6OEfGfPqMI1e 
      O1PqRkx59Q2q1s2cFNrqfml8Y3RQ
      ```

      Note that the FairPlay response is a "ready-to-use" URL string.
