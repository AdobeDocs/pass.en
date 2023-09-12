---
description: You can provide custom metadata on content, ads, and chapter tracking calls by using callback functions.
title: Implement custom metadata support
exl-id: d5d8b476-0f7c-434c-9386-d060a6eb99f9
---
# Implement custom metadata support {#implement-custom-metadata-support}

You can provide custom metadata on content, ads, and chapter tracking calls by using callback functions.

Callback functions are invoked just before the tracking call is made, so your application can attach the metadata that is specific to an ad or chapter. 

1. Invoke callback functions for content, ads, and chapters.

   ```
   // Video Metadata Block 
       vaTrackingMetadata.videoMetadataBlock = ^NSDictionary *() 
       { 
           return @{ 
                    @"myvideoid": @"1234", 
                    @"mysdkversion": [PTSDK apiVersion] 
                    }; 
       }; 
         
   // Ad Metadata Block invoked on every ad start 
       vaTrackingMetadata.adMetadataBlock = ^NSDictionary *(PTAd *ad) 
       { 
           return @{ 
                    @"myadid": @"ad-1234", 
                    @"myad-sdkversion": [PTSDK apiVersion] 
                    }; 
       }; 
         
   // Chapter Metadata Block invoked on every chapter start 
       vaTrackingMetadata.chapterMetadataBlock = ^NSDictionary *(PTVideoAnalyticsChapterData *chapter) 
       { 
           return @{ 
                    @"mychapterid": @"chapter-1234", 
                    @"mychapter-sdkversion": [PTSDK apiVersion] 
                    }; 
       };
   ```
