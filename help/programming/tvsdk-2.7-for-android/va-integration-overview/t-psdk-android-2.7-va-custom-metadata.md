---
description: You can provide custom metadata on content, ads, and chapter tracking calls by using callback functions.
title: Implement custom metadata support
exl-id: b14d3550-db25-4521-babd-ddfa6bc9f4f6
---
# Implement custom metadata support {#implement-custom-metadata-support}

You can provide custom metadata on content, ads, and chapter tracking calls by using callback functions.

Callback functions are invoked just before the tracking call is made, so your application can attach the metadata that is specific to an ad or chapter. 

1. Invoke callback functions for content, ads, and chapters.

   ```java
   // Video Metadata Block 
   // In a separate public class Implement an instance  
   // of VideoAnalyticsMetadata.VideoMetadataBlock 
    
   public class VideoMetadataBlockImpl  
     implements VideoAnalyticsMetadata.VideoMetadataBlock { 
    
       private final String video_id; 
       private final String player_version; 
    
       public VideoMetadataBlockImpl(String id, String version) { 
           this.video_id = id == null ? "" : id; 
           this.player_version = version == null ? "" : version; 
       } 
       @Override 
       public HashMap<String, String> call() { 
           HashMap<String, String> result = new HashMap<String, String>(); 
           result.put("videoid", video_id); 
           result.put("mysdkversion", player_version); 
           return result;   
       } 
   } 
   // Create an instance of the above created  
   // public class and assign it to vaMetadata 
   vaMetadata.setVideoMetadataBlock( 
     new VideoMetadataBlockImpl("1234", "1.2.3.4")); 
    
   // Ad Metadata Block that is invoked on every ad start 
   // In a separate public class Implement an instance of  
   // VideoAnalyticsMetadata.AdMetadataBlock 
    
   public class AdMetadataBlockImpl  
     implements VideoAnalyticsMetadata.AdMetadataBlock { 
    
       private final String ad_id; 
       private final String ad_sdkversion;

       public AdMetadataBlockImpl(String id, String version) { 
           this.ad_id = id == null ? "" : id; 
           this.ad_sdkversion = version == null ? "" : version; 
       } 
    
       @Override 
       public HashMap<String, String> call() { 
           HashMap<String, String> result = new HashMap<String, String>();\ 
           result.put("myadid", ad_id); 
           result.put("myad-sdkversion", ad_sdkversion); 
           return result; 
       } 
   } 
   // Create an instance of above created  
   // public class and assign it to vaMetadata 
   vaMetadata.setAdMetadataBlock( 
     new AdMetadataBlockImpl("ad-1234", "1.2.3.4")); 
    
   // Chapter Metadata Block that is invoked on every chapter start 
   // In a separate public class Implement an instance of  
   // VideoAnalyticsMetadata.ChapterMetadataBlock 
    
   public class ChapterMetadataBlockImpl  
     implements VideoAnalyticsMetadata.ChapterMetadataBlock { 
    
       private final String chapter_id; 
       private final String chapter_sdkversion; 
    
       public ChapterMetadataBlockImpl(String id, String version) { 
    
           this.chapter_id = id == null ? "" : id; 
           this.chapter_sdkversion = version == null ? "" : version; 
       } 
    
       @Override 
       public HashMap<String, String> call() { 
    
           HashMap<String, String> result = new HashMap<String, String>(); 
           result.put("mychapterid", chapter_id); 
           result.put("mychapter-sdkversion", chapter_sdkversion); 
           return result; 
    
           } 
   } 
   // Create an instance of above created public class and  
   // assign it to vaMetadata 
   vaMetadata.setChapterMetadataBlock( 
     new ChapterMetadataBlockImpl("chapter-1234", "1.2.3.4")); 
   
   ```
