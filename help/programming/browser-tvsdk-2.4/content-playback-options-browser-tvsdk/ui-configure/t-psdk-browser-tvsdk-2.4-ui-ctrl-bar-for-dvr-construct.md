---
description: You can implement a control bar with DVR support for VOD and live streaming. DVR support includes the concept of a seekable window and the client live point.
title: Construct a control bar enhanced for DVR
exl-id: e4846f1e-bc57-452b-b393-8f8f55434e7a
---
# Construct a control bar enhanced for DVR{#construct-a-control-bar-enhanced-for-dvr}

You can implement a control bar with DVR support for VOD and live streaming. DVR support includes the concept of a seekable window and the client live point.

* For VOD, the length of the seekable window is the duration of the entire asset. 
* For live streaming, the length of the DVR (seekable) window is defined as the time range starting at the live playback window and ending at the client live point.

  The client live point is calculated by subtracting the buffered length from the live window end. The target duration is a value bigger than or equal to the maximum duration of a fragment in the manifest.

  The control bar for live playback supports DVR by first positioning the thumb at the client live point when starting playback and by displaying a region that marks the area where seek is not allowed.

For a control bar:

1. Add an overlay to the control bar that represents the playback range.

1. When the user starts to seek, check whether the desired seek position is within the seekable range.
