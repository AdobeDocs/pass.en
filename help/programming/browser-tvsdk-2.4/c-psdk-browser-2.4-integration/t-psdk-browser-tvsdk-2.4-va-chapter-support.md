---
title: Implement chapter support
description: Implement chapter support
copied-description: yes
exl-id: 8a962706-50cd-41c2-96a7-6af1b24145a4
---
# Implement chapter support{#implement-chapter-support}

A chapter is defined as the time between each ad break. For example, the time between a pre-roll ad break and the first mid-roll is defined as the first chapter. You can define and track chapters for video tracking in a Browser TVSDK-based application using custom chapters. Custom chapters are managed by the application and are based on CMS data or another way that the application uses to define chapters. 

1. Define and track custom chapters.

   ```js
   vaObj.enableChapterTracking = true; 
     
   // For custom chapter definitions, provide an array of chapters through the metadata: 
   // For example: 3 chapters of 60 second duration each 
   var chapters = []; 
   var chapterDuration = 60; 
   for (var i = 0; i < 3; i++) { 
       var chapterData = new AdobePSDK.VA.VideoAnalyticsChapterData("chapter_" + (i+1), i * chapterDuration, chapterDuration, (i+1)); 
       chapters.push(chapterData); 
   } 
     
   vaObj.chapters = chapters;
   ```
