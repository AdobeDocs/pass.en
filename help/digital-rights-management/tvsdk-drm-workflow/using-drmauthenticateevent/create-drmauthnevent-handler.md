---
description: The DRMAuthenticateEvent object is dispatched when a Primetime object tries to play protected content that requires a user credential for authentication before playback (and authentication has not been performed yet). The DRMAuthenticateEvent handler is responsible for gathering the required credentials (user name, password, and type) and passing the values to the .setDRMAuthenticationCredentials() method for validation.
title: Create a DRMAuthenticateEvent handler
exl-id: fe01340b-8a76-4fd4-8c6c-85454d0e2218
---
# Create a DRMAuthenticateEvent handler{#create-a-drmauthenticateevent-handler}

The DRMAuthenticateEvent object is dispatched when a Primetime object tries to play protected content that requires a user credential for authentication before playback (and authentication has not been performed yet). The DRMAuthenticateEvent handler is responsible for gathering the required credentials (user name, password, and type) and passing the values to the .setDRMAuthenticationCredentials() method for validation.

The application must provide some mechanism for obtaining user credentials. For example, the application could provide a user with a simple user interface to enter user name and password values. Also, it should provide a mechanism for handling and limiting repeated authentication failure attempts. 

Create an event handler that passes a set of hard-coded authentication credentials to the Primetime object that originated the event:

   ```
   var connection:NetConnection = new NetConnection();  
   connection.connect(null);  
   var videoStream:Primetime = new Primetime(connection);  
    
   videoStream.addEventListener( 
     DRMAuthenticateEvent.DRM_AUTHENTICATE,  
     drmAuthenticateEventHandler)  
     private function drmAuthenticateEventHandler(event:DRMAuthenticateEvent):void {  
       videoStream.setDRMAuthenticationCredentials("administrator", "password", "drm");  
   } 
   ```

   (The code for playing the video and making sure that a successful connection to the video stream has been made is not included here.)
