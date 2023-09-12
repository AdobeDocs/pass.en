---
description: You can configure your player to track and analyze video use.
title: Initialize and configure video analytics
exl-id: 58d560d1-f668-4e1d-a817-b2e02008fdbe
---
# Initialize and configure video analytics{#initialize-and-configure-video-analytics}

You can configure your player to track and analyze video use.

Before activating video tracking (video heartbeats), ensure that you have the following:

* TVSDK for Desktop HLS 
* Configuration / Initialization Information - Contact your Adobe representative for your specific video-tracking account information: 

<table id="table_3565328ABBEE4605A92EAE1ADE5D6F84"> 
 <tbody> 
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
   <td colname="col1"> Visitor tracking server endpoint </td> 
   <td colname="col2"> The URL of the back-end endpoint that provides a unique identifier for the current video viewer. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Publisher </td> 
   <td colname="col2"> This is the Publisher ID, which is provided to customers by their Adobe representative. <p>Tip:  This ID is not just a string with the brand/television name. </p> </td> 
  </tr> 
 </tbody> 
</table>

To configure video tracking in your player: 

1. Instantiate and configure the VisitorAPI library.

       Keep the following information in mind:

    * Instantiation requires a Marketing Cloud organization ID input parameter that is provided by Adobe.

      This is a string value. 
    * The only configuration option for the VisitorAPI library is the URL of the back-end endpoint that provides the unique identifier for the current user. 
    * The URL of the visitor tracking server is the same as the URL of the analytics tracking server.

      For information about implementing the Visitor ID Service, see Visitor ID Service Implementation.

   ```
   var_visitor = new Visitor("MARKETING_CLOUD_ORG_ID"); 
   _visitor.trackingServer = "URL_OF_THE_VISITOR_TRACKER_SERVER”; 
    
   ```

1. Instantiate and configure the AppMeasurement component.

   The AppMeasurement instance has many configuration options. For more information, see the [Adobe Analytics Developer](https://microsite.omniture.com/t2/help/en_US/reference/#Developer) documentation. The options in the following sample code ( `account`, `visitorNamespace`, and `trackingServer`) are required, and the values are provided by Adobe. 

   >[!IMPORTANT]
   >
   >You must ensure that the dependency chain is correctly set up. The AppMeasurement instance aggregates (depends on) the Visitor API component.

   ```
   // Instantiate and configure AppMeasurement 
    
   // Instantiate AppMeasurement instance only once! 
   if (_appMeasurementObject == null) {  
       _appMeasurementObject = new AppMeasurement(); 
   } 
    
   with (_appMeasurementObject) { 
       account = "ACCOUNT_NAME"; // Also known as RSID 
       trackingServer = "URL_OF_THE_ADOBE_ANALYTICS_TRACKING_SERVER"; 
    
       // Use the same value here as for the Visitor API component 
       visitorNamespace = "MARKETING_CLOUD_ORG_ID"; 
    
       // Attach the Visitor API to the AppMeasurement instance. 
       visitor = _visitor;  
       pageName = "pageName"; 
       charSet = "UTF-8"; 
       currencyCode = "USD"; 
   } 
   
   ```

   >[!IMPORTANT]
   >
   >In your application, ensure that `appMeasurementObject.visitor` is populated before initiating the video analytics flow, or you might not get any tracking results. These results are indicated by the  messages in your log. You can add an empty track call ( `appMeasurementObject.track`), poll the `visitor` property until it is populated, and initiate video analytics.

1. Initialize and configure video heartbeat tracking metadata.

   >[!IMPORTANT]
   >
   >You can stop the video analytics module midstream and reinitialize it again as necessary. Before the module is reinitialized, ensure that the video analytics metadata is also updated to the correct content metadata. To recreate the metadata, repeat sub-steps 1 and 2.

   1. Create an instance of the Video Analytics metadata.
   
      This instance contains all of the configuration information that is needed to enable video heartbeat tracking. For example:    
   
      ```   
      private function getVideoAnalyticsTrackingMetadata():VideoAnalyticsMetadata {     
          // Initialize visitor id service and appMeasurement      
          [...] // as shown in the previous steps     
       
          var vaMetadata:VideoAnalyticsMetadata = new VideoAnalyticsMetadata(); 
       
          with (vaMetadata) { 
              trackingServer = "hbTrackingServer"; 
              publisher = "hbPublisher"; 
              channel = "hbChannel";  
              playerName = "hbPlayerName"; 
       
              // this overwrites the ContextData variable a.media.friendlyName 
              videoName = "hbFriendlyName";  
       
              // this will overwrite the ContextData variable a.media.name 
              videoId = "hbName"; 
       
              enableChapterTracking = true; 
       
              // Set these to false for production deployment 
              debugLogging = true;  
              quietMode = false; 
       
          } 
      } 
      
      ```

   1. Add the Video Analytics metadata to the global metadata instance.
   
      When you are ready, set the global metadata instance on the media resource or the media player item:

      ```   
      var resourceMetadata:Metadata = _player.currentItem.resource.metadata; 
      resourceMetadata.setMetadata(DefaultMetadataKeys.VIDEO_ANALYTICS_METADATA_KEY,  
                                   getVideoAnalyticsTrackingMetadata());
      ```   
   
   1. Initialize the Video Analytics tracker.
   
      After creating a media player instance, you must create a Video Analytics tracker instance and provide a reference to the media player instance.    
   
      >[!TIP]
      >
      >Always create a new tracker instance for each content playback session and remove the previous reference after you detach the media player instance.

      ```   
      _videoAnalyticsProvider = new VideoAnalyticsProvider(_appMeasurementObject); 
      _videoAnalyticsProvider.attachMediaPlayer(_player);
      ```

   1. Destroy the Video Analytics tracker.
   
      Before you begin a new content playback session, destroy the previous instance of the video tracker. After you receive the content complete event (or notification), wait a few minutes before you destroy the video tracker instance. Destroying the instance immediately might interfere with the Video Analytics tracker's ability to send a video complete ping.

      ```   
      if (videoAnalyticsTracker) { 
          videoAnalyticsTracker.detachMediaPlayer(); 
          videoAnalyticsTracker = null; 
      }
      ```   
   
   1. Manually mark the Live/Linear stream as complete.
   
      If you have various episodes on one live stream, you can manually mark an episode as complete by using the complete API. This ends the video tracking session for the current video episode, and you can start a new tracking session for the next episode.    
   
      >[!TIP]
      >
      >This API is optional and is not needed for VOD video tracking.
