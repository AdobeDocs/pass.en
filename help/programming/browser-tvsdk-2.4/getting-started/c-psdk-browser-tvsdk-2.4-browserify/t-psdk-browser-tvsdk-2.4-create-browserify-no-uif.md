---
description: Use the Browserify library file provided by Browser TVSDK in your app, to create a Browserify-compatible player.
title: Create a Browserify-compatible player without the UI-Framework
exl-id: 27b5e1c5-49c3-44e4-9e34-0f50a50e36f5
---
# Create a Browserify-compatible player without the UI-Framework{#create-a-browserify-compatible-player-without-the-ui-framework}

Use the Browserify library file provided by Browser TVSDK in your app, to create a Browserify-compatible player.

The topic [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md) lists the set of Browser TVSDK libraries that you normally include when you create a basic video player. To do this you simply add `script` tags with `src` attributes pointing to the libraries.

The process is slightly different for creating a Browserify-compatible player. For this, you use the `require` command to include the [!DNL AdobePSDK.module.js] file (provided by the Browser TVSDK) in your app. This file bundles the basic player library files in their proper order of dependency, and returns the `AdobePSDK` namespace you use to implement features for your player.

Browser TVSDK provides the following sample Browserify application and build files in the release package:

* [!DNL […]/samples/browserify/reference/build/Gruntfile.js] 
* [!DNL […]/samples/browserify/reference/build/package.json] 
* [!DNL […]/samples/browserify/reference/examples/sample.html] 
* [!DNL […]/samples/browserify/reference/examples/sample.js]

To create a Browserify-compatible video player: 

1. Require the Browserify-compatible library file that returns the `AdobePSDK` namespace:

   ```
   var AdobePSDK = require('./AdobePSDK.module.js'); 
   var player; 
   function Load () { 
       player = new AdobePSDK.MediaPlayer(); 
   […]
   ```

1. Create your player as described in [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-tvsdk.md).

   Step 1 in this task replaces the step in the basic player instructions in which you source the individual basic player libraries in your app file.
You can now bundle your app files using Browserify.
