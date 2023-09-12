---
description: Quality of service (QoS) offers a detailed view into how the video engine is performing. TVSDK provides detailed statistics about playback, buffering, and devices.
title: Track at the fragment level using load information
exl-id: 29e82a93-783f-4e32-ab5e-12713a60cfec
---
# Track at the fragment level using load information{#track-at-the-fragment-level-using-load-information}

Quality of service (QoS) offers a detailed view into how the video engine is performing. TVSDK provides detailed statistics about playback, buffering, and devices.

TVSDK also provides information about the following downloaded resources:

1. Playlist/manifest files 
1. File fragments 
1. Tracking information for files

   You can read quality of service (QoS) information about downloaded resources, such as fragments and tracks, from the `LoadInfo` class. 

1. Implement the `onLoadInfo` callback event listener.
1. Register the event listener, which TVSDK calls every time a fragment has downloaded.
1. Read the data of interest from the `LoadInfo` parameter that is passed to the callback.

   <table id="table_06BD536A23AB4A73B510998426BAE143"> 
    <thead> 
      <tr> 
      <th colname="col01" class="entry"> Property </th> 
      <th colname="col1" class="entry"> Type </th> 
      <th colname="col2" class="entry"> Description </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col01"> <span class="codeph"> downloadDuration </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> <p>The duration of the download in milliseconds. </p> <p>TVSDK does not differentiate between the time it took the client to connect to the server and the time it took to download the full fragment. For example, if a 10 MB segment takes 8 seconds to download, TVSDK provides that information, but does not tell you that it took 4 seconds until the first byte and another 4 seconds to download the entire fragment. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> mediaDuration </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> The media duration of the downloaded fragments in milliseconds. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> periodIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> The timeline period index associated with the downloaded resource. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> size </span> </td> 
      <td colname="col1"> <span class="codeph"> long </span> </td> 
      <td colname="col2"> The size of the downloaded resource in bytes. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackIndex </span> </td> 
      <td colname="col1"> <span class="codeph"> int </span> </td> 
      <td colname="col2"> The index of the corresponding track, if known; otherwise, 0. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackName </span> </td> 
      <td colname="col1"> <span class="codeph"> String </span> </td> 
      <td colname="col2"> The name of the corresponding track, if known; otherwise, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> trackType </span> </td> 
      <td colname="col1"> <span class="codeph"> String </span> </td> 
      <td colname="col2"> The type of the corresponding track, if known; otherwise, null. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> type </span> </td> 
      <td colname="col1"> <span class="codeph"> String </span> </td> 
      <td colname="col2"> What TVSDK downloaded. One of the following: 
      <ul id="ul_9C3BDEBD878544DA95C7FF81114F9B5C"> 
      <li id="li_A093552B492A44FD8B30785E465F6886">MANIFEST - A playlist/manifest </li> 
      <li id="li_DEF9AC71AA564F9BB4C5D4E834432EE5">FRAGMENT - A fragment </li> 
      <li id="li_57821F47B6F04CD38570BCE6447A01B8">TRACK - A fragment associated with a specific track </li> 
      </ul> Sometimes it might not be possible to detect the type of the resource. If this occurs, FILE is returned. </td> 
      </tr> 
      <tr> 
      <td colname="col01"> <span class="codeph"> url </span> </td> 
      <td colname="col1"> <span class="codeph"> String </span> </td> 
      <td colname="col2"> The URL that points to the downloaded resource. </td> 
      </tr> 
    </tbody> 
   </table>
