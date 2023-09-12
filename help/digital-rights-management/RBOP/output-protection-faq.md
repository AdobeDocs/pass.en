---
description: Frequently asked questions about using resolution-based output protection.
title: RBOP FAQ
exl-id: 16b95db4-43a9-4458-b7f4-94033a36542e
---
# RBOP FAQ {#rbop-faq}

Frequently asked questions about using resolution-based output protection.

* **Q.** *When defining a digital output requirement for a pixel constraint, I'm getting parsing/formatting errors when I leave the HDCP version out, but I don't have any HDCP requirements. How should I configure my digital output requirement in this case?* **A.** Since HDCP version checking is not supported in the client currently, Adobe recommends setting the HDCP version to `1.0`. This will ensure that your configuration is formatted correctly and is semantically consistent in the future when HDCP version checking is supported. The following snippet illustrates a configuration with this HDCP value. 

  ```
  { "pixelConstraints":  
    [  
      { "pixelCount": 720, "digital":  
        [  
          {  
            "output": "REQUIRED", "hdcp": {"major": 1, "minor": 0}  
          }  
        ]  
      }  
    ]  
  }
  ```

* **Q.** *Are RBOP pixel constraints discrete or range based?* **A.** RBOP pixel constraints are ranged based. Each pixel count defines the requirements for all pixel counts less than or equal to the given count or up to the largest count smaller than that value if more than one pixel constraint exists. Simply put, the values apply as maximum thresholds for each vertical pixel count.

  Let's suppose an MBR stream with vertical resolutions of 240, 480, 600, 720, and 1080 is passed to your player with the following RBOP settings.

  **RBOP Policy settings:**

    * 720P - HDCP required 
    * 480P - No OP

  The following rules will be applied to each variant.

  **Streams:**

    * 240, 480: Both are <= 480; no OP shall be required and streams will load with or without HDCP present.
    * 600, 720: Both are <= 720; HDCP is required for playback 
    * 1080: > 720; the stream is block listed (error returned) as it is not found in the rules above.

* **Q.** On some of my Android devices, the pixel count restrictions I have defined are not being applied exactly as defined. What is happening?

  **A.** Some Android devices are reporting frame sizes slightly higher than the normal size. To remedy this situation, adjust your frame sizes ( `maxPixel` and `pixelCount` settings) upward by 20 pixels. For example, adjust your frame size settings upward, from: 

  ```
  { 
      "maxPixel": 800, 
      "pixelConstraints": [ 
          { "pixelCount": 532, 
            "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
            "analog": {"output": "REQUIRED"} 
          }, 
  ... 
  
  ```

  to: 

  ```
  { 
      "maxPixel": 820, 
      "pixelConstraints": [ 
          { "pixelCount": 552, 
            "digital": [{"output": "REQUIRED", "hdcp":{"major": 1,"minor": 0}}], 
            "analog": {"output": "REQUIRED"} 
          }, 
  ... 
  
  ```

  throughout, for all instances of `maxPixel` and `pixelCount`.
