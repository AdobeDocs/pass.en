---
title: Implement chapter support
description: Implement chapter support
copied-description: yes
exl-id: c6d9300e-33ce-4948-af5b-f28945fd47e4
---
# Implement chapter support {#implement-chapter-support}

You can define and track chapters for video tracking in a TVSDK-based application in the following ways:

* Default chapters, which are managed internally by TVSDK.

  A chapter is defined as the time between each ad break. For example, the time between a pre-roll ad break and the first mid-roll is defined as the first chapter. 
* Custom chapters, which are managed by the application and are based on CMS data or another way that the application uses to define chapters.

  Define and track default or custom chapters.

   ```
   // First, enable chapter tracking by setting the boolean 'enableChapterTracking' to true: 
    
       vaMetadata.enableChapterTracking = true; 
     
   // For custom chapter definitions, provide an array of chapters through the metadata:  
   // For example: 3 chapters of 60 second duration each 
    
       var chapters:Vector.<VideoAnalyticsChapterData> = new Vector.<VideoAnalyticsChapterData>(); 
       var chapterDuration:int = 60; 
       for (var i:int = 0; i < 3; i++) { 
           var chapterData:VideoAnalyticsChapterData =  
             new VideoAnalyticsChapterData(i * chapterDuration, (i + 1) * chapterDuration); 
           chapterData.name = "chapter_%d" + (i+1); 
     
           chapters.push(chapterData); 
       } 
     
       vaMetadata.chapters = chapters; 
     
   // For default chapters, the application must not set custom chapters on the tracking metadata  
   // and simply enable chapters to be tracked by setting the boolean value as defined above. 
   ```
