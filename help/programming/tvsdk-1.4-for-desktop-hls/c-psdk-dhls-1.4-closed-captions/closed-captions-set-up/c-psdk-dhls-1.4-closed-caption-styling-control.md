---
description: You can provide styling information for closed-caption tracks using the ClosedCaptionStyles class. This sets the style for any closed captions that are displayed by your player.
title: Control closed-caption styling
exl-id: fd94a851-1e8f-4406-a3bb-ca115b4e60f8
---
# Control closed-caption styling{#control-closed-caption-styling}

You can provide styling information for closed-caption tracks using the ClosedCaptionStyles class. This sets the style for any closed captions that are displayed by your player.

This class encapsulates closed-caption styling information such as the font type, size, color, and background opacity. An associated helper class, `ClosedCaptionStylesBuilder`, facilitates working with closed-caption style settings.

## Set closed-caption styles {#section_DAE84659D1964DB1B518F91B59AF29D9}

You can style the closed-caption text with TVSDK methods.

1. Wait for the MediaPlayer to have at least the PREPARED status (see [Wait for a valid state](../../../tvsdk-1.4-for-desktop-hls/t-psdk-dhls-1.4-configure/c-psdk-dhls-1.4-ui-configure/t-psdk-dhls-1.4-ui-state-prepared-wait-for.md)). 
1. To change the styling settings, do one of the following:

    * Use the `ClosedCaptionStylesBuilder` helper class (operates on `ClosedCaptionStyles` behind the scenes). 
    * Use the `ClosedCaptionStyles` class directly.

>[!NOTE]
>
>Setting the closed-caption style is an asynchronous operation so it might take up to a few seconds for the changes to appear on the screen.

## Closed caption styling options {#section_D28F50B98C0D48CF89C4FB6DC81C5185}

You can provide styling information for closed-caption tracks using the `ClosedCaptionStyles` class. This sets the style for any closed captions that are displayed by your player.

