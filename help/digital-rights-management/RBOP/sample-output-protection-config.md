---
description: This section presents a sample configuration that illustrates the concepts and form of the configuration.
title: Sample RBOP Configuration
exl-id: 0f40be83-9c7f-482b-ac42-9aa4e3f46f58
---
# Sample RBOP Configuration {#sample-rbop-configuration}

This section presents a sample configuration that illustrates the concepts and form of the configuration.

The following sample JSON configuration defines a pixel output policy that specifies the following:

* Restrict decryption of the video to resolutions of 1080 or below 
* Impose specific constraints for resolutions of 720 and 480:

    * For 720 resolution: require HDCP for digital output; require *Copy Generation Management System - Analog* (CGMS-A) protection for analog output. 
    * For 480 resolution: require HDCP for digital output; do not require protection for analog

```
{ 
  "pixelConstraints":  
    [ 
      { 
        "pixelCount": 720, 
        "digital": 
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "REQUIRED_CGMSA"} 
      }, 
      { 
        "pixelCount": 480, 
        "digital":  
          [ 
            {"output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}} 
          ], 
        "analog": {"output": "NO_PROTECTION"} 
      } 
    ], 
  "maxPixel": 1080 
}
```

Note the following about the sample configuration above:

* The `pixelCount` specifications are one level down in the JSON structure, within the `pixelConstraints` section. 

* Within each pixel count specification, output protection is specified for both digital and analog output. 
* In the digital output specifications, HDCP versions are specified, although the client does not currently support HDCP versioning. See the FAQ for more information.
