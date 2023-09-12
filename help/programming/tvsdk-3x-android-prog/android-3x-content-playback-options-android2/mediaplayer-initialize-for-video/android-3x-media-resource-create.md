---
description: The MediaResource class represents the content to be loaded by the MediaPlayer instance.
title: Create a media resource
exl-id: d9693ee5-c192-4ac5-925a-d64e629920b4
---
# Create a media resource {#create-a-media-resource}

For each new video content, initialize a MediaResource instance with information about the video content and load the media resource.

The MediaResource class represents the content to be loaded by the MediaPlayer instance.

1. Create a `MediaResource` by passing information about the media to the `MediaResource` constructor.

   The `MediaResource` constructor requires the following parameters:

   <table id="table_22886D6770FB45E99D35D0B90E6CC302"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> Constructor Parameter </th> 
      <th colname="col2" class="entry"> Description </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> <span class="codeph"> url </span> </td> 
      <td colname="col2"> A string representing the URL of the manifest/playlist of the media. </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> type </span> </td> 
      <td colname="col2"> One of the following members of the <span class="codeph"> MediaResource.Type </span> enum, corresponding to the indicated file type: 
      <ul id="ul_C286ED3C31364B858A1C9AF3356E9282"> 
      <li id="li_25B24EF76D8849DE8764539F25E435FA"> <span class="codeph"> HLS </span> - M3U8 </li> 
      <li id="li_1344A41B434D49229E392F1AAF9ECA81"> <span class="codeph"> ISOBMFF </span> - ISO base media file format (MP4) </li> 
      <li id="li_92392073B7334916B06B16570C51AC91"> <span class="codeph"> DASH </span> - MPEG-DASH media presentation description (MPD) </li> 
      </ul> </td> 
   </tr> 
   <tr> 
      <td colname="col1"> <span class="codeph"> metadata </span> </td> 
      <td colname="col2"> An instance of the <span class="codeph"> Metadata </span> class (a dictionary-like structure), which might contain additional information about the content that is about to be loaded, such as alternate or ad content to place inside the main content. If using advertising, set up <span class="codeph"> AuditudeSettings </span> before using this constructor <a href="/help/programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-insertion-metadata/android-3x-ad-insertion-metadata.md"> Ad insertion metadata </a>. </td> 
   </tr> 
   </tbody> 
   </table>

   >[!IMPORTANT]
   >
   >TVSDK supports playback for only specific types of content. If you attempt to load any other type of content, TVSDK dispatches an error event. 
   >
   >For MP4 video-on-demand (VOD) content, TVSDK does not support trick play, adaptive bit rate (ABR) streaming, ad insertion, closed captions, or DRM. 

   The following code creates a `MediaResource` instance:        >

   ```java
   // To do: Create metadata here 
   MediaResource res = new MediaResource( 
     "https://www.example.com/video/some-video.m3u8",  
   MediaResource.Type.HLS, 
     metadata); 
   ```

   At any time after this step, you can use `MediaResource` accessors (getters) to examine the resource's type, URL, and metadata. 
    
1. Load the media resource using one of the following options:

   * The MediaPlayer instance. 
   * `MediaPlayerItemLoader` For more information, see [Load a media resource using MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

   >[!IMPORTANT]
   >
   >Do not load the media resource on a background thread. Most TVSDK operations need to run on the main thread, and running them on a background thread can cause the operation to throw an error and exit.
