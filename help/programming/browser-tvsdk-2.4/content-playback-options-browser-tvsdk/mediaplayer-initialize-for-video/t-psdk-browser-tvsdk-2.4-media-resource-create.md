---
description: The MediaResource class represents the content to be loaded by the MediaPlayer instance.
title: Create a media resource
exl-id: ab66255d-7848-479a-a8cd-c6113cdd7749
---
# Create a media resource {#create-a-media-resource}

The MediaResource class represents the content to be loaded by the MediaPlayer instance.

1. Create a `MediaResource` by passing information about the media to the `MediaResource` constructor.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
    <tr> 
    <th colname="col1" class="entry"> Constructor Parameter </th> 
    <th colname="col2" class="entry"> Description </th> 
    </tr> 
    </thead>
    <tbody> 
    <tr> 
    <td colname="col1"> <p>url </p> </td> 
    <td colname="col2"> <p>A string that represents the URL of the manifest/playlist of the media. </p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>type </p> </td> 
    <td colname="col2"> <p>One of the following members of the <span class="codeph"> MediaResource.Type </span> enumeration that corresponds to the indicated file type: </p> <p> 
    <ul id="ul_E9689FA06DC94BF4848F16E1F2F01A59"> 
    <li id="li_83A14B96CDC648C6AF6F5FA745343E1F"> <span class="codeph"> MP4 </span> - ISO base media file format (MP4) </li> 
    <li id="li_FCD355151515412D9A78C3815DD09129"> <span class="codeph"> HLS </span> - M3U8 </li> 
    <li id="li_9D3D306D49264830AC6EFB1F49524A3B"> <span class="codeph"> DASH </span> - MPD </li> 
    </ul> </p> <p></p> </td> 
    </tr> 
    <tr> 
    <td colname="col1"> <p>metadata </p> </td> 
    <td colname="col2"> <p>An instance of the <span class="codeph"> Metadata </span> class, which might contain custom information about the content to be loaded. Examples of content are alternate or ad content to place inside the main content. If using advertising, set up <span class="codeph"> AuditudeSettings </span> before using this constructor. For more information, see <a href="../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md">Ad-insertion-metadata</a>. </p> <p>Tip:  You can force Flash fallback, if necessary, by using the <span class="codeph"> forceFlash </span> parameter when creating a media resource. This can be useful because currently not all of the features (such as Live Ad workflows) are supported in Browser TVSDK. Flash fallback is used to play video content. </p> </td> 
    </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >Browser TVSDK supports playback for only specific types of content. If you attempt to load any other type of content, Browser TVSDK dispatches an error event.

   The following code creates a `MediaResource` instance:

   ```js
   //create a MediaResource instance pointing to some HLS content 
   Metadata metadata = //TODO: create metadata here 
   mediaResource = new AdobePSDK.MediaResource ( 
         "https://www.example.com/video/some-video.m3u8", 
         AdobePSDK.MediaResourceType.HLS,  
         metadata);
   ```

   >[!TIP]
   >
   >At any time after this, you can use `MediaResource` accessors (getters) to examine the resource's type, URL, and metadata.

1. Load your MediaPlayer instance. For more information, see [Load a media resource in the MediaPlayer](../../content-playback-options-browser-tvsdk/mediaplayer-initialize-for-video/t-psdk-browser-tvsdk-2.4-media-resource-load.md).
