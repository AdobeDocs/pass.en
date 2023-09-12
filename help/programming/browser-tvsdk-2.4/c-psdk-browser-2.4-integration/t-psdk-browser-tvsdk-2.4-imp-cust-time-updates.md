---
description: In some analytics implementations, the client application might want to provide a different playhead position than the position reported by the Browser TVSDK localTime value.
title: Implement custom time updates
exl-id: 4d045c4d-298a-42ae-af61-0463a76bc872
---
# Implement custom time updates{#implement-custom-time-updates}

In some analytics implementations, the client application might want to provide a different playhead position than the position reported by the Browser TVSDK localTime value.

For example, during a linear stream playback, each program's playhead can be provided relative to its start time.

>[!TIP]
>
>Override this method only if you want to provide a playhead position other than the default position.

To override the default playhead position: 

```js
vaMetadata.currentTimeUpdateBlock = function() { 
       return playerPositionInSeconds; 
}; 

```

>[!IMPORTANT]
>
>The values in this code snippet are only samples. You need to use different values for your custom playhead position.
