---
title: Create a DRMStatusEvent handler
description: Create a DRMStatusEvent handler
copied-description: yes
---

# Create a DRMStatusEvent handler{#create-a-drmstatusevent-handler}

The following example creates an event handler that outputs the DRM content status information for the Primetime object that originated the event. 

Add an event handler to a Primetime object that points to protected content:

   ```
   function drmStatusEventHandler(event:DRMStatusEvent):void { trace(event); } 
   ```

