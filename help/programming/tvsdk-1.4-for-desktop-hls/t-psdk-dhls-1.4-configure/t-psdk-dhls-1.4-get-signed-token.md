---
description: The Flash Runtime TVSDK needs a signed token to validate that you have the right to call the TVSDK API on the domain where your application resides.
title: Load your signed token
exl-id: fef6b764-dc65-412e-a990-3f0b1fef94dd
---
# Load your signed token {#load-your-signed-token}

The Flash Runtime TVSDK needs a signed token to validate that you have the right to call the TVSDK API on the domain where your application resides.

1. Get a signed token from your Adobe representative for each of your domains (where each domain could be a specific domain or a wildcard domain).

       To get a token, provide Adobe with either the domain where your application will be stored or loaded, or, preferably, the domain as a SHA256 hash. In return, Adobe provides you with a signed token for each domain. These tokens take one of these forms:

    * An [!DNL .xml] file acting as the token for a single domain or wildcard domain.     
    
      >[!NOTE]
      >
      >A token for a wildcard domain covers that domain and all of its subdomains. For example, a wildcard token for the domain [!DNL mycompany.com] would also cover [!DNL vids.mycompany.com] and [!DNL private.vids.mycompany.com]; a wildcard token for [!DNL vids.mycompany.com] would also cover [!DNL private.vids.mycompany.com]. *Wildcard domain tokens are supported only for certain Flash Player versions.*

    * A [!DNL .swf] file containing token information for multiple domains (not including wildcards)(single or wildcard), which your application can load dynamically.

1. Store the token file in the same location or domain as your application.

   By default, TVSDK looks for the token in this location. Alternatively, you can specify the token's name and location in `flash_vars` in your HTML file.
1. If your token file is a single XML file:
   1. Use `utils.AuthorizedFeaturesHelper.loadFrom` to download the data stored at the specified URL (the token file) and extract the `authorizedFeatures` information from it.
   
      This step can vary. For example, you might want to perform authentication before starting the application, or you might receive the token directly from your content management system (CMS). 
   
   1. TVSDK dispatches a `COMPLETED` event if the load is successful or a `FAILED` event otherwise. Take appropriate action when you detect either event.
   
      This must be successful for your application to provide the required `authorizedFeatures` objects to TVSDK in the form of a `MediaPlayerContext`.

   This example shows how you can use a single-token [!DNL .xml] file.

   ```
   private function loadDirectTokenURL():void { 
       var url:String = constructAuthorizedFeatureTokenURL(); 
       _logger.debug("#onApplicationComplete Loading token from [{0}].", url); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE,  
           onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR,  
           onFeatureError); 
        _authorizedFeatureHelper.loadFrom(url); 
    }
   ```

1. If your token is a [!DNL .swf] file:
   1. Define a `Loader` class to dynamically load the [!DNL .swf] file.
   1. Set the `LoaderContext` to specify the loading to be in the current application domain, which allows TVSDK to choose the correct token within the [!DNL .swf] file. If `LoaderContext` is not specified, the default action of `Loader.load` is to load the .swf in the child domain of the current domain.
   1. Listen for the COMPLETE event, which TVSDK dispatches if the load is successful.
   
      Also listen for the ERROR event and take appropriate action.   
   1. If the load is successful, use the `AuthorizedFeaturesHelper` to get a `ByteArray` that contains the PCKS-7 encoded security data.
   
      This data is used through AVE V11 API to get authorization acknowledgment from the Flash Runtime Player. If the byte array has no content, instead use the procedure to look for a single-domain token file.   
   1. Use `AuthorizedFeatureHelper.loadFeatureFromData` to get the required data from the byte array.
   1. Unload the [!DNL .swf] file.

   The following examples show how you could use a multiple-token [!DNL .swf] file.

   **Multiple-token example 1:**

   ```
   private function onApplicationComplete(event:FlexEvent):void { 
       var url:String = constructAuthorizedFeatureTokenURLFromSwf();   
       _loader = new Loader(); 
       var swfUrl:URLRequest = new URLRequest(url); 
       var loaderContext:LoaderContext =  
           new LoaderContext(false, ApplicationDomain.currentDomain, null); 
       _loader.contentLoaderInfo.addEventListener(Event.COMPLETE,  
           modEventHandler); 
       _loader.contentLoaderInfo.addEventListener(IOErrorEvent.IO_ERROR,  
           errEventHandler); 
       _loader.contentLoaderInfo.addEventListener(ProgressEvent.PROGRESS,  
           onProgressHandler); 
       _loader.uncaughtErrorEvents.addEventListener(UncaughtErrorEvent. 
           UNCAUGHT_ERROR, uncaughtEventHandler); 
       _logger.debug("# Loading token swf with context from [{0}].", url); 
       _loader.load(swfUrl, loaderContext); 
   } 
     
   private function modEventHandler(e:Event):void { 
       _logger.debug("loadSWF with domainID {0}",  
       SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
           loader.contentLoaderInfo.applicationDomain. 
           getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       _authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       _authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       _authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray = myTokens. 
           FetchToken(SecurityDomain.currentDomain.domainID); 
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           _logger.debug("token bytearry size {0}", byteArray.length); 
           _authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
   
   ```

   **Multiple-token example 2:**

   ```
   private function tokenSwfLoadedHandler(e:Event):void { 
       trace("loadSWF with domainID {0}", SecurityDomain.currentDomain.domainID); 
       var loader : Loader = e.currentTarget.loader as Loader; 
       var myAuthorizedTokensLoaderClass:Class =  
         loader.contentLoaderInfo.applicationDomain. 
         getDefinition("AuthorizedTokensLoader") as Class; 
       var myTokens:Object = new myAuthorizedTokensLoaderClass(); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       var byteArray:ByteArray =  
           myTokens.FetchToken(SecurityDomain.currentDomain.domainID); 
       var myDomains:Array = ["domain.com"]; 
       if (byteArray == null || byteArray.length == 0) { 
           // check for wildcard tokens 
           if (myTokens.hasOwnProperty("FetchWildCardToken") == true) { 
               // contains wildcard domains 
               for each (var domain:String in myDomains) { 
                   byteArray = myTokens.FetchWildCardToken(domain); 
                   if (byteArray != null && byteArray.length != 0) { 
                       break; 
                   } 
               }; 
           } 
       } 
    
       if (myTokens == null || byteArray == null || byteArray.length == 0) 
           loadDirectTokenURL(); 
       else { 
           trace("token bytearry size {0}", byteArray.length); 
           authorizedFeatureHelper.loadFeatureFromData(byteArray); 
       } 
       _loader.unload(); 
   } 
    
   private function loadDirectTokenURL():void { 
       trace("#onApplicationComplete Loading token from [{0}].", tokenUrl); 
       authorizedFeatureHelper = new AuthorizedFeaturesHelper(); 
       authorizedFeatureHelper.addEventListener(Event.COMPLETE, onFeatureComplete); 
       authorizedFeatureHelper.addEventListener(ErrorEvent.ERROR, onFeatureError); 
       authorizedFeatureHelper.loadFrom(tokenUrl); 
   }
   ```
