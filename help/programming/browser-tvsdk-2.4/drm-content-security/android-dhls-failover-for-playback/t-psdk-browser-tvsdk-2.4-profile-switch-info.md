---
description: When the media player switches its current profile to a new profile, you can retrieve information about the switch, including when it switched, width and height information, or why a different bit rate was used.
title: Get information about profile switch
exl-id: 3ef4b319-dd78-4abd-9c2d-ab1d608f6cea
---
# Get information about profile switch{#get-information-about-profile-switch}

When the media player switches its current profile to a new profile, you can retrieve information about the switch, including when it switched, width and height information, or why a different bit rate was used.

1. Listen for the `AdobePSDK.PSDKEventType.PROFILE_CHANGED` event.

   The Browser TVSDK media player dispatches this event when its adaptive bit rate switching algorithm switches to another profile because of network or machine conditions. (When the bit rate or the period changes.)
1. When the event occurs, check the following properties for information about the switch:

    * `profile`: Identifier for the new profile being used. 
    * `time`: The stream time at which the switch occurred. 
    * `description`: Textual description of the reason for a bit rate change, as a string of semicolon-separated key/value pairs. Includes a maximum of one `Reason` and one `Bitrate`. If the information is not available or the bit rate did not change, this string is empty.     
    
    <table id="table_E400FD9C57FF40CBAC14AF6847CD8301"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Key name </th> 
      <th colname="col2" class="entry"> Possible values </th> 
      </tr> 
    </thead>
    <tbody> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Reason </span> </td> 
      <td colname="col2"> 
        <ul id="ul_37DDE3F297634ED6B47DF5D73F969369"> 
        <li id="li_E374B029E1AF40689D70A9D30E057C5B">Network Adaptation </li> 
        <li id="li_753862EEF1C9474EA8E20C89F5EF5D8D">Seek </li> 
        <li id="li_EC14923F92CF4D11A47928A8D2DE6D8B">Profile Not Supported </li> 
        <li id="li_695AB4A89C9D4833AF6D8B6424FC912B">Failover </li> 
        </ul> </td> 
      </tr> 
      <tr> 
      <td colname="col1"> <span class="codeph"> Bitrate </span> </td> 
      <td colname="col2"> 
        <ul id="ul_1B49BD90A91147359712E1AFD8877E23"> 
        <li id="li_1C8E593C65D34742B14A8D0EAD43E0A9"> <span class="codeph"> up </span>: The bit rate increased </li> 
        <li id="li_B1A00E3985A849B6855E15CF70D79BB8"> <span class="codeph"> down </span>: The bit rate decreased </li> 
        </ul> </td> 
      </tr> 
    </tbody> 
    </table>    
    
    Here are some examples of returned `description` strings:     

    ```    
    "Bitrate::=up;Reason::=Network Adaptation;" 
    
    "Bitrate::=down;Reason::=Failover;"
    ```

    * `width`: Integer indicating width in pixels. 
    * `height`: Integer indicating height in pixels.

    >[!NOTE]
    >
    >Width and height data are only available when they are included in the `RESOLUTION` tag in the M3U8 manifest. If the information is not included in the M3U8, the width and height properties are set to 0, as they are not part of the profile information.
