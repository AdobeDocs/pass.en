---
title: Set the XSTS token in your player
description: Set the XSTS token in your player
copied-description: yes
---

# Set the XSTS token in your player{#set-the-xsts-token-in-your-player}

In Xbox360, you set the token asynchronously in response to the `MediaPlayer.RequestKeyAttribute` event. 

Set the XSTS token.

   The sample app bundled with your software shows how to set the XSTS token in your player. Here is the relevant code snippet from the sample player: 

   ```
      MediaPlayer mMediaPlayer;  
    
   mMediaPlayer.RequestKeyAttribute += Player_RequestKeyAttribute;  
    
   private void Player_RequestKeyAttribute(object sender, RequestKeyAttributeEventArgs args) {  
       string token = "";  
       // XBOX XSTS Token...  
       KeyAttribute keyAttribute = new KeyAttribute(System.Text.Encoding.UTF8.GetBytes(token), null);  
       mMediaPlayer.SetKeyAttribute(args.RequestIdentifier, keyAttribute);  
   } 
   
   ```

