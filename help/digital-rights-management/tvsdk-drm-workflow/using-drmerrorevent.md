---
title: Using the DRMErrorEvent class overview
description: Using the DRMErrorEvent class overview
copied-description: yes
exl-id: c651cdcf-f8f8-4085-a88e-d82030f90f11
---
# Using the DRMErrorEvent class {#using-the-drmerrorevent-class}

Primetime dispatches a `DRMErrorEvent` object when a Primetime object, trying to play protected content, encounters a [DRM-related error](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages). If user credentials are invalid, the `DRMAuthenticateEvent` object repeatedly dispatches until the user enters valid credentials or the application denies further attempts. The application is responsible for listening to any other DRM error events to detect, identify, and handle the [DRM-related errors](https://help.adobe.com/en_US/primetime/drm/index.html#reference-DRM_Client_Error_Messages).

Even with valid user credentials, the terms of the content's license can still prevent a user from viewing the encrypted content. For example, a user can be denied access for attempting to view content in an unauthorized application (e.g., Application Allow listing). An unauthorized application is one that has not been signed with a allow listed Application Signing Certificate. In this case, a `DRMErrorEvent` object is dispatched.

Error events can also be fired if the content is corrupted or if the application's version does not match what the license specifies. The application must provide an appropriate mechanism for handling errors.

## Create a DRMErrorEvent handler {#create-a-drmerrorevent-handler}

Create an event handler to process error events dispatched from Primetime when it encounters an error while trying to play protected content.

   Normally, when an application encounters an error, it performs any number of clean-up tasks. It then informs the user of the error and provides options for solving the problem. 

   ```
   private function drmErrorEventHandler(event:DRMErrorEvent):void {  
       trace(event.toString());  
   } 
   ```
