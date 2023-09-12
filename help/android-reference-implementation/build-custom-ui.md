---
description: You can easily build a custom user interface based on the reference implementation framework.
title: Build a custom user interface
exl-id: 96008010-cd63-4fb1-a3fc-2fc94b624413
---
# Build a custom user interface {#build-a-custom-user-interface}

You can build a custom user interface based on the reference implementation framework.

The UI components of the following features are already integrated:

* Clickable ads 
* Ad overlays 
* Late-binding audio 
* Closed captions 
* Listeners for all of the above components

1. Edit the [!DNL PlayerFragment.java] file to initialize the UI components that you want to use in your player.

1. Edit the [!DNL res/player/player_fragment.xml] file to customize the user interface.
1. Build the project.

>[!NOTE]
>
>To make UI changes to the seek bar, you can edit the MarkableSeekBar class. The [MarkableSeekBar](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/ui/player/MarkableSeekBar.html) class handles the slider, thumb of the slider, ad marker holder, cue markers, buffer range, and seek range backgrounds.
