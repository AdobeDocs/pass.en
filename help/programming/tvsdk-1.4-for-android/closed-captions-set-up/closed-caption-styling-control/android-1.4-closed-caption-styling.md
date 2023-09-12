---
description: You can provide styling information for closed-caption tracks using the TextFormat class. This sets the style for any closed captions that are displayed by your player.
title: Control closed-caption styling
exl-id: 0083c141-9c03-46a2-902b-6e7eebaadea4
---
# Control closed-caption styling {#control-closed-caption-styling-overview}

You can provide styling information for closed-caption tracks using the TextFormat class. This sets the style for any closed captions that are displayed by your player.

This class encapsulates closed-caption styling information such as the font type, size, color, and background opacity. An associated helper class, `TextFormatBuilder`, facilitates working with closed-caption style settings.

## Set closed-caption styles {#set-closed-caption-styles}

You can style the closed-caption text with TVSDK methods.

1. Wait for the media player to be in at least the PREPARED state.
1. Create a `TextFormatBuilder` instance.

   You can provide all the closed-caption styling parameters now or set them later.

   TVSDK encapsulates closed-caption styling information in the `TextFormat` interface. The `TextFormatBuilder` class creates objects that implement this interface.

   ```java
   public TextFormatBuilder( 
      Font font, 
      Size size, 
      FontEdge fontEdge, 
      Color fontColor, 
      Color backgroundColor, 
      Color fillColor, 
      Color edgeColor, 
      int fontOpacity, 
      int backgroundOpacity, 
      int fillOpacity)
   ```

1. To obtain a reference to an object that implements the `TextFormat` interface, call the `TextFormatBuilder.toTextFormat` public method.

   This returns a `TextFormat` object that can be applied to the media player. 

   ```java
   public TextFormat toTextFormat()
   ```

1. Optionally get the current closed-caption style settings by doing one of the following:

    * Get all the style settings with `MediaPlayer.getCCStyle`.

      The return value is an instance of the `TextFormat` interface.     
    
      ```js    
      /** 
      * @return the current closed captioning style.  
      * If no style was previously set, it returns a TextFormat object 
      * with default values for each attribute. 
      * @throws IllegalStateException if media player was already released. 
      */ 
      public TextFormat getCCStyle() throws IllegalStateException;
      ```

    * Get the settings one at a time through the `TextFormat` interface getter methods.     
    
      ```js    
      public Color getFontColor(); 
      public Color getBackgroundColor(); 
      public Color getFillColor(); // retrieve the font fill color 
      public Color getEdgeColor(); // retrieve the font edge color 
      public Size getSize(); // retrieve the font size 
      public FontEdge getFontEdge(); // retrieve the font edge type 
      public Font getFont(); // retrieve the font type 
      public int getFontOpacity(); 
      public int getBackgroundOpacity();
      ```

1. To change the style settings, do one of the following:

   >[!NOTE]
   >
   >You cannot change the size for WebVTT captions.

    * Use the setter method `MediaPlayer.setCCStyle`, passing an instance of the `TextFormat` interface:     
    
      ```js    
      /** 
      * Sets the closed captioning style. Used to control the closed captioning font, 
      * size, color, edge and opacity.  
      * 
      * This method is safe to use even if the current media stream doesn't have closed 
      * captions. 
      * 
      * @param textFormat 
      * @throws IllegalStateException 
      */ 
      public void setCCStyle(TextFormat textFormat) throws IllegalStateException;
      ```

    * Use the `TextFormatBuilder` class, which defines individual setter methods.

      The `TextFormat` interface defines an immutable object so there are only getter methods and no setters. You can set the closed-caption styling parameters only with the `TextFormatBuilder` class:

      ```js    
      // set font type 
      public void setFont(Font font)  
      public void setBackgroundColor(Color backgroundColor) 
      public void setFillColor(Color fillColor) 
      // set the font-edge color 
      public void setEdgeColor(Color edgeColor)  
      // set the font size 
      public void setSize(Size size)  
      // set the font edge type 
      public void setFontEdge(FontEdge fontEdge)  
      public void setFontOpacity(int fontOpacity) 
      public void setBackgroundOpacity(int backgroundOpacity) 
      // set the font-fill opacity level 
      public void setFillOpacity(int fillOpacity)  
      public void setFontColor(Color fontColor)
      ```

Setting the closed-caption style is an asynchronous operation, so it might take up to a few seconds for the changes to appear on the screen.

## Closed caption styling options {#closed-caption-styling-options}

You can specify several caption styling options, and these options override the style options in the original captions

```
public TextFormatBuilder(
 Font font,
 Size size,
 FontEdge fontEdge,
 Color fontColor,
 Color backgroundColor,
 Color fillColor,
 Color edgeColor,
 int fontOpacity,
 int backgroundOpacity,
 int fillOpacity,
 String bottomInset)
```

>[!TIP]
>
>In options that define default values (for example, DEFAULT), that value refers to what the setting was when the caption was originally specified.

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
 </tbody> 
</table>

## Caption formatting examples {#examples-caption-formatting}

You can specify closed-caption formatting.

**Example 1: Specify format values explicitly**

```java
private final MediaPlayer.PlaybackEventListener  
  _playbackEventListener = new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // Set CC style. 
        TextFormat tf = new TextFormatBuilder(TextFormat.Font.DEFAULT, 
        TextFormat.Size.DEFAULT, 
        TextFormat.FontEdge.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.Color.DEFAULT, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY, 
        TextFormat.DEFAULT_OPACITY).toTextFormat(); 
        mediaPlayer.setCCStyle(tf); 
        ... 
    } 
} 

```

**Example 2: Specify format values in parameters**

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
public TextFormatBuilder( 
    Font font, Size size, FontEdge fontEdge, 
    Color fontColor, Color backgroundColor,  
    Color fillColor, Color edgeColor, 
    int fontOpacity, int backgroundOpacity, 
    int fillOpacity); 
 
/** 
* Creates a TextFormat with the parameters supplied to this builder. 
*/ 
public TextFormat toTextFormat(); 
 
/** 
* Sets the text font. 
* @param font The desired font 
* @return This builder object to allow chaining calls 
*/ 
public TextFormatBuilder setFont(Font font); 
... 

```
