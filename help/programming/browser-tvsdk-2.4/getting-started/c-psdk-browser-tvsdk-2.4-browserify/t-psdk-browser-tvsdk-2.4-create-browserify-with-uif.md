---
description: Use the Browserify library files provided by Browser TVSDK in your app to create a Browserify-compatible player using the UI-Framework.
title: Create a Browserify-compatible player using the UI-Framework
exl-id: cd72cae1-f67e-4192-9a7e-1c1492d88922
---
# Create a Browserify-compatible player using the UI-Framework {#create-a-browserify-compatible-player-using-the-ui-framework}

Use the Browserify library files provided by Browser TVSDK in your app to create a Browserify-compatible player using the UI-Framework.

Sample Browserify files included in the TVSDK:

* [!DNL […]/samples/browserify/ui-framework/build/Gruntfile.js] 
* [!DNL […]/samples/browserify/ui-framework/build/package.json] 
* [!DNL […]/samples/browserify/ui-framework/examples/sample.html] 
* [!DNL […]/samples/browserify/ui-framework/examples/sample.js]

To create a Browserify-compatible app using the UI-Framework, you must `require` the two Browserify modules (provided by Browser TVSDK) in your app code: 

1. Require Browserify modules:

   ```
   var AdobePSDK = require('../../../../frameworks/player/AdobePSDK.module.js');  
   var ptp = require('../../../ui-framework/libs/Primetimevisualapi.module.js);  
   […]
   ```

1. Proceed with development as described in [](../../../browser-tvsdk-2.4/getting-started/c-psdk-browser-tvsdk-2.4-create-a-basic-player/t-psdk-browser-tvsdk-2.4-create-basic-player-uif.md).
>You can now bundle your app files using Browserify.
