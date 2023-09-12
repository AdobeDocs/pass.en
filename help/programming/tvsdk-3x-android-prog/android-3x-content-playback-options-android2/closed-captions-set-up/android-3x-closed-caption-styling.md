---
description: You can provide styling information for closed caption tracks using the TextFormat class, which sets the style for closed captions that are displayed by your player.
title: Control closed-caption styling
exl-id: 43c1391d-a937-464f-99fd-fe8deda7da44
---
# Control closed-caption styling {#control-closed-caption-styling}

You can provide styling information for closed caption tracks using the TextFormat class, which sets the style for closed captions that are displayed by your player.

This class encapsulates closed caption styling information such as the font type, size, color, and background opacity.

## Set closed-caption styles {#section_C9B5E75C70DD42E59DC4DD0F308C8216}

You can style the closed-caption text with TVSDK methods.

1. Wait for the media player to be in at least the `PREPARED` status. 
1. Create a `TextFormatBuilder` instance.

   You can provide all the closed-caption styling parameters now or set them later.

   TVSDK encapsulates closed-caption styling information in the `TextFormat` interface. The `TextFormatBuilder` class creates objects that implement this interface.

   ```java
   public TextFormatBuilder( 
      TextFormat.Font font, 
      TextFormat.Size size, 
      TextFormat.FontEdge fontEdge, 
      java.lang.String fontColor, 
      java.lang.String backgroundColor, 
      java.lang.String fillColor, 
      java.lang.String edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity 
      java.lang.String bottomInset, 
      java.lang.String safeArea)
   ```

1. To obtain a reference to an object that implements the `TextFormat` interface, call the `TextFormatBuilder.toTextFormat` public method. 

    This returns a `TextFormat` object that can be applied to the media player.

    `public TextFormat toTextFormat()`
   

1. Optionally get the current closed-caption style settings by doing one of the following:

    * Get all the style settings with `MediaPlayer.getCCStyle` The return value is an instance of the `TextFormat` interface.     
    
      ```java    
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws MediaPlayerException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws MediaPlayerException;
      ```

    * Get the settings one at a time through the `TextFormat` interface getter methods.     
    
      ```java    
      public java.lang.String getFontColor(); 
      public java.lang.String getBackgroundColor(); 
      public java.lang.String getFillColor(); // retrieve the font fill color 
      public java.lang.String getEdgeColor(); // retrieve the font edge color 
      public TextFormat.Size getSize(); // retrieve the font size 
      public TextFormat.FontEdge getFontEdge(); // retrieve the font edge type 
      public TextFormat.Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity(); 
      public java.lang.String getBottomInset(java.lang.String bi); 
      public java.lang.String getSafeArea(java.lang.String sa);
      ```

1. To change the style settings, do one of the following:

    * Use the setter method `MediaPlayer.setCCStyle`, passing an instance of the `TextFormat` interface:     
    
      ```java    
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws MediaPlayerException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws MediaPlayerException;
      ```

    * Use the `TextFormatBuilder` class, which defines individual setter methods.

      The `TextFormat` interface defines an immutable object so there are only getter methods and no setters. You can set the closed-caption styling parameters only with the `TextFormatBuilder` class:     
    
      ```java    
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(String backgroundColor) 
      public void setFillColor(String fillColor) 
      // set the font-edge color 
      public void setEdgeColor(String edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(String fontColor) 
      public void setBottomInset(String bi) 
      public void setSafeArea(String sa) 
      public void setTreatSpaceAsAlphaNum(bool)
      ```

      >[!IMPORTANT]
      >
      >**Color Settings:** In Android TVSDK 2.X, an enhancement was made to color styling of closed captions. The enhancement allows for setting closed caption colors using a hex string representing RGB color values. The RGB hex color representation is the familiar 6 byte string you use in applications such as Photoshop:
      >
      >* FFFFFF = Black 
      >* 000000 = White 
      >* FF0000 = Red 
      >* 00FF00 = Green 
      >* 0000FF = Blue 
      >and so on.
      >
      >In your application, whenever you pass color styling information to `TextFormatBuilder`, you still use the `Color` enumeration as before, but now you must add `getValue()` to the color to get the value as a string. For example:
      >
      >`tfb = tfb.setBackgroundColor(TextFormat.Color.RED      <b>.getValue()</b>);`

Setting the closed-caption style is an asynchronous operation, so it might take up to a few seconds for the changes to appear on the screen.

## Closed caption styling options {#section_6D685EC2D58C42A2BDDD574EDFCCC2A0}

You can specify several caption styling options, and these options override the style options in the original captions. 

```java
public TextFormatBuilder( 
   Font font, 
   Size size, 
   FontEdge fontEdge, 
   String fontColor, 
   String backgroundColor, 
   String fillColor, 
   String edgeColor, 
   int fontOpacity, 
   int backgroundOpacity, 
   int fillOpacity,  
   String bottomInset 
   String safeArea)
```

>[!TIP]
>
>In options that define default values (for example, `DEFAULT`), that value refers to what the setting was when the caption was originally specified.

<table frame="all" colsep="1" rowsep="1" id="table_87205DEFEE384AF4AF83952B15E18A42"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b> Format </b></th> 
   <th colname="2" class="entry"> <b>Description</b> </th> 
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
   <td colname="1"> Font edge </td> 
   <td colname="2"> <p>The effect used for the font edge, such as raised or none. </p> <p>Can be set only to a value that is defined by the <span class="codeph"> TextFormat.FontEdge </span> enumeration. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Font color </td> 
   <td colname="2"> <p>The font color. </p> <p>Can be set only to a value defined by the <span class="codeph"> TextFormat.Color </span> enumeration. </p> </td> 
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
   <td colname="2"> <p>The color of the background of the window in which the text is located. </p> <p>Can be set to any of the values that are available for the font color. </p> </td> 
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
  <tr rowsep="1"> 
   <td colname="1"> Bottom Inset </td> 
   <td colname="2"> <p>Vertical distance from the bottom of the caption window for captions to avoid. </p> <p>Expressed as a percentage of the caption window height (for example, "20%") or a number of pixels (for example, "20"). </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> Safe area </td> 
   <td colname="2"> <p>A region around the edge of the screen between 0% to 25% where captions will not appear. </p> <p>By default, the safe area for WebVTT is 0%. This setting allows your application to override that default. If two values are provided, for example, the string "10%,20%", the first value is the horizontal safe area and the second value is the vertical safe area. If one value is provided, for example, the string "15%", both the vertical and horizontal axes use the specified safe area. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Caption formatting examples {#section_58E8E82494EC4683B010FFDE67485CF9}

Here are some examples that show you how to specify closed caption formatting.

```java
private final MediaPlayer.PlaybackEventListener _playbackEventListener = 
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder( 
            TextFormat.Font.DEFAULT, 
            TextFormat.Size.DEFAULT, 
            TextFormat.FontEdge.DEFAULT, 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.Color.DEFAULT.getValue(), 
            TextFormat.DEFAULT_OPACITY, 
            TextFormat.DEFAULT_OPACITY, 
            TextFormat.DEFAULT_OPACITY).toTextFormat(); 
 
        mediaPlayer.setCCStyle(tf); 
        ... 
    } 
} 

```

```java
/** 
* Constructor using parameters to initialize a TextFormat. 
* 
* @param font 
* The desired font. 
* @param size 
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
public  
<b>TextFormatBuilder</b>( 
    Font font, Size size, FontEdge fontEdge, 
    String fontColor, String backgroundColor,  
    String fillColor, String edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat  
<b>toTextFormat</b>(); 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public  
<b>TextFormatBuilder</b> setFont(Font font); 
...
```
