---
description: You can set up a user interface control for sound volume.
title: Provide volume control
exl-id: 058d79d2-35cc-4238-8fc1-2820a2d91ffb
---
# Provide volume control{#provide-volume-control}

You can set up a user interface control for sound volume.

1. Wait for the MediaPlayer instance to be in a valid status for this command.

   Any state except for except RELEASED is valid.
1. Call the volume set method on the `MediaPlayer` instance to set the audio volume.

   ```    
   public function set volume(value:Number):void
   ```

   The value for the volume represents the requested volume expressed as a proportion of the maximum volume, where 0 is silent and 1 is the maximum volume.

   <table id="table_144A2B1260374FBE8D976194F602DDC7"> 
   <thead> 
   <tr> 
      <th colname="col1" class="entry"> If the specified volume is </th> 
      <th colname="col2" class="entry"> The resulting volume is </th> 
   </tr> 
   </thead>
   <tbody> 
   <tr> 
      <td colname="col1"> Less than 0 </td> 
      <td colname="col2"> 0 </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Between 0 and 1 </td> 
      <td colname="col2"> The specified volume </td> 
   </tr> 
   <tr> 
      <td colname="col1"> Greater than 1 </td> 
      <td colname="col2"> The value divided by 100 and set to one of the following values: 
      <ul id="ul_8C2282F0EDC44A408820F5768709214F"> 
      <li id="li_B00BC6F4812D4000891358F762C8E492">The result if it is between 0 and 1 </li> 
      <li id="li_03B7F30662554F299320040CAC2DEB7A">1 if the result is greater than 1 </li> 
      </ul> <p>Tip:  This logic handles values that are supplied from clients based on earlier versions of the 
      <span class="codeph">phrases/primetime-sdk-name</span>, where volume values ranged from 0 to 100. </p> </td> 
   </tr> 
   </tbody> 
   </table>
