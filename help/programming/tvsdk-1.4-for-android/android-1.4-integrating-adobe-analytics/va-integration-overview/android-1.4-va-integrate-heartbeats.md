---
description: You can configure your player to track and analyze video use.
title: Initialize and configure video analytics
exl-id: 82013882-e314-44fd-82f2-0640575d3c68
---
# Initialize and configure video analytics{#initialize-and-configure-video-analytics}

You can configure your player to track and analyze video use.

Before activating video tracking (video heartbeats), ensure that you have the following:

* TVSDK for Android 
* Configuration / Initialization Information - Contact your Adobe representative for your specific video-tracking account information: 

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="filepath"> ADBMobileConfig.json </span> </td> 
   <td colname="col2"> <p>Important:  This JSON config file name must remain <span class="codeph"> ADBMobileConfig.json </span>. The name and the path of this configuration file cannot be changed. The path to this file must be <span class="codeph"> &lt;source root&gt;/assets </span>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AppMeasurement tracking server endpoint </td> 
   <td colname="col2"> The URL of the Adobe Analytics (formerly SiteCatalyst) back-end collection endpoint. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Video analytics tracking server endpoint </td> 
   <td colname="col2"> The URL of the video analytics back-end collection endpoint. This is where all video heartbeat tracking calls are sent. <p>Tip:  The URL of the visitor tracking server is the same as the URL of the analytics tracking server. For information about implementing the Visitor ID Service, see <a href="https://experienceleague.adobe.com/docs/id-service/using/implementation/setup-target.html?lang=en" format="html" scope="external"> Implement ID Service </a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Account name </td> 
   <td colname="col2"> Also known as the Report Suite ID (RSID). </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Marketing Cloud organization ID </td> 
   <td colname="col2"> A string value required for instantiating the Visitor component. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Publisher </td> 
   <td colname="col2"> This is the Publisher ID, which is provided to customers by their Adobe representative. <p>Tip:  This ID is not just a string with the brand/television name. </p> </td> 
  </tr> 
 </tbody> 
</table>

To configure video tracking in your player: 

1. Confirm that load-time options in the `ADBMobileConfig.json` resource file are correct.

   ```
   { 
       "version" : "1.1", 
       "analytics" : { 
           "rsids" : "adobedevelopment", 
           "server" : "10.131.129.149:3000", 
           "charset" : "UTF-8", 
           "ssl" : false, 
           "offlineEnabled" : false, 
           "lifecycleTimeout" : 5, 
           "batchLimit" : 50, 
           "privacyDefault" : "optedin", 
           "poi" : [] 
       }, 
       "marketingCloud": { 
           "org": "ADOBE PROVIDED VALUE"  
       }, 
       "target" : { 
           "clientCode" : "", 
           "timeout" : 5 
       }, 
       "audienceManager" : { 
           "server" : "" 
       } 
   }
   ```

   This JSON-formatted configuration file is bundled as a resource with TVSDK. Your player reads these values only at load time, and the values remain constant while your application runs.

   To configure load-time options: 

   1. Confirm that the `ADBMobileConfig.json` file contains the appropriate values that are provided by Adobe.
   1. Confirm that this file is located in the `assets` folder.
   
      This folder must be located in the root of your application source tree.   
   1. Compile and build your application.
   1. Deploy and run the bundled application.
   
      For more information about these AppMeasurement settings, see [Measuring Video in Adobe Analytics](https://experienceleague.adobe.com/docs/media-analytics/using/media-overview.html?lang=en).   
1. Initialize and configure video heartbeat tracking metadata.

   >[!IMPORTANT]
   >
   >You can stop the video analytics module midstream and reinitialize it again as necessary. Before the module is reinitialized, ensure that the video analytics metadata is also updated to the correct content metadata. To recreate the metadata, repeat sub-steps 1 and 2.

   1. Create an instance of the Video Analytics metadata.
   
      This instance contains all of the configuration information that is needed to enable video heartbeat tracking. For example:    
   
      ```java   
      private VideoAnalyticsMetadata getVideoAnalyticsTrackingMetadata() { 
          VideoAnalyticsMetadata vaMetadata = new VideoAnalyticsMetadata(); 
        
          vaMetadata.setTrackingServer("example.com"); 
          vaMetadata.setPublisher("sample-publisher"); 
          vaMetadata.setChannel("test-channel"); 
          vaMetadata.setVideoName("myvideo"); 
          vaMetadata.setVideoId("myvideoid"); 
          vaMetadata.setPlayerName("PSDK Player"); 
          vaMetadata.setUseSSL(false); 
          vaMetadata.debugLogging = true; // Set to NO for production deployment. 
          vaMetadata.quietMode = false; // Set to NO for production deployment. 
          vaMetadata.setEnableChapterTracking(true); 
          // use this API to override the default asset length -1 for live streams 
          vaMetadata.setAssetDuration(SAMPLE_ASSET_DURATION); 
        
          return vaMetadata; 
      }
      ```

   1. Add the Video Analytics metadata to the global metadata instance.
   
      When you are ready, set the global metadata instance on the media resource or the media player item:

      ```java   
      ((MetadataNode)resourceMetadata).setNode( 
            DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY.getValue(), vaMetadata);
      ```   
   
   1. Initialize the Video Analytics tracker.
   
      After creating a media player instance, you must create a Video Analytics tracker instance and provide a reference to the media player instance.    
   
      >[!TIP]
      >
      >Always create a new tracker instance for each content playback session and remove the previous reference after you detach the media player instance.

      ```java   
      VideoAnalyticsProvider videoAnalyticsProvider =  
        new VideoAnalyticsProvider(appContext); 
       
      // Attach the TVSDK media player instance 
      videoAnalyticsProvider.attachMediaPlayer(mediaPlayer); 
      ```

   1. Destroy the Video Analytics tracker.
   
      Before you begin a new content playback session, destroy the previous instance of the video tracker. After you receive the content complete event (or notification), wait a few minutes before you destroy the video tracker instance. Destroying the instance immediately might interfere with the Video Analytics tracker's ability to send a video complete ping.

      ```java   
      if (_videoAnalyticsProvider) { 
          _videoAnalyticsProvider.detachMediaPlayer(); 
          _videoAnalyticsProvider = null; 
      }
      ```   
   
   1. Manually mark the Live/Linear stream as complete.
   
      If you have various episodes on one live stream, you can manually mark an episode as complete by using the complete API. This ends the video tracking session for the current video episode, and you can start a new tracking session for the next episode.    
   
      >[!TIP]
      >
      >This API is optional and is not needed for VOD video tracking.

      ```java   
      if (_videoAnalyticsProvider) { 
         _videoAnalyticsProvider.trackVideoComplete();    
      }
      ```
