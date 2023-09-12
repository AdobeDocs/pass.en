---
description: These classes provide information about the timeline of the particular media, including the placement of ads.
title: Timeline classes
exl-id: bb879592-aef2-4adb-acbc-c927133a5cc5
---
# Timeline classes{#timeline-classes}

These classes provide information about the timeline of the particular media, including the placement of ads.

 Package: [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Name </th> 
   <th colname="2" class="entry"> <p>Description </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/PlacementOpportunity.html" format="html" scope="external"> PlacementOpportunity</a></span> </td> 
   <td colname="2"> An opportunity class represents a point of interest on the timeline. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Timeline</a> </td> 
   <td colname="2"> Interface that provides an iterator for processing timeline markers. Represents the timeline of the content, including ad breaks. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> TimelineItem</a> </span> </td> 
   <td colname="2"> Class. Generic immutable representation of a timeline item. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> TimelineMarker</a> </span> </td> 
   <td colname="2"> Interface that represents a marker on the timeline. This marks a region of interest on the actual timeline. Currently, the regions of interest are the ads, which you might want to mark, for example, with a different color on the scrub bar UI. Each marker is defined by a position and a duration (each expressed in milliseconds). </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineOperation.html" format="html" scope="external"> TimelineOperation</a> </td> 
   <td colname="2"> Base class for all operations that affect the timeline. </td> 
  </tr> 
 </tbody> 
</table>
