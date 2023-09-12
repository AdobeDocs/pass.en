---
description: TVSDK features are driven by configuration and implemented through the MediaPlayer.
title: Creating feature managers by passing configuration information to the MediaPlayer
exl-id: 47377ceb-ed3e-4dca-9b55-82e4fe6b0194
---
# Creating feature managers by passing configuration information to the MediaPlayer {#creating-feature-managers-by-passing-configuration-information-to-the-mediaplayer}

TVSDK features are driven by configuration and implemented through the MediaPlayer.

* Configuration is the list of specific settings for the feature, such as initial bit rate of ABR control and default closed captioning visibility.

  Feature managers need to get the configurations in order to determine the feature behavior.

  In the Primetime reference implementation, the configuration is stored in shared preferences, but you can store the configuration in whatever way makes sense for your environment. 

* `MediaPlayer` is the TVSDK media player object that contains the video resource.

  Feature managers register TVSDK event listeners to this player object, retrieve data from the playback session and trigger TVSDK features to the playback session.

Each feature has a corresponding configuration interface. For example, `CCManager` uses `ICCConfig` to retrieve the configuration. `ICCConfig` contains methods to get the configuration information related to closed captioning only.

The following example shows the [!DNL ICCConfig.java] file, configured to receive information about closed caption visibility, font style, and font edge from the `MediaPlayer`:

```java
// Constructor of CCManager 
 
<b>public CCManager(ICCConfig ccConfig, MediaPlayer mediaPlayer) {...}</b> 
  
// ICCConfig methods 
 
<b>public interface ICCConfig {</b> 
  
    /** 
     * Get the closed captioning visibility config 
     * 
     * @return true if visibility is set to true, false otherwise 
     */ 
    
<b> public boolean getCCVisibility();</b> 
  
    /** 
     * Get the closed captioning font style 
     * 
     * @return TextFormat.Font object represents font style 
     */ 
     
<b>public TextFormat.Font getCCFont();</b>

    /** 
     * Get the closed captioning font edge 
     * 
     * @return TextFormat.FontEdge represents of font edge 
     */ 
     
<b>public TextFormat.FontEdge getCCFontEdge();</b> 
... 
}
```

An application that uses a TVSDK feature can create its feature manager with a configuration provider and a `MediaPlayer` object. For example:

```java
// This application needs to use the advertising workflow feature 
AdsManager adsManager = new AdsManagerOn();
```

Feature manager configuration API docs: [Javadoc](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/config/package-summary.html)
