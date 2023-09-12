---
title: Create a DRMErrorEvent handler
description: Create a DRMErrorEvent handler
copied-description: yes
---

# Create a DRMErrorEvent handler{#create-a-drmerrorevent-handler}

Create an event handler to process error events dispatched from Primetime when it encounters an error while trying to play protected content.

   Normally, when an application encounters an error, it performs any number of clean-up tasks. It then informs the user of the error and provides options for solving the problem. 

   ```
   private function drmErrorEventHandler(event:DRMErrorEvent):void {  
       trace(event.toString());  
   } 
   ```

