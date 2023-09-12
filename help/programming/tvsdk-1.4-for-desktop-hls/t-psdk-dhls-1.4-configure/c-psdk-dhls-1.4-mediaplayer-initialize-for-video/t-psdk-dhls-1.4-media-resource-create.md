---
description: The MediaResource class represents the content to be loaded by the MediaPlayer instance.
title: Create a media resource
exl-id: 20515e90-cbe4-4945-823a-fe882ed460db
---
# Create a media resource {#create-a-media-resource}

For each new video content, initialize a MediaResource instance with information about the video content and load the media resource.

The MediaResource class represents the content to be loaded by the MediaPlayer instance.

1. Create a `MediaResource` by passing information about the media to the `MediaResource` constructor.

   <table id="table_DD0D5D9129D54F73881399B9B4FF546A"> 
    <thead> 
      <tr> 
      <th colname="col1" class="entry"> Constructor Parameter </th> 
      <th colname="col2" class="entry"> Description </th> 
      </tr>
    </thead>
    =<tbody> 
      <tr> 
      <td colname="col1"><span class="codeph"> url</span> </td> 
      <td colname="col2"> <p>A string that represents the URL of the manifest/playlist of the media. </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> type</span> </td> 
      <td colname="col2"> <p>One of the following string values that corresponds to the indicated file type: 
        <ul id="ul_7512E90B7B294EF9BFBA2D68DE678CBB"> 
        <li id="li_AA84434E84184A3D909552794B425ABD"><span class="codeph"> MP4</span> - ISO base media file format (MP4) </li> 
        <li id="li_8A2F3752569344B59EE30303A8393488"><span class="codeph"> HLS</span> - M3U8 </li> 
        </ul> </p> </td> 
      </tr> 
      <tr> 
      <td colname="col1"><span class="codeph"> metadata</span> </td> 
      <td colname="col2"> <p>An instance of the <span class="codeph"> Metadata</span> class, which might contain custom information about the content to be loaded. </p> <p>Examples of content are alternate or ad content to place inside the main content. If using advertising, set up <span class="codeph"> AuditudeSettings</span> before using this constructor. For more information, see <a href="../../../tvsdk-1.4-for-desktop-hls/ad-insertion/ad-insertion-metadata/c-psdk-dhls-1.4-ad-insertion-metadata.md" format="dita" scope="local"> Ad Insertion Metadata</a>. </p> </td> 
      </tr> 
    </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK supports playback for only specific types of content. If you attempt to load any other type of content, TVSDK dispatches an error event. 
   >
   >For MP4 video-on-demand (VOD) content, TVSDK does not support trick play, adaptive bit rate (ABR) streaming, ad insertion, closed captions, or DRM.

   The following code creates a `MediaResource` instance:

   ```
   // To do: Create metadata here
   MyResource = new MediaResource(
            "https://www.example.com/video/some-video.m3u8", 
            "HLS",
            MyMetadata)
   ```

   >[!TIP]
   >
   >At this point, you can use `MediaResource` accessors (getters) to examine the resource's type, URL, and metadata.

1. Load the media resource by using one of the following:

    * Your MediaPlayer instance.

      For more information, see [Load a media resource in the Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md). 
    * A `MediaPlayerItemLoader` For more information, see [Load a media resource in the Mediaplayer](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-mediaplayer-initialize-for-video/t-psdk-dhls-1.4-media-resource-load.md).
