---
description: You can provide custom metadata on content, ads, and chapter tracking calls by using callback functions.
title: Implement custom metadata support
exl-id: 59d56d5e-959d-4fb3-8434-55ae8219fca6
---
# Implement custom metadata support {#implement-custom-metadata-support}

You can provide custom metadata on content, ads, and chapter tracking calls by using callback functions.

Callback functions are invoked just before the tracking call is made, so your application can attach the metadata that is specific to an ad or chapter. 

   Invoke callback functions for content, ads, and chapters.

   ```java
   // Video Metadata Block 
   vaMetadata.setVideoMetadataBlock(new VideoAnalyticsMetadata.VideoMetadataBlock() { 
       @Override 
       public HashMap<String, String> call() { 
           HashMap<String, String> result = new HashMap<String, String>(); 
           result.put("myvideoid", "1234"); 
           result.put("mysdkversion", Version.getVersion()); 
     
           return result; 
       } 
   }); 
     
   // Ad Metadata Block invoked on every ad start 
   vaMetadata.setAdMetadataBlock(new VideoAnalyticsMetadata.AdMetadataBlock() { 
       @Override 
       public HashMap<String, String> call(Ad ad) { 
           HashMap<String, String> result = new HashMap<String, String>(); 
           result.put("myadid", "ad-1234"); 
           result.put("myad-sdkversion", Version.getVersion()); 
     
           return result; 
       } 
   }); 
     
   // Chapter Metadata Block invoked on every chapter start 
   vaMetadata.setChapterMetadataBlock(new VideoAnalyticsMetadata.ChapterMetadataBlock() { 
       @Override 
       public HashMap<String, String> call(VideoAnalyticsChapterData chapter) { 
           HashMap<String, String> result = new HashMap<String, String>(); 
           result.put("mychapterid", "chapter-1234"); 
           result.put("mychapter-sdkversion", Version.getVersion()); 
     
           return result; 
       } 
   });
   ```
