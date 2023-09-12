---
description: These classes assist in detecting opportunities in a timeline for placement of content, such as ads.
title: Timeline generators classes
exl-id: 2c9d1f10-fdf6-48b9-8bda-cee291befeab
---
# Timeline generators classes{#timeline-generators-classes}

These classes assist in detecting opportunities in a timeline for placement of content, such as ads.

 Package: [com.adobe.mediacore.timeline.generators](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/package-detail.html) 

|  Name  | Description  |
|---|---|
| [AdSignalingModeOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/AdSignalingModeOpportunityGenerator.html)  | Class which creates an initial opportunity for the specified advertising signaling mode.  |
| [OpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGenerator.html)  | Base class for all opportunity generators.  |
|  [OpportunityGeneratorClient](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/OpportunityGeneratorClient.html)  | Interface used by opportunity generators to communicate with TVSDK components.  |
| [SpliceOutOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/SpliceOutOpportunityGenerator.html)  | Class which monitors the playback timeline and detects ad placement opportunities inserted into the manifest as SpliceOut comments.  |
| [TimedMetadataOpportunityGenerator](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/generators/TimedMetadataOpportunityGenerator.html)  | Default implementation of an opportunity generator which is using timed metadata information to detect and generate advertisement opportunities.  |
