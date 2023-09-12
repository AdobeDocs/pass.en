---
description: The TVSDK player dispatches events to display custom ad loading status or to ignore an ad that is taking too long to load or has errors. These events are defined in events.CustomAdEvents.
title: Custom ad events
exl-id: 44f32584-7f6c-4071-82b6-9cc9584418ee
---
# Custom ad events{#custom-ad-events}

The TVSDK player dispatches events to display custom ad loading status or to ignore an ad that is taking too long to load or has errors. These events are defined in events.CustomAdEvents.

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Event </th> 
   <th colname="col2" class="entry"> Definition </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru </span> </td> 
   <td colname="col2"> The number of times the viewer clicked a custom ad. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError </span> </td> 
   <td colname="col2"> An error occurred with the custom ad. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded </span> </td> 
   <td colname="col2"> The custom ad has loaded.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading </span> </td> 
   <td colname="col2"> The custom ad is loading. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused </span> </td> 
   <td colname="col2"> The custom ad has paused. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed </span> </td> 
   <td colname="col2"> The custom ad has continued playing after a pause. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlaying </span> </td> 
   <td colname="col2"> The custom ad is playing. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress </span> </td> 
   <td colname="col2"> <p>The custom ad player notifies the TVSDK player about the progress of the custom ad. &amp;nbsp; </p> <p>The <span class="codeph"> currentTime </span> and <span class="codeph"> totalTime </span> of the ad are passed with this event. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> The custom ad has started playing and is displayed to the viewer.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> The custom ad has finished playing. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->
