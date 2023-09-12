---
description: You can specify several caption styling options, and these options override the style options in the original captions.
title: Closed caption styling options
exl-id: df5377c2-741b-4239-b345-145753896c6b
---
# Closed caption styling options{#closed-caption-styling-options}

You can specify several caption styling options, and these options override the style options in the original captions.

```js
new TextFormat( 
   font,  
   fontColor,  
   edgeColor,  
   fontEdge,  
   backgroundColor,  
   fillColor,  
   size,  
   fontOpacity,  
   backgroundOpacity,  
   fillOpacity, 
   bottomInset, 
   safeArea) 
```

>[!TIP]
>
>In options that define default values (for example, `DEFAULT`), that value refers to what the setting was when the caption was originally specified.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Format </th> 
   <th colname="2" class="entry"> Description </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Font </td> 
   <td colname="2"> <p>The font type. </p> <p>Can be set only to a value that is defined by the <span class="codeph"> TextFormat.Font </span> enumeration and represents, for example, monospaced with or without serifs. </p> <p>Tip:  The actual fonts that are available on a device might vary, and substitutions are used when necessary. Monospace with serifs is typically used as a substitute, although this substitution can be system specific. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Size </td> 
   <td colname="2"> <p>The caption's size. </p> <p> Can be set only to a value defined by the <span class="codeph"> TextFormat.Size </span> enumeration: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIUM </span> - The standard size </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> LARGE </span> - Approximately 30% larger than medium </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> SMALL </span> - Approximately 30% smaller than medium </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> DEFAULT </span> - The default size for the caption; the same as medium </li> 
     </ul> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Font color </td> 
   <td colname="2"> <p>The font color. </p> <p>Can be set only to a value defined by the <span class="codeph"> TextFormat.Color </span> enumeration. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Background color </td> 
   <td colname="2"> <p>The background character cell color. </p> <p>Can be set only to values that are available for the font color. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Font opacity </td> 
   <td colname="2"> <p>The opacity of the text. </p> <p>Expressed as a percentage from 0 (fully transparent) to 100 (fully opaque). <span class="codeph"> DEFAULT_OPACITY </span> for the font is 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Bottom inset </td> 
   <td colname="2"> <p>Vertical distance from the bottom of the caption window for captions to avoid. </p> <p>Expressed as a percentage of the caption window height (for example, "20%") or a number of pixels (for example, "20"). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Safe area </td> 
   <td colname="2"> <p>A region around the edge of the screen between 0% to 25% where captions will not appear. </p> <p>By default, the safe area for 608/708 is 12% and the safe area for WebVTT is 0%. This setting allows your application to override that default. If two values are provided, for example, the string "10%,20%", the first value is the horizontal safe area and the second value is the vertical safe area. If one value is provided, for example, the string "15%", both the vertical and horizontal axes use the specified safe area. </p> </td> 
  </tr> 
 </tbody> 
</table>