```
public function TextFormat( 
   font:String = default,  
   size:String = default,  
   fontEdge:String = default,  
   fontColor:String = default,  
   backgroundColor:String = default,  
   fillColor:String = default,  
   edgeColor:String = default,  
   fontOpacity:int,  
   backgroundOpacity:int,  
   fillOpacity:int)
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
   <td colname="2"> <p>The font type. </p> <p>Can be set only to a value that is defined by the <span class="codeph"> ClosedCaptionStyles.FONT </span> array and represents, for example, monospaced with or without serifs. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;AVCaptionStyle.MONOSPACE_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.MONOSPACED_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITH_SERIFS, 
      &nbsp;AVCaptionStyle.PROPORTIONAL_WITHOUT_SERIFS, 
      &nbsp;AVCaptionStyle.CASUAL, 
      &nbsp;AVCaptionStyle.CURSIVE, 
      &nbsp;AVCaptionStyle.SMALL_CAPITALS 
      &nbsp;]; 
     </code> </p> <p>Tip:  The actual fonts that are available on a device might vary, and substitutions are used when necessary. Monospace with serifs is typically used as a substitute, although this substitution can be system specific. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Size </td> 
   <td colname="2"> <p>The caption's size. </p> <p> Can be set only to a value defined by the <span class="codeph"> ClosedCaptionStyles.FONT_SIZE </span> array: 
     <ul compact="yes" id="ul_544BFC7A46474A74839477108F1AB1E9"> 
      <li id="li_A592ED46B8DF4D8FAD7AF3BD931A712B"> <span class="codeph"> MEDIUM </span> - The standard size </li> 
      <li id="li_4F8CEDE54965430EB707DD3D5B2E3F87"> <span class="codeph"> LARGE </span> - Approximately 30% larger than medium </li> 
      <li id="li_D78D823883F54D869118BAB58257E377"> <span class="codeph"> SMALL </span> - Approximately 30% smaller than medium </li> 
      <li id="li_9299C13408584A38835F8D91BD048083"> <span class="codeph"> DEFAULT </span> - The default size for the caption; the same as medium </li> 
     </ul> </p> <p>Tip:  You can change the font size of WebVTT captions by changing the size parameter for the <span class="codeph"> DefaultMediaPlayer.ccStyles setter </span> function. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Font edge </td> 
   <td colname="2"> <p>The effect used for the font edge, such as raised or none. </p> <p>Can be set only to a value that is defined by the <span class="codeph"> ClosedCaptionStyles.FONT_EDGE </span> array. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;FONT_EDGE&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.NONE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RAISED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEPRESSED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.UNIFORM, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.LEFT_DROP_SHADOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RIGHT_DROP_SHADOW 
      &nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Font color </td> 
   <td colname="2"> <p>The font color. </p> <p>Can be set only to a value defined by the <span class="codeph"> ClosedCaptionStyles.COLOR </span> array. 
     <code class="syntax actionscript">
       public&nbsp;static&nbsp;const&nbsp;COLOR&nbsp;:Array&nbsp;=&nbsp;[ 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DEFAULT, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLACK, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GRAY, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_WHITE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_RED, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_GREEN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_BLUE, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_YELLOW, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_MAGENTA, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.DARK_CYAN, 
      &nbsp;&nbsp;&nbsp;&nbsp;AVCaptionStyle.BRIGHT_CYAN&nbsp;&nbsp;&nbsp;]; 
     </code> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Edge color </td> 
   <td colname="2"> <p>The color of the edge effect. </p> <p>Can be set to any of the values that are available for the font color. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Background color </td> 
   <td colname="2"> <p>The background character cell color. </p> <p>Can be set only to values that are available for the font color. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Fill color </td> 
   <td colname="2"> <p>The color of the background of the window in which the text is located. </p> <p>Can be set to any of the values that are available for the font color. </p> <p>Important:  This does not apply to WebVTT captions, because WebVTT does not use this feature. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Font opacity </td> 
   <td colname="2"> <p>The opacity of the text. </p> <p>Expressed as a percentage from 0 (fully transparent) to 100 (fully opaque). <span class="codeph"> DEFAULT_OPACITY </span> for the font is 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Background opacity </td> 
   <td colname="2"> <p>The opacity of the background character cell. </p> <p>Expressed as a percentage from 0 (fully transparent) to 100 (fully opaque). <span class="codeph"> DEFAULT_OPACITY </span> for the background is 100. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Fill opacity </td> 
   <td colname="2"> <p>The opacity of the background of the caption window. </p> <p>Expressed as a percentage from 0 (fully transparent) to 100 (fully opaque). <span class="codeph"> DEFAULT_OPACITY </span> for fill is 0. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Examples: Caption formatting {#section_63E33840B7A14D26990046E2ACF2ECA1}

You can specify closed-caption formatting.

## Example 1: Specify format values explicitly {#section_BD7B48F3B66D4E9290E1CB2F464E08E4}

```
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    var formatBuilder:TextFormatBuilder = new TextFormatBuilder(); 
    formatBuilder.font = Font.DEFAULT,  
    formatBuilder.fontSize = FontSize.DEFAULT,  
    formatBuilder.fontEdge = FontEdge.DEFAULT,  
    formatBuilder.fontColor = Color.DEFAULT,  
    formatBuilder.backgroundColor = Color.DEFAULT,  
    formatBuilder.fillColor = Color.DEFAULT,  
    formatBuilder.edgeColor = Color.DEFAULT,  
    formatBuilder.fontOpacity = .DEFAULT_OPACITY,  
    formatBuilder.backgroundOpacity = Font.DEFAULT_OPACITY,  
    formatBuilder.fillOpacity = TextFormat.DEFAULT_OPACITY 
    mediaPlayer.set CCStyle(formatBuilder.toTextFormat()); 
} 

```

## Example 2: Specify format values in parameters {#section_147036D7C31C4010A5A7DF49997014A9}

```
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param fontSize 
* The desired text size. 
* @param fontEdge 
* The desired font edge. 
* @param fontColor 
* The desired font color. 
* @param backgroundColor 
* The desired background color. 
* @param fillColor 
* The desired fill color. 
* @param edgeColor 
* The desired color to draw the text edges. 
* @param fontOpacity 
* The desired font opacity. 
* @param backgroundOpacity 
* The desired background opacity. 
* @param fillOpacity 
* The desired fill opacity. 
*/ 
public function TextFormatBuilder(font:Font, fontSize:FontSize, fontEdge:FontEdge,  
                                  fontColor:Color, backgroundColor:Color,  
                                  fillColor:Color, edgeColor:Color, fontOpacity:int, 
                                  backgroundOpacity:int, fillOpacity:int); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public function toTextFormat():TextFormat; 
... 

```
